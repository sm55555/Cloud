# IAM

**대원칙** 


공통적으로 MFA_USER가 들어간다.

ServerAdmin는 AdministratorAccess

NetworkAdmin는 NetworkAdministrator, ReadOnlyAccess

DBAdmin는 AmazonRDSFullAccess, ReadOnlyAccess

```
각 사용자 그룹에 최소한의 권한만 줘야한다.
```

### Root MFA 설정

루트 계정 접속 후, My Security Credentials에서 MFA 삭제 및 추가 가능하다.

![image](https://user-images.githubusercontent.com/38831314/131781152-dce8b370-9371-4d72-a3ab-0a0480cfabd9.png)

