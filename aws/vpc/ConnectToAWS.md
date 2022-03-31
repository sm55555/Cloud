## Site to Site VPN

온 프레미스의 네트워크와 AWS 네트워크를 연결하기 위한 서비스
AWS Stie to Site VPN은 네트워크 VPC 또는 Transit Gateway 사이에 암호화 된 2개의 터널을 생성하여 사용
또한 인터넷 프로토콜은 보안(IPsec) VPN 연결을 지원합니다.
각 터널은 최대 1.25Gbps의 처리량을 지원합니다.

![image](https://user-images.githubusercontent.com/38831314/160997112-d141e5d4-24de-4292-8725-eea69e877ed3.png)

## AWS Direct Connect

온 프레미스의 네트워크와 AWS 네트워크를 연결하기 위한 서비스입니다.
이미지와 같이 Direct Connect Location을 거쳐 AWS 환경로 연결됩니다.
Direct Connect Location와 온 프레미스 사이에는 전용선으로 통신하게 됩니다.
구성 방법에 따라 지원되는 속도가 다르며 최소 50Mbps부터 최대 100Gbps까지 지원합니다.

![image](https://user-images.githubusercontent.com/38831314/160997186-ea4f5af3-dd06-45b4-a63a-a16ac904f7fa.png)


아래 링크는 100Gbps 지원 Location 위치 아쉽지만 한국은 해당 안된다.

https://aws.amazon.com/ko/about-aws/whats-new/2021/02/aws-direct-connect-announces-native-100-gbps-connections-select-locations/





