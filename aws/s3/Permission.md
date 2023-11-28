### 아래와 같은 방식으로 Bucket(Public)으로 접속하는 IP를 차단한다. 내부 시스템이라도 NAT 타고 나오면 해당 IP를 넣어주면 막힌다.

```yml
{
  "Id": "SourceIP",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SourceIP",
      "Action": "s3:*",
      "Effect": "Deny",
      "Resource": [
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET",
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
      ],
      "Condition": {
        "NotIpAddress": {
          "aws:SourceIp": [
            "11.11.11.11/32",
            "22.22.22.22/32"
          ]
        }
      },
      "Principal": "*"
    }
  ]
}
```

### 특정 버킷에 하위 폴더에만 권한 줄때 my-company버킷 home/David/ 하위 폴더에

이렇게 하면 조회 DOC-EXAMPLE-BUCKET 다 되지만, sync 명령어등 GetObjec는DOC-EXAMPLE-BUCKET/temp/하위만 먹힘

```yml
{
  "Id": "SourceIP",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": [
          "s3:GetObject",
          "s3:ListBucket"
      ]
      "Resource": [
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET",
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET/temp/*"
      ]
    }
  ]
}
```
