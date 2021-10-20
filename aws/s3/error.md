## aws cli cp 에러
```
aws s3 cp D:\util\test\test.txt s3://test/

Failed to connect to proxy URL: "https://127.0.0.1:8080"

```

아래 내용으로 조치하면 된다..

![image](https://user-images.githubusercontent.com/38831314/132426046-d3f3fb32-3229-4faf-b09d-817690d07430.png)


### s3 Access Denied

에러 상세 내용

```
2021-10-13 00:59:28 aaaaaaaa-bbbb-cccc-dddd-89ac9ea9e0fb DEBUG AwsS3Handler:708 - [upload exception = Access Denied (Service: Amazon S3; Status Code: 403; 
Error Code: AccessDenied; Request ID: ASDSAD123ASDXZC; S3 Extended Request ID: asjdksdjsajkdsa)]
```

CloudTrail로 에러 로그 확인 

Username을 람다함수로 확인한다. Error code toggle 활성화해서 검색

에러 내용에 따라 IAM Role 변경 가능IAM role session 때문에 람다를 즉시 deploy해야 바로 반영됨

![image](https://user-images.githubusercontent.com/38831314/137048615-255f3a97-9722-4b74-b93c-5b98c1618bcd.png)

[조치사항]

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt",
                "kms:GenerateDataKey"
            ],
            "Resource": "*"
        }
    ]
}
```

안되면 KMS 풀권한 부여 (IAM Police에서 Resource 범위 보고 넣어주자..... 범위 제한 되어 있으면 제대로 넣어도 동작안함)

[참고 URL]

https://docs.aws.amazon.com/streams/latest/dev/permissions-user-key-KMS.html

https://aws.amazon.com/ko/premiumsupport/knowledge-center/s3-troubleshoot-403/


### ec2 -> s3 접근 이슈

1. 일단 접근하느 버킷 되는지 확인

aws s3api head-object  --bucket [name] -key [fileName] 명령어를 통해 조회 -> 성공하면 현재 접속 문제 없음 성공하면 아래와 같이 나옴

![image](https://user-images.githubusercontent.com/38831314/138027687-c3933124-c9af-436e-b541-c892b3da4e80.png)

2. 아래 이슈,,,정확한 원인 파악 하기







