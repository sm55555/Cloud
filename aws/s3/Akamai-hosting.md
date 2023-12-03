### Akamai CDN으로 hosting

단계

### 1. Iam 유저 생성 (해당 버킷에 Get 권한만 있는, List까지 있으면 최상단 접속하면 리스트가 다 보인다.)

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

### 2. 해당 Bucket CORS 설정

```
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "HEAD"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]
```

#### 3. Akamai에 해당 정보 전달 및 테스트 URL 검증 지원


