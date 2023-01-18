## window -> S3 file upload

### 1. AWS CLI 2 다운로드

https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/install-cliv2.html

### 2. S3 프로그래밍 되는 계정 생성

IAM S3 FullAccess 권한 할당 !

### 3. 해당 서버 내에서 AWS CLI 세팅

[기본설정] 

```
$ aws configure
AWS Access Key ID [None]: AAAAAAAAASDAEXAMPLE
AWS Secret Access Key [None]: wlsdjasdJxckasdasdkdsddPLEKEY
Default region name [None]: us-west-2
Default output format [None]: ENTER
```

[모든 구성 데이터를 나열]

```
$ aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************ABCD  shared-credentials-file    
secret_key     ****************ABCD  shared-credentials-file    
    region                us-west-2             env    AWS_DEFAULT_REGION
```

[모든 프로파일 이름을 나열]

```
$ aws configure list-profiles
default
test
```
https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-configure-files.html

### 4. S3 네트워크 설정

[설정 방법]

aws configure set default.s3.max_bandwidth 500MB/s

[확인 방법]

https://docs.aws.amazon.com/cli/latest/topic/s3-config.html

### 5. 보내는 명령어

리젼 인식이 안되면 --region ap-northeast-2 를 명령어 뒤에 넣어야한다.

ex) aws s3 sync G:\201307 s3://test/test2/201307
ex) aws s3 sync G:\201307\test.jpg s3://test/test2/201307/test.jpg

warning: Skipping file ~~~ File does not exist. 뜰 경우 sync (객체 동기화 폴더에 사용 가능) -> cp(객체 복사 주로 사용)로 변경

### tip

윈도우에서는 .bat 만들어서 진행했다.

배치파일 text에 명령어만 넣고 실행


