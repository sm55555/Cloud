## service_updates

Amazon ElasticCache 메뉴에 Service updates에서

```
Auto-update after due date가 YES이면 -> Apply-by date이후에 임의의 날짜로 진행된다.
Auto-update after due date가 NO이면 -> 나중에 진행되어 completed가 되어도 실제로 수행된 것은 아니다.
```

### AWS Recommned Apply By Date 이후 적용 시점

각 Redis Cluster -> Maintenance and backups -> Backups -> Maintenance Modify에서 변경할 수 있다. 이것은 기본적으로 생성 시 설정하는거


