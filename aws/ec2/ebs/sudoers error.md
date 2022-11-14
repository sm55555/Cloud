## sudoers error

"/etc/sudoers: syntax error near line xx"
"sudo: parse error in /etc/sudoers near line xx"
"sudo: no valid sudoers sources found, quitting"
"sudo: unable to initialize policy plugin"

이런 문구가 뜨면 아래 url참고

https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-sudoers-syntax-errors-sudo/

### 간단요약

1. 해당 서버 종료 후 루트 볼륨 분리
2. 다른 서버에 mount -> sudo mount -o nouuid /dev/xvdf1 /mnt
3. cd /mnt/etc/sudoers.d 에서 편진
4. 다른 서버 종료 후 루트 볼륨 분리
5. 다시 원래 서버 붙이기 Device name 맞추기 /dev/xvda
