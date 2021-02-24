# BillingAlram

참고 URL

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html

사용 사례 블로그

https://ark1st.tistory.com/36

일반 적으로 비용은 미국 동부(버지니아 북부로)에 다 통합되기에 비용설정알람 region은 미국 동부로 설정한다.



## 설정 방법

### 1. 계정에서 빌링 알람을 활성화 시켜준다.

<img src="https://user-images.githubusercontent.com/38831314/108953890-47269f80-76af-11eb-8894-08919fc2f3da.png">

### 2. CloudWatch 알람생성 -> Select Metric -> All metrics -> Billing -> Total Estimated Charge

<img src="https://user-images.githubusercontent.com/38831314/108954636-7689dc00-76b0-11eb-849f-4a7f49b49848.png">

### 3. 알람 부분 디테일 설정

<img src="https://user-images.githubusercontent.com/38831314/108954780-a933d480-76b0-11eb-93e5-1b398185b492.png">

### 4. 주제 및 Email 수신자 설정

<img src="https://user-images.githubusercontent.com/38831314/108955086-ebf5ac80-76b0-11eb-90f1-04d2f4c64a59.png">

### 5. 완성 및 확인

<img src="https://user-images.githubusercontent.com/38831314/108955377-658d9a80-76b1-11eb-9dc6-a3341dc5872e.png">



