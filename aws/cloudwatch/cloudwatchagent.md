### EC2 Cloudwatch Agent

![image](https://github.com/sm55555/Cloud/assets/38831314/cb4518ef-c946-4552-b7b9-5f924fe14861)

```
sudo yum install amazon-cloudwatch-agent -y
mkdir -p /opt/aws/amazon-cloudwatch-agent/etc
vi /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```
[content]
```

```


```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json -s
systemctl enable amazon-cloudwatch-agent.service
systemctl restart amazon-cloudwatch-agent.service
systemctl status amazon-cloudwatch-agent.service
```
