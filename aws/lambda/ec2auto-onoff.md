# Lambda ec2 auto on off

https://aws.amazon.com/ko/premiumsupport/knowledge-center/start-stop-lambda-cloudwatch/


### region 확인 후 코드 부분 수정 

끄는 거 

```python
import boto3
region = 'ap-northeast-2'
instances = ['i-12345cb6de4f78g9h', 'i-08ce9b2d7eccf6d26']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.stop_instances(InstanceIds=instances)
    print('stopped your instances: ' + str(instances))
```
키는 거

```python
import boto3
region = 'ap-northeast-2'
instances = ['i-12345cb6de4f78g9h', 'i-08ce9b2d7eccf6d26']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.start_instances(InstanceIds=instances)
    print('started your instances: ' + str(instances))
```

### lambda role에서 ec2 권한 할당해야함

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Start*",
        "ec2:Stop*"
      ],
      "Resource": "*"
    }
  ]
}

```

### cloudwatch 시간 설정

KMT 기준 평일 오전 7:00 ~ 오후 7:00 (주말 off) crontab

KMT는 GMT+9 시간이므로 생각해봐라,,,

```
0 22 ? * SUN-THU *
0 10 ? * MON-FRI *
```


