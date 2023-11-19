# Error 모음집 


## OutOfMemory Error: Heap Space 발생 시


### Dockerfile 수정 (32GB)

```
CMD java -Xmx32G -classpath [serviceName]
```

### Task Definition 변경 (30GB, 4vCPU가 최대)

![image](https://user-images.githubusercontent.com/38831314/148891494-371b0d0d-1b91-4f60-b96b-f558ced4eafe.png)


### The specified capacity provider already exists 문제 시 조회 및 삭제

```
aws ecs describe-capacity-providers --query capacityProviders\[\].name --region ap-northeast-2
aws ecs delete-capacity-provider --capacity-provider [ecs-capacity] --region ap-northeast-2

저번에 버그성으로 게속 생성이 안되서 describe에는 없었는데 없는 것도 지웠다 !

```
