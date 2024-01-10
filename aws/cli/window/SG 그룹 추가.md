```cmd
SET temp=sg-1111(공통SG)
SET sg=%var%    %temp%

for /f "tokens=*" %a in ('aws ec2 describe-instances --instance-ids i-1234 --query "Reservations[].Instances[].SecurityGroups[].GroupId[]" --output text --region=ap-northeast-2') do set var=%a

echo %sg%

aws ec2 modify-instance-attribute --instance-id i-1234 --groups %sg% --region=ap-northeast-2
```
