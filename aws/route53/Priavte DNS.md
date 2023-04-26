# Route53에서 Private DNS 만들기


1. VPC에서 사설 도메인으로 동작할 수 있도록 enable한다.

#### Edit DNS hostnames, resoltion 체크

![image](https://user-images.githubusercontent.com/38831314/150745331-a2d07f81-4d4c-4548-88fb-6fcfdb4cf0a4.png)

![image](https://user-images.githubusercontent.com/38831314/150745837-4ad9fda9-d7c7-43a9-bb6f-444b33d755d0.png)


2. Route53에서 Private Hosted Zone 만들기

3. 필요레코드 만들기

4. 질의 (dig ~~~)

![image](https://user-images.githubusercontent.com/38831314/150745705-7ccf59de-f5cc-4cf3-9b1d-ec25f85070ec.png)

### Route53에서 만든 DNS 다른 대역 윈도우 서버에서 사용할떄

1. Inbound Endpoint 생성
2. Security Group에 윈도우 서버 대역 방화벽 Inbound Endpoint IP Address open TCP/UDP 53 오픈
3. 윈도우 서버에서 Telnet [Inbound Endpoint IP Address] 53 확인 후 Inbound Endpoint IP Address으로 DNS 설정
