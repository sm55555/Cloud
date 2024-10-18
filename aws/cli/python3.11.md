
### Install pip for Python 3.11
 
```
python3.11 -m ensurepip --upgrade
```

### Verify Installation of pip for Python 3.11

```
python3.11 -m pip --version
```

### Installation of pip for Python 3.11

```
pip3.11 install aws-encryption-sdk-cli -i https://[nexus-host]:443/repository/pypi-public/simple -v --trusted-host [nexus-host] 
```

```
pip3.11 install -r requirements.txt -i https://[nexus-host]:443/repository/pypi-public/simple -v --trusted-host [nexus-host] 
```

중요한건 가장 마지막에 실제 nexus에는없어도  /simple을 넣어야한다.
