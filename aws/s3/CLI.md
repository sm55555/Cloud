### 파일이름으로 S3 검색

```
aws s3 ls s3://your-bucket/ --recursive | grep your-search | cut -1
```
