## EC2 List 출력

```python
import boto3
region = 'ap-south-1'

ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    instance_ids = []
    response = ec2.describe_instances(Filters=[{'Name': 'instance-type', 'Values': ["t2.micro", "t3.micro"]}])
    instances_full_details = response['Reservations']
    for instance_detail in instances_full_details:
        group_instances = instance_detail['Instances']

        for instance in group_instances:
            instance_id = instance['InstanceId']
            instance_ids.append(instance_id)
    return instance_ids
```

https://stackoverflow.com/questions/64801543/aws-lambda-to-list-ec2-instance-id-using-python-boto3
