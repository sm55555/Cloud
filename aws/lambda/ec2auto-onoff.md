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

KMT 기준 평일 오전 7:00 ~ 오후 7:00 (주말 off)

0 22 ? * SUN-THU *

0 10 ? * MON-FRI *



