### 볼륨 용량 증설

루트 볼륨 용량 증설
https://aws.amazon.com/ko/premiumsupport/knowledge-center/expand-root-ebs-linux/

-> 요약 : 증설 후 재부팅 or 볼륨떼고 다시 붙히기

루트 및 이외 용량 증설

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html

-> EBS 콘솔에서 변경 후 

```linux
[ec2-user ~]$ sudo xfs_growfs -d /data
[ec2-user ~]$ sudo resize2fs /dev/nvme1n1
```

### GP2 vs GP3

웬만하면 gp3 가 더낮다, 서버가 켜져있는 동안에도 변경 가능

![image](https://user-images.githubusercontent.com/38831314/129137908-f40cfbf4-d586-444e-921a-4afaa5ab1a54.png)


-> 요금 측정 사이트
https://aws.amazon.com/ko/ebs/pricing/

### EBS 옵션 변경 시 주의 사항

볼륨 확장 후 -> 타입을 변경하려고(gp2 -> gp3) 하면 최소 6시간 이상 대기해야한다...

### EC2 생성시 Storage

```
EBS 생성할때 Delete on Termination 옵션 체크하면 EC2 사라질 때 같이 사라짐(기본적으로 Root 볼륨은 전부 해당된다.)
그래서 EC2 지우면 Root 말고 나머지 볼륨은 available 상태로 남아 있다.
```

### EBS 교체 방법

결론은 인스턴스 끄지 않고도 교체가능하다. 루트볼륨도 해당 아래 내용 참고

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/ebs-restoring-volume.html


