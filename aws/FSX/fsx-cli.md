
- 22번 포트 확인 !

```
ssh fsxadmin@[Management endpoint - IP Address]
```

- 조회 cli

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
