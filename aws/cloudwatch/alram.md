## 알람 거는 법 (SNS 와 연동)

공통 SNS 추가

Create Topic -> Details 선택 -> Subscriptions - Create subscription - Topic 연결 - Protocol = Email
이제는 이벤트 패턴을 만들어 특정 API가 발생될 때, SNS를 호출하도록 설정하겠습니다.

AWS Web Console - CloudWatch - Rules - Create rule - Event pattern - Event by service - EC2 - 
AWS API call via CloudTrail - Specific operation(s) -

### 1. Change SG

1. AuthorizeSecurityGroupIngress
2. AuthorizeSecurityGroupEgress
3. RevokeSecurityGroupIngress
4. RevokeSecurityGroupEgress
5. CreateSecurityGroup
6. DeleteSecurityGroup

![image](https://user-images.githubusercontent.com/38831314/159929736-1143b1e4-74b2-496f-aeb6-f25d27ca861a.png)

### 2. IAM User Create/Delete

AWS Web Console - CloudWatch - Rules - Create rule - Event pattern - Event by service - IAM -
AWS API call via CloudTrail - Specific operation(s) -

IAM에 대한 Resource는 us-east-1(버지니아 북부)에 위치하기 때문에 꼭!! Region을 us-east-1으로 변경합니다.

1. CreateUser
2. DeleteUser

![image](https://user-images.githubusercontent.com/38831314/159929814-db449e8a-d6f5-47fd-946a-2fb8e8894b14.png)

