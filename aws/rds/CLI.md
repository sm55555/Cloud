### RDS CLI

RDS Cluster 조회 방법

```linux
aws rds describe-db-clusters --region ap-northeast-2 --query 'DBClusters[*].Endpoint' --output table
```
