## Trust Relationship

```
IAM Role trust policy는 Role에 연결되는 정책으로 역할을 수임할 수 있는 보안 주체 Entity를 정의하는 정책입니다.
```

![image](https://user-images.githubusercontent.com/38831314/148474544-fc4d8b66-724e-4a30-b808-46d7bbb33111.png)


![image](https://user-images.githubusercontent.com/38831314/148474804-142274ef-a6e7-40dd-8015-a511193a8c14.png)


### Edit trust relationship

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

자신 계정의 특정권한을 -> 타인에게 사용할 수 있게 허락해준다. 여기서는 ReadOnlyAcceess

<strong>sts:AssumeRole</strong> 의미는? 이 Role(역할)의 행동을 맡기겠다는 의미입니다.
더 정확하게 말하면 특정 Role(Role에 결부된 권한)을 임시로 인수(Assume)한다라는 행동입니다.

