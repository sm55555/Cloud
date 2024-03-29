테스트는 EFS Client Connections 수
테스트 방법은 해당 서버에서 mount, umount 반복으로 진행

### 1. SNS Topic 생성 후 인증

### 2. EFS Monitoring에서 Metrics CloudWatch 생성

### 3. Webhook URL 생성

https://velog.io/@king/slack-incoming-webhook

### 4. Lambda 함수 생성

Use a Blueprint -> Blueprint name (Send Cloudwatch alram notification via SNS) -> SNS Triiger 추가, Enviroment variables 추가

webhook 생성 및, SLACK_CHANNEL Enviroment 생성

```python
import boto3
import json
import logging
import os

from base64 import b64decode
from urllib.request import Request, urlopen
from urllib.error import URLError, HTTPError
# KST 변환 필요 모듈
from datetime import datetime, timedelta

HOOK_URL = os.environ['HookUrl']
SLACK_CHANNEL = "efs_client_connections"

logger = logging.getLogger()
logger.setLevel(logging.INFO)


def lambda_handler(event, context):
    logger.info("Event: " + str(event))
    message = json.loads(event['Records'][0]['Sns']['Message'])
    logger.info("Message: " + str(message))

    alarm_name = message['AlarmName']
    #old_state = message['OldStateValue']
    new_state = message['NewStateValue']
    reason = message['NewStateReason']
    # UTC 9시간 추가
    now = datetime.now() + timedelta(hours=9);
    TARGET="0";
    status ="🔥";
    
    if new_state == 'ALARM':
        status ="🔥"
    else:
        status ="✅"

    # EFS ID
    if "fs-111111111111" in str(event):
        TARGET ="AWS-EFS-TEST"
    else:
        TARGET ="???"
    
    slack_message = {
        'channel': SLACK_CHANNEL,
        'text': "%s [%s] Client connections is now %s %s" % (status, TARGET, new_state, now.strftime('%Y-%m-%d %H:%M:%S'))
    }
    
    req = Request(HOOK_URL, json.dumps(slack_message).encode('utf-8'))
    try:
        response = urlopen(req)
        response.read()
        logger.info("Message posted to %s", slack_message['channel'])
    except HTTPError as e:
        logger.error("Request failed: %d %s", e.code, e.reason)
    except URLError as e:
        logger.error("Server connection failed: %s", e.reason)

```
