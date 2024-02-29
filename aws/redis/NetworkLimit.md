### NetworkLimit

Case

<img width="272" alt="image" src="https://github.com/sm55555/Cloud/assets/38831314/8f6f6d5a-59c4-49f7-aa51-71642373151a">

위 그림과 같이 ASG 환경에서 Redis를 호출하는 경우가 있다. 다만 어떤 로직에 의하여(호출을 많이하는) Redis의 Network Liumt이 발생하는 현상이 있다. 

Redis도 Node Type이 존재하여 위 링크에서 처럼 정해진 대역폭만을 할당받는다.

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/general-purpose-instances.html

만약 이 할당량을 넘으면 CloudWatch 어떠한 수치가 발견되는데,

```
NetworkBandwidthInAllowanceExceeded/NetworkBandwidthOutAllowanceExceeded : 처리량이 집계된 대역폭 제한을 초과하여 형성된 네트워크 패킷입니다.

NetworkConntrackAllowanceExceeded : 노드에 할당된 모든 보안 그룹에서 추적되는 최대 연결 수를 초과했기 때문에 형성되는 패킷입니다. 이 기간 동안 새 연결이 실패할 가능성이 높습니다.

NetworkPackets PerSecondAllowanceExceeded : 초당 최대 패킷 수를 초과했습니다. 매우 크기가 작은 요청의 비율이 높은 워크로드는 최대 대역폭 전에 이 제한에 도달할 수 있습니다.
```

특히 NetworkBandwidthOutAllowanceExceeded 이 부분이 Metric이 확인된다면 Network Limit 자체가 발생되는 것이다.

따라서 해결책은 EC2에서 부하량을 줄이거나, Redis의 스펙을 올려야한다.
