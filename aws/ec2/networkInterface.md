### networkInterface 관련

네트워크 카드 추가 방식으로 한 EC2에 IP가 추가 가능하다.

EBS와 같이 생성 후 EC2에 추가하는 방식 !!

```cmd
ifconfig
```


![image](https://user-images.githubusercontent.com/38831314/129303246-da508d77-7be8-4b01-a500-887b9a5589fa.png)

참고 URL : https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/using-eni.html

### networkInterface 방화벽 관련

기존 네트워크 카드끼리 통신되어도 새로운 네트워크 카드 추가가 되면 그쪽에도 추가 요청해야한다.... 

