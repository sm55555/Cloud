### NetworkLimit

Case

<img width="272" alt="image" src="https://github.com/sm55555/Cloud/assets/38831314/8f6f6d5a-59c4-49f7-aa51-71642373151a">

위 그림과 같이 ASG 환경에서 Redis를 호출하는 경우가 있다. 다만 어떤 로직에 의하여(호출을 많이하는) Redis의 Network Liumt이 발생하는 현상이 있다. 

Redis도 Node Type이 존재하여 위 링크에서 처럼 정해진 대역폭만을 할당받는다.

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/general-purpose-instances.html

만약 이 할당량을 넘으면 어떠한 수치가 발견되는데,
