## Trust Relationship

```
IAM Role trust policy는 Role에 연결되는 정책으로 역할을 수임할 수 있는 보안 주체 Entity를 정의하는 정책입니다.
```

![image](https://user-images.githubusercontent.com/38831314/148474373-385358c8-91fc-40c2-8735-960eb15e49e2.png)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {}
    }
  ]
}

```
