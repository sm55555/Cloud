### Ec2 접속 방법

#### 1. SSH 접속 (SSH 포트 사용)

#### 2. EC2 인스턴스 연결 (SSH 포트 사용)

#### 3. Session Manager (SSH 포트 사용 X, only IAM 권한만 필요)

- Agent 설치 (일반적으로 되어 있다.)

https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-ssm-agent.html

```
yum install -y https://s3.ap-northeast-2.amazonaws.com/amazon-ssm-ap-northeast-2/latest/linux_amd64/amazon-ssm-agent.rpm

sudo systemctl enable amazon-ssm-agent
sudo systemctl start amazon-ssm-agent
sudo systemctl status amazon-ssm-agent
```


![image](https://user-images.githubusercontent.com/38831314/142751838-ac1120c2-5b85-4a4e-ac27-b916cf4efd21.png)

IAM SSM Role ec2에 연결

![image](https://user-images.githubusercontent.com/38831314/142751888-d2b31a7e-a714-4660-80ea-32868631afdc.png)

세션 시작

![image](https://user-images.githubusercontent.com/38831314/142751925-3122a12c-8ca2-426a-8574-5881cb52e57c.png)

Cloudwatch를 통해 로그 기능 가능

#### 4. EC2 직렬 콘솔 (시리얼 포트 사용)

- root 패스워드를 통한 접속, 부팅/네트워크 화면 보임
