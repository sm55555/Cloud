
```python
import boto3
import requests
import json
from slacker import Slacker
from base64 import b64decode
#from slack_sdk import WebClient

def process_tags_in_batches(elbv2, lb_arns):
    all_tag_descriptions = []
    for i in range(0, len(lb_arns), 20):
        batch = lb_arns[i:i + 20]
        tag_descriptions = elbv2.describe_tags(ResourceArns=batch)
        all_tag_descriptions.extend(tag_descriptions['TagDescriptions'])
    return all_tag_descriptions

def parse_lb_name_from_arn(arn):
    """Extract the load balancer name for its ARN"""
    parts = arn.split('/')
    if 'loadbalancer' in arn:
        return parts[-2]
    return 'Unknown'

result = ""
terminate_emoji = '☠️'
ok_emoji = '✅'
channel = "#aws-terminate-resource"

# EC2
ec2 = boto3.client('ec2', 'ap-northeast-2')
    # Search for EC2 instances with tag key "terminated"
ec2_response = ec2.describe_instances()
for reservation in ec2_response['Reservations']:
    for instance in reservation['Instances']:
        # Retrieve name tag value if exists
        terminated_tag = next((tag['Value'] for tag in instance.get('Tags', []) if tag['Key'] == 'terminated'), None)
        name_tag = next((tag['Value'] for tag in instance.get('Tags', []) if tag['Key'] == 'Name'), None)
        if terminated_tag:
            result += "EC2 -> " + name_tag
            result +="\n"
            result += "It will terminate -> " + terminated_tag
            result +="\n"

# S3
result +="\n"
s3 = boto3.client('s3')
buckets = s3.list_buckets()
filtered_buckets = []
   
for bucket in buckets['Buckets']:
   
    bucket_name = bucket['Name']
   
    try:
        # Get the bucket tagging
        tags = s3.get_bucket_tagging(Bucket=bucket_name)
        bucket_tags = {tag['Key']: tag['Value'] for tag in tags['TagSet']}
       
        # Check for 'terminated' tag and 'Name' tag
        terminated_tag = bucket_tags.get('terminated', None)
   

        # Check if 'terminated' tag is present and not empty
        if terminated_tag is not None and terminated_tag.strip() != '':
            bucket_info = {
                'BucketName' : bucket_name,
                'Terminated' : terminated_tag
            }
            print("S3 Bucket Name is " + bucket_name)
            print("It will terminate -> " + terminated_tag)
       
          
    except s3.exceptions.ClientError as e:
        if e.response['Error']['Code'] == 'NoSuchTagSet':
            print(f"NoSuchTagSet")
        else:    
            print(f"else")
        
    except Exception as e:
        # Handle cases where the bucket may not have any tags or other errors
        print(f"Error retrieving tags for bucket {bucket['Name']}: {str(e)}")

# Create an IAM client
result +="\n"
iam = boto3.client('iam')

# List all IAM users
users = iam.list_users()
user_info_list = []

# Iterate over each user
for user in users['Users']:
    user_name = user['UserName']
    # Get tags for each user
    tags = iam.list_user_tags(UserName=user_name)

    # Check for 'terminated' tag and print information
    for tag in tags['Tags']:
        if tag['Key'] == 'terminated':
            result += "IAM User -> " + user_name
            result +="\n"
            result += "It will terminate -> " + tag['Value']
            result +="\n"
        
#Security Groups
result +="\n"
security_groups = ec2.describe_security_groups()

# Iterate over each security group
for sg in security_groups['SecurityGroups']:
    # Extract tags into a dictionary for easy access
    tags_dict = {tag['Key']: tag['Value'] for tag in sg.get('Tags', [])}
   
    # Check for 'terminated' tag and get 'Name' tag
    terminated_tag = tags_dict.get('terminated', None)
    name_tag = tags_dict.get('Name', None)

    # Print and collect information if 'terminated' tag is found
    if terminated_tag:
        sg_info = {
            'SecurityGroupName': sg['GroupName'],
            'TerminatedTagValue': terminated_tag,
            'NameTagValue': name_tag
        }
        result += "Security Group -> " + sg['GroupName']
        result +="\n"
        result += "It will terminate -> " + terminated_tag
        result +="\n"

# Create an ELB client
result +="\n"
elbv2 = boto3.client('elbv2')
elb = boto3.client('elb')

# Initialize lists for data collection
all_lbs = []
all_tag_descriptions = []

# Handle ELBv2 (ALBs and NLBs)
paginator_v2 = elbv2.get_paginator('describe_load_balancers')
page_iterator_v2 = paginator_v2.paginate()

for page in page_iterator_v2:
    all_lbs.extend(page['LoadBalancers'])

lb_arns = [lb['LoadBalancerArn'] for lb in all_lbs]
if lb_arns:
    all_tag_descriptions.extend(process_tags_in_batches(elbv2, lb_arns))
    # Process ELBv2 tags
    for tag_desc in all_tag_descriptions:
        tags_dict = {tag['Key']: tag['Value'] for tag in tag_desc['Tags']}
        terminated_tag = tags_dict.get('terminated', None)
        name_tag = tags_dict.get('Name', 'No Name Tag')  # Default if no Name tag
        lb_name = parse_lb_name_from_arn(tag_desc['ResourceArn'])
    
        if terminated_tag:
            result += "Loadbalancer -> " + lb_name
            result +="\n"
            result += "It will terminate -> " + terminated_tag
            result +="\n"
       

# Handle Classic Load Balancers (CLBs)
clbs = elb.describe_load_balancers()
clb_names = [clb['LoadBalancerName'] for clb in clbs['LoadBalancerDescriptions']]
if clb_names:
    tag_descriptions_clb = elb.describe_tags(LoadBalancerNames=clb_names)
    # Process CLB tags
    for tag_desc in tag_descriptions_clb['TagDescriptions']:
        tags_dict = {tag['Key']: tag['Value'] for tag in tag_desc['Tags']}
        terminated_tag = tags_dict.get('terminated', None)
        if terminated_tag:
            result += "Loadbalancer -> -> " + tag_desc['LoadBalancerName']
            result +="\n"
            result += "It will terminate -> " + terminated_tag
            result +="\n"



# Slack 연동 부분

def lambda_handler(channel, text):
    attachments_dict = dict()
    if len(result) < 5:
        attachments_dict['pretext'] = ok_emoji + " terminate-resource : " + '*test(12312312321312)*'
        attachments_dict['text'] = "Nothing"
        attachments_dict['color'] = '#344FEB'
    else:
        attachments_dict['pretext'] = terminate_emoji + " terminate-resource : " + '*test(12312312321312)*'
        attachments_dict['text'] = result
        attachments_dict['color'] = '#FF0000'
    attachments_dict['mrkdwn_in'] = ["text"]
    attachments = [attachments_dict]

    token = "xoxb-111111111111111111111111111111111111111111"
    channel = "#aws-terminate-resource"
    requests.post("https://slack.com/api/chat.postMessage",headers={"Authorization": "Bearer "+ token},data={"channel":channel,"attachments":json.dumps(attachments)})
```
