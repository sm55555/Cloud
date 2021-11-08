# Lambda ec2 auto on off

https://aws.amazon.com/ko/premiumsupport/knowledge-center/start-stop-lambda-cloudwatch/


### region 확인 후 코드 부분 수정 

ap-northeast-2

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

오전 8:30 ~ 오후 5:30 (주말 off)
30 23 ? * SUN-THU *
30 8 ? * SUN-THU *



