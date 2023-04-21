### ARN이 자기인 경우에만 tags 바꾸기

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DeleteTags",
                "ec2:CreateTags",
		"ec2: Describelnstances"
            ],
            "Resource": "*"
            "Condition":{
              "StringEquals": {
                 "aws:ARN": "${ec2:SourcelnstanceARN}"
              },
               "ForAllValues:StringEquals": {
                  "aws:test": "Testnumber"
              }
            }
        }
    ]
}
```
