### IP 및 Role로 제한

test bucket 사용할때만, ip와 role 로 제한한다. 나머지는 정상 통신

```
{
	"Version": "2008-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": "*",
			"Action": "*",
			"Resource": "*"
		},
		{
			"Effect": "Deny",
			"Principal": "*",
			"Action": "s3:*",
			"Resource": [
				"arn:aws:s3:::test/*",
				"arn:aws:s3:::test"
			],
			"Condition": {
				"StringNotEquals": {
					"aws:PrincipalArn": [
						"arn:aws:iam::123412341234:role/call-role",
						"arn:aws:iam::123412341234:role/call-role"
					]
				}
			}
		},
		{
			"Effect": "Deny",
			"Principal": "*",
			"Action": "s3:*",
			"Resource": [
				"arn:aws:s3:::test/*",
				"arn:aws:s3:::test"
			],
			"Condition": {
				"StringEquals": {
				// 해당 서버가 있는 VPC 정보
					"aws:SourceVpc": "vpc-1234123412314"
				},
				// 해당 서버의 IP 
				"NotIpAddress": {
					"aws:VpcSourceIp": [
						"192.168.123.123/32",
						"192.168.123.124/32"
					]
				}
			}
		}
	]
}
```
