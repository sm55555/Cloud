### 하드웨어 장애

#### [정상인 경우]

![image](https://user-images.githubusercontent.com/38831314/135445218-404f6663-8b4e-4b86-8559-88dd0ec4a723.png)

#### [비정상인 경우]

![image](https://user-images.githubusercontent.com/38831314/135445750-ae67ba3d-5850-4287-aa7a-5b0bf604a375.png)

Cloudwatch metric에서 StatusCheckFailed "System" 의 지표가 상승했던 것으로 확인이 되면 즉 인스턴스는 underlying hardware 이슈로 인해 문제가 발생 존재

시스템 상태 확인 실패가 발생하는 경우는 아래와 같이 여러 가지 원인이 있을 수 있습니다.

- 네트워크 연결 끊김
- 시스템 전원 중단
- 물리적 호스트의 소프트웨어 문제
- 네트워크 연결성에 영향을 주는 물리적 호스트의 하드웨어 문제
