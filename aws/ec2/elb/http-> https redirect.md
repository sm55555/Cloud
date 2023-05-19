## http-> https redirect

### Not Use ALB

User -> NLB 80 -> TG 80 -> Ec2 (nginx 80 to 443 Redirect) -> NLB 443 -> TG 80 -> nginx 443

### Use ALB

