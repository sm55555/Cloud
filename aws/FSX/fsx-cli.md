
- 22번 포트 확인 !

```
ssh fsxadmin@[Management endpoint - IP Address]
```

- 조회 cli

```
FSXID1232131313123::> volume show -fiedls size
vserver  volume  size
-------  ------  ----
vol1     abc1    10GB
vol1     abc2    100GB
vol1     abc4    1TB
```

```
volume show -vserver [File system name]
```

```
volume show -vserver [File system name] -volume [Volume name]
```

- 특정 부분만 조회

```
volume show -vserver [File system name] -volume [Volume name] -fields size
```

- 변경 cli

```
volume modify -vserver [File system name] -volume [Volume name] -files 100000
```
