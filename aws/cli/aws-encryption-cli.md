### [secretsmanager]
```
aws secretsmanager get-secret-value --secret-id test
```

명령어 결과 나온 Secret Binary 값을

```
echo AgV4r0adasddkldasdl;asdadasdkaskldaskkl;asdasd~~~ | base64 --decode > test.encrypted
```

```
x҅��iT�{����@i��v���
                   ��矓naws-crypto-public-keyDA!~~!@~!@~~!@~!~!@~!@~~~~~~~~~~~~ow==purposetestaws-kmsParn:aws:kms:ap-northeast-2:123412341234:key123871232189831892asd�xn��F��M��w�K6
0o0m0h�F`�He.0���b���瀛<~0| *�H�
```

나오면 성공 ! kms arn 으로 해독 가능

### [aws-encryption-cli --decrypt] 복호화 방법 decrypt 권한 필요

```
aws-encryption-cli --decrypt \
                     --input test.encrypted \
                     --wrapping-keys key=arn:aws:kms:ap-northeast-2:123412341234:key/712322132132132133 \
                     --commitment-policy require-encrypt-require-decrypt \
                     --encryption-context purpose=test \
                     --metadata-output /home/ec2-user/test-decrypt.out \
                     --max-encrypted-data-keys 1 \
                     --buffer \
                     --output .
```


### [aws-encryption-cli --encrypt] 암호화 방법 generatekey 권한 필요
```
aws-encryption-cli --encrypt \
                     --input hello.txt \
                     --wrapping-keys key=arn:aws:kms:ap-northeast-2:123412341234:key/712322132132132133 \
                     --metadata-output /home/ec2-user/encrypt.out \
                     --encryption-context purpose=test \
                     --commitment-policy require-encrypt-require-decrypt \
                     --output .
```

```
aws-encryption-cli --decrypt \
                     --input hello.txt.encrypted \
                     --wrapping-keys key=arn:aws:kms:ap-northeast-2:123412341234:key/712322132132132133 \
                     --commitment-policy require-encrypt-require-decrypt \
                     --encryption-context purpose=test \
                     --metadata-output /home/ec2-user/decrypt.out \
                     --max-encrypted-data-keys 1 \
                     --buffer \
                     --output .
```






