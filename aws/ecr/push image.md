### push image


```
aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --psasword-stdin 123412341234.dkr.ecr.ap-northeast-2.aamzonaws.com

docker tag 123123123 123412341234.dkr.ecr.ap-northeast-2.aamzonaws.com/nginx:latest
docker push 123412341234.dkr.ecr.ap-northeast-2.aamzonaws.com/nginx:latest
```
