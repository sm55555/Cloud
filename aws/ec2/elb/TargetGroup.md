## 서비스 포트 개념

#### if  NLB Listen 포트 80 -> TargetGroup 기본 Listen port 80인 경우 (healthcheck가 8000포트이면)

TargetGroup 서버들에서 inbound로 NLB IP 80과 8000 두개를 열어야한다. 그렇지 않으면 unhelathy 뜬다
