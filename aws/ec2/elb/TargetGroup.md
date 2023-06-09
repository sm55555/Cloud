## 서비스 포트 개념

#### if  NLB Listen 포트 80 -> TargetGroup 포트 80 (healthcheck가 8000포트이면)

TargetGroup 서버들에서 inbound로 NLB IP 80과 8000 두개를 열어야한다.
