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
### 로컬 -> S3 에 폴더 업로드

```
aws s3 sync /home/user/sm55555/datafolder s3://test-bucket/img/ --region ap-northeast-2
```

### S3 에서 폴더 다운로드

```
aws s3 cp "S3 버킷 경로" "로컬 경로" --recursive
```

### S3 특정 하위 폴더에서 특정 조건에 맞는 파읾만 다운로드

test 버킷 하위에 /data가 있고 그 하위에 여러 파일이 있다고 가정하고, /data 하위에 20230923이 들어간 파일들

```
aws s3 cp s3://test/data/ /home/test --recursive --exclude "*" --include "*20230923*"
```

## S3 동기화

aws sync 명령어는 기본적으로 하위까지 하기 때문에 --recursive 가 필요 없다.

```
test 버킷에서 -> 로컬 서버 /home/ec2-user/img 위치로 파일 변경

aws s3 sync /<ORIGIN_PATH> /<TARGET_PATH>

aws s3 sync s3://test /home/ec2-user/img
```

## S3 Object 삭제

```
# 디렉터리 내 파일을 삭제하되 .sh로 끝나는 파일은 남겨두기 위해, --exclude 옵션으로 *.sh 패턴을 지정. 
$ aws s3 rm --recursive --exclude "*.sh" s3://test/rm_test/
```

## S3 명령어 임시 테스트

```
# 결과 출력 시, dryrun임을 표시하여 실제로 수행되지 않았음을 알려준다.
$ aws s3 rm s3://test-bucket-inpa/folder1/ --dryrun
(dryrun) delete: s3://test-bucket-inpa/folder1/
```

## S3 특정 기간 이후 업로드 된 파일 조회

2024년 2월 1일 이후 데이터 조회

```
aws s3api list-objects --bucket TestBucket --query "Contents[?LastModified>= '2024-02-01'].Key" --output json | jq -r '.[]'
```

그 데이터들을 Download

```
aws s3api list-objects --bucket TestBucket --query "Contents[?LastModified>= '2024-02-01'].Key" --output json | jq -r '.[]' | xargs -I {} aws s3 cp s3://TestBucket/{} /home/ec2-user/
```



