### 파일이름으로 S3 검색

```
aws s3 ls s3://your-bucket/ --recursive | grep your-search | cut -1
```

### S3 에 파일 업로드

```
aws s3 cp "로컬 경로" "S3 버킷 경로"
aws s3api put-object --bucket dev-test --key text.txt --region ap-northeast-2
```

### S3 에서 파일 다운로드

```
aws s3 cp "S3 버킷 경로" "로컬 경로"
aws s3 cp s3://dev-test/text.txt /home/ec2-user --region ap-northeast-2
```
### S3 에 폴더 업로드

```
aws s3 cp "로컬 경로" "S3 버킷 경로" --recursive
```

### S3 에서 폴더 다운로드

```
aws s3 cp "S3 버킷 경로" "로컬 경로" --recursive
```
