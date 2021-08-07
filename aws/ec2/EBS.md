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

### gp2 VS gp3

웬만하면 gp3 가 더낮다, 서버가 켜져있는 동안에도 변경 가능

### EBS 옵션 변경 시 주의 사항

볼륨 확장 후 -> 타입을 변경하려고(gp2 -> gp3) 하면 최소 6시간 이상 대기해야한다...

### EC2 생성시 Storage**

```
EBS 생성할때 Delete on Termination 옵션 체크하면 EC2 사라질 때 같이 사라짐(EC2)
```
