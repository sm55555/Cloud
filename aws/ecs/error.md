# Error 모음집 


## OutOfMemory Error: Heap Space 발생 시


### Dockerfile 수정 (32GB)

```
CMD java -Xmx32G -classpath [serviceName]
```

### Task Definition 변경 (30GB, 4vCPU가 최대)

![image](https://user-images.githubusercontent.com/38831314/148891494-371b0d0d-1b91-4f60-b96b-f558ced4eafe.png)
