```cmd
SET temp=sg-1111(공통SG)
SET sg=%var%    %temp%

---여기까지는 변수 값 초기 설정

for /f "tokens=*" %a in ('aws ec2 describe-instances --instance-ids i-1234 --query "Reservations[].Instances[].SecurityGroups[].GroupId[]" --output text --region=ap-northeast-2') do set var=%a

echo %sg%

aws ec2 modify-instance-attribute --instance-id i-1234 --groups %sg% --region=ap-northeast-2
```

아니면 아래와 같이 변수를 나누어서 넣어도 된다.

```
aws ec2 modify-instance-attribute --instance-id i-1234 --groups %var% %temp% --region=ap-northeast-2
```
