### ec2에서 s3 접근 시

아래 에러 시 policy 추가 후 role에 추가해야한다. 

```
com.amazonaws.services.kms.model.AWSKMSException: User: arn:aws:sts::111111111111:assumed-role/test-role/i-111111111111 is not authorized to
perform: kms:GenerateDataKey on resource: arn:aws:kms:ap-northeast-2:111111111111:key/ because no resource-based 
policy allows the kms:GenerateDataKey action (Service: AWSKMS; Status Code: 400; Error Code: AccessDeniedException;)
```

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:GenerateDataKey",
		"kms:Decrypt"
            ],
            "Resource": "*"
        }
    ]
}

```

처음에 키를 생성해야하기에 "kms:GenerateDataKey" 권한이 필요

![image](https://user-images.githubusercontent.com/38831314/140848427-01058cbc-aee5-4e04-bfb0-ece2e123a373.png)

그 다음 데이터 복호화를 위해 "kms:Decrypt" 권한이 필요

![image](https://user-images.githubusercontent.com/38831314/140848514-cc2abf7f-b4f6-43b9-be40-66b74a9acb9b.png)


참고 URL

https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html



