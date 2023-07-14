### userdata reset 방법

```
rm -rf /var/lib/cloud/instances
```

예를들어 userdata가 /~~/EC2.log에 쌓이면 지우고 이미지 떠야한다.

```
systemctl --type=service 로 cloud 관련 서비스 이슈없는지 확인
```
