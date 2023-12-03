### Akamai CDN으로 hosting

단계

Iam 유저 생성 (해당 버킷에 Get 권한만 있는, List까지 있으면 최상단 접속하면 리스트가 다 보인다.)

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":
            "s3:GetObject"
         "Resource":[
            "arn:aws:s3:::DOC-EXAMPLE-BUCKET1/*",
            "arn:aws:s3:::DOC-EXAMPLE-BUCKET1",
        ]
      }
   ]
}
```
