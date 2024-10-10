3### [secretsmanager]
```
aws secretsmanager get-secret-value --secret-id test
```

명령어 결과 나온 Secret Binary 값을

```
echo AgV4r0adasddkldasdl;asdadasdkaskldaskkl;asdasd~~~ | base64 --decode
```

```
x҅��iT�{����@i��v���
                   ��矓naws-crypto-public-keyDA!~~!@~!@~~!@~!~!@~!@~~~~~~~~~~~~ow==purposetestaws-kmsParn:aws:kms:ap-northeast-2:123412341234:key123871232189831892asd�xn��F��M��w�K6
0o0m0h�F`�He.0���b���瀛<~0| *�H�
```

나오면 성공 ! kms arn 으로 해독 가능


### [aws-encryption-cli --encrypt]
```
aws-encryption-cli --encrypt \
                     --input hello.txt \
                     --wrapping-keys key=arn \
                     --metadata-output /home/ec2-user/encrypt.out \
                     --encryption-context purpose=test \
                     --commitment-policy require-encrypt-require-decrypt \
                     --output .
```
