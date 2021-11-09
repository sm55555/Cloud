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


