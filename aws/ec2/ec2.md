# EC2

**인스턴스 실수로 종료 막기** 

```
disableApiTermination 속성을 true
```


**리눅스 shutdown -h or Window shutdown 막으려면** 

```
instanceInitiatedShutdownBehavior 인스턴스 속성을 stop이나 terminate 설정
```

**On_Demand** 

```
내가 사용한 시간만큼 돈내는거,,
```

**Reserved Instance** 

```
어느 특정 기간을 약정하고 쓰던 안쓰던 돈이나감,,, 대신 On_Demand 보다는 가격이 싸다
```

**Spot Instacne** 

```
남는거 떨이해서 씀 -> 엄청 싸지만 언제 자원 뺏길지 
```

**인스턴스 AMI 생성시**

```
해당 EC2에서 생성하면 해당 EC2가 잠깐의 다운된다.
```

**Auto scaling 생성시**

<div>
	<img width="800px" height="300px" src="https://user-images.githubusercontent.com/38831314/81523360-90a83700-9388-11ea-846a-17e59a629a8d.PNG">
</div>

```
Health Check type 부분  ELB는 EC2에 올라간 application의 헬스만 체크하는것이고 (ex: ec2위에 올라간 웹서버)

EC2를 체크하면 단순히 EC2가 살아있는건지 죽은건지 확인하는것이다.
```
