### PassRole 관련

```cmd
com.amazonaws.services.lambda.model.AWSLambdaException: User: arn:aws:iam::11111111:user/test
is not authorized to perform: iam:PassRole on resource: arn:aws:iam::11111111:role/service-role/
Lambda-role
```
위와 같은 이슈가 있을때 test 계정 Policy부분에서 PassRole을 추가하면 된다.

![image](https://user-images.githubusercontent.com/38831314/135800034-f1dbdf0f-a12b-4095-8c4b-22389d36e0c9.png)

```cmd
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "lambda:*",
                "iam:GetRole",
                "iam:PassRole"
            ],
            "Resource": "*"
        }
    ]
}
```
