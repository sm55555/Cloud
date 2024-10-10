### [secretsmanager]
```
aws secretsmanager get-secret-value --secret-id test
```

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
