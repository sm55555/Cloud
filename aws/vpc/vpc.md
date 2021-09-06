# VPC

**VPC Peering : VPC간에 연결**

```
Transitive Peering 불가능 : 한다리 건너 연결 되어 있다고 해서 Peering 된 것이 아님 

ex) A<->B, B<->C 되있다고 A<->C가 되는 것은 아님
```


**NACL / Security Group**

```
-> NACL => Stateless, Sg => Stateful
-> 기본적으로 VPC 생성시 만들어줌
```

**Network ACLs**

<div>
	<img width="100%" height="150px" src="https://user-images.githubusercontent.com/38831314/81630004-741b0600-943f-11ea-8f19-21fe526785ab.PNG">
</div>

```
Deny는 NACL에서만 가능 
```
