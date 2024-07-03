## EC2 Cloudwatch Agent

## [Architecture]
![image](https://github.com/sm55555/Cloud/assets/38831314/cb4518ef-c946-4552-b7b9-5f924fe14861)



```
sudo yum install amazon-cloudwatch-agent -y
mkdir -p /opt/aws/amazon-cloudwatch-agent/etc
vi /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```
[content] messgae 로그 및 nginx access 로그

```
        "agent": {
                "metrics_collection_internal" : 10,
                "run_as_user": "root"
        },
        "logs": {
            "logs_collected": {
                    "files": {
                            "collect_list": [
                                    {
                                            "file_path": "/var/log/messages",
                                            "log_group_name": "message",
                                            "log_stream_name": "{instance_id}"
                                    },
                                    {
                                            "file_path": "/var/log/nginx/access.log",
                                            "log_group_name": "nginx-access",
                                            "log_stream_name": "{instance_id}"
                                    },
                            ]
                    }
            }
```


```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json -s
systemctl enable amazon-cloudwatch-agent.service
systemctl restart amazon-cloudwatch-agent.service
systemctl status amazon-cloudwatch-agent.service
```
