### 서비스에 간헐적(20초 이상 딜레이 발생)으로 접속이 되는 현상

-> 라우팅 c 존으로 접속하는 라우팅 문제 였음

ELB 2개의 IP에 80 / 443 접속시도 및 netstat을 접속 현상파악

```cmd
C:\>netstat -na | findstr "1.1.1.1 2.2.2.2"
TCP    192.168.0.14:52592     1.1.1.1:443        SYN_SENT
TCP    192.168.0.14:64203     1.1.1.1:443        SYN_SENT

C:\>netstat -na | findstr "1.1.1.1 2.2.2.2"
TCP    192.168.0.14:53396     2.2.2.2:443        ESTABLISHED
TCP    192.168.0.14:60655     2.2.2.2:443        ESTABLISHED
```

### 갑자기 504 접속 에러

#### 참고

https://aws.amazon.com/ko/premiumsupport/knowledge-center/504-error-classic/

타켓 그룹 2개 인스턴스 unhealthy 상태

![image](https://user-images.githubusercontent.com/38831314/154779625-55140750-a05c-437d-b052-eff37da6f0dc.png)

한국 시간으로 검색 변경

![image](https://user-images.githubusercontent.com/38831314/154779744-8132e0a0-3c5e-4505-bcdc-fd113a39ccfe.png)

새벽 2시부터 unhealthy확인

![image](https://user-images.githubusercontent.com/38831314/154779670-1a6bf5d3-3eb2-48c9-9288-6d12e69d7c6e.png)

네트워크 팀 SG 변경으로 인한 기존 ALB랑 통신 끊기는 문제 확인 해결
