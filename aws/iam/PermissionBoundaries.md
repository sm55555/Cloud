# 권한 범위 (PermissionBoundaries)
- IAM 자격증명(사용자, 역할)이 행사 가능한 최대 권한을 정의
- 실제로 자격을 부여하지 않고 행사 할 수 있는 권한의 범위만 정의
- 자격 증명이 행사 할 수 있는 권한은 권한 범위와 실제 부여된 권한 중 겹치는 부분

#### 권한 범위 설정

![image](https://user-images.githubusercontent.com/38831314/154845682-ac8b3b3e-9b08-427d-984a-c07110ee9694.png)

#### 권한 범위에는 EC2 전체 권한을 주었지만, stage라는 tag가 "Production" 이면 권한을 거부한다.

![image](https://user-images.githubusercontent.com/38831314/154845705-3b7b2385-537d-4361-9a9c-f4f545a968f2.png)

#### 그냥 권한은 admin을 준다.

![image](https://user-images.githubusercontent.com/38831314/154845802-f1e6ef3a-0079-47c9-a99a-dc05b82120de.png)


```
이렇게 되면 해당 유저는 s3, dynnamdb등 아무것도 쓸 수 없고 권한과 권한 범위가 겹쳐진 EC2만 사용가능하고 그중에서 stage라는 tag가 "Production"이 아니면 권한이 있다.
```

