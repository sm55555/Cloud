# Endpoint를 통한 EC2, S3 연결

1. S3 Bucket 생성

2. VPC안에 Public / Private Subnet을 준비한다.

3. 각 Subnet에 인스턴스를 만들고 접속 테스트 Key Pair 생성

4. SSH 접근 위해서 22번 포트 활성화

5. Private Subnet에 있는 인스턴스에 접근을 위해서 Public에서 접속 세팅 (공부 !)

6. AWS CLI를 통해 AWS S3의 Bucket 목록을 불러온다. (Private Subnet에 있는 서버)
```
aws s3 ls
```
-----> 실패

7. AWS 콘솔에서 VPC > Endpoints 메뉴에서 “Create Endpoint”를 선택한다.
```
“Service Name” 항목에서 “s3”를 검색한 후 “com.amazonaws.ap-northeast-2.s3”를 선택한다.
위에서 생성한 EC2가 있는 VPC를 선택한다.
아래 “Configure route tables”가 표시되면 Private subnet에서 사용하고 있는 Route Table을 선택한다.
아래 “Policy”에서 특정 Bucket에 대한 정책을 제한할 수 있지만, 지금은 그냥 “Full Access”를 선택한다.
```

![image](https://user-images.githubusercontent.com/38831314/161671263-7466fd68-822a-4737-beff-c1e7a03286bf.png)

8. (6) 번 과정을 수행한다.
```
aws s3 ls
```
-----> 성공
