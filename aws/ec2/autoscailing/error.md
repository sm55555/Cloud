### ELB, AutoScailing

ELB에서 80 Listen하는데 ALB 세팅에 ELB만 체크 되있는 경우

예를들어 서버는 정상인데 웹서비스가 안올라와있으면 ELB는 502 에러는 내뱉으며 AutoScailing 동작 안 할 수 있다.

아래와 같이 ELB도 상태 점검을 체크 해줘야한다.

![image](https://user-images.githubusercontent.com/38831314/143664080-7fe11ac9-575f-4b0d-a831-863f9f0d352d.png)
