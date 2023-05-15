아래와 같은 방식으로 Bucket(Public)으로 접속하는 IP를 차단한다. 내부 시스템이라도 NAT 타고 나오면 해당 IP를 넣어주면 막힌다.

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
