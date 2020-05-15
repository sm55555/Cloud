# IAM

**대원칙** 


공통적으로 MFA_USER가 들어간다.

ServerAdmin는 AdministratorAccess

NetworkAdmin는 NetworkAdministrator, ReadOnlyAccess

DBAdmin는 AmazonRDSFullAccess, ReadOnlyAccess

```
각 사용자 그룹에 최소한의 권한만 줘야한다.
```
