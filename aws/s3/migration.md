### window -> S3

1. S3 프로그래밍 되는 계정 생성

2. configure 세팅
aws configure set default.s3.max_bandwidth 500MB/s

3. 보내는 명령어

ex)

aws s3 sync G:\201307 s3://test/test2/201307

