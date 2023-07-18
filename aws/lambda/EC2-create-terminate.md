
Custodian으로 EC2 Event 검색 -> Webhook 으로 쏨

Custodian

```yaml
policies:
- name: ec2-create-terminate
  resource: ec2
  mode:
    type: cloudtrail
    role: arn:aws:iam: :123123123:role/temp-roll
    events:
      - source: ec2.amazonaws.com
        event: Runinstances
        ids: "responseElements InstancesSet, items[], instanceld"
      - source: ec2.amazonaws.com
        event: TerminateInstances
        ids: "responseElements InstancesSet, items[], instanceld"

   filters:
      - or:
        - tag:aws:autoscaling:groupName: absent
        - tag:spotinst:aws:ec2:group:createdBy: absent

    actions:
        - type: webhook
            url: https://hooks.slack.com/services/asdassdasdsd
            body: 'message"
```


webhook.py 수정

```python
# Copyright The Cloud Custodian Authors.
# SPDX-License-Identifier: Apache-2.0

try:
    import certifi
except ImportError:
    certifi = None

import jmespath
import json
import urllib3
from urllib import parse

from c7n import utils
from .core import EventAction


class Webhook(EventAction):
    """Calls a webhook with optional parameters and body
       populated from JMESPath queries.

        .. code-block:: yaml

          policies:
            - name: call-webhook
              resource: ec2
              description: |
                Call webhook with list of resource groups
              actions:
               - type: webhook
                 url: http://foo.com
                 query-params:
                    resource_name: resource.name
                    policy_name: policy.name
    """

    schema_alias = True
    schema = utils.type_schema(
        'webhook',
        required=['url'],
        **{
            'url': {'type': 'string'},
            'body': {'type': 'string'},
            'batch': {'type': 'boolean'},
            'batch-size': {'type': 'number'},
            'method': {'type': 'string', 'enum': ['PUT', 'POST', 'GET', 'PATCH', 'DELETE']},
            'query-params': {
                "type": "object",
                "additionalProperties": {
                    "type": "string",
                    "description": "query string values"
                }
            },
            'headers': {
                "type": "object",
                "additionalProperties": {
                    "type": "string",
                    "description": "header values"
                }
            }
        }
    )

    def __init__(self, data=None, manager=None, log_dir=None):
        super(Webhook, self).__init__(data, manager, log_dir)
        self.http = None
        self.url = self.data.get('url')
        self.body = self.data.get('body')
        self.batch = self.data.get('batch', False)
        self.batch_size = self.data.get('batch-size', 500)
        self.query_params = self.data.get('query-params', {})
        self.headers = self.data.get('headers', {})
        self.method = self.data.get('method', 'POST')
        self.lookup_data = None

    def process(self, resources, event=None):
        self.lookup_data = {
            'account_id': self.manager.config.account_id,
            'region': self.manager.config.region,
            'execution_id': self.manager.ctx.execution_id,
            'execution_start': self.manager.ctx.start_time,
            'policy': self.manager.data,
            'event': event
        }
        
        global account, principalId,eventName,serverName,privateIP,region,instanceId
        account = (self.manager.config.account_id)
        principalId = (event['detail']['userIdentity']['principalId'].split(":"))
        eventName = (event['detail']['eventName'])
        instanceId = (event['detail']['responseElements']['instancesSet']['items'][0])
        region = (event['detail']['awsRegion'])
        
        
        print("region#######")
        print(region)
        print("privateIP#######")
        print(account)
        print("principalId#######")
        print(principalId)
        print("eventName########")
        print(eventName)
        print("instanceId########")
        print(instanceId)
        print(instanceId['instanceId'])
        
        
        if eventName == 'RunInstances':
            instanceName = (event['detail']['requestParameters']['tagSpecificationSet']['items'])
            json_data = (event['detail']['requestParameters']['tagSpecificationSet']['items'][0])
            tags = (event['detail']['requestParameters']['tagSpecificationSet']['items'][0]['tags'])
            privateIP = (event['detail']['responseElements']['instancesSet']['items'][0]['privateIpAddress'])
            print("instanceName########")
            print(instanceName)
            print(privateIP)
            print("account#######")
            
    
            ##json_data_tags  배열 
            
            check = 0
            
            # tags는 Dictionary의 배열이며 하나의 Dictionary의 Value가 Name인 다음 Dictionary의 콘텐츠에 NameTag 값이 있어서
            # check 변수를 써서 확인하는 로직이다.
                    
            for temp in tags:
                if check == 1:
                    break;
                for key,value in temp.items():
                    if check == 1:
                        serverName = value
                        print("serverName is " + serverName)
                        break;
                    if value == 'Name':
                        check =1
                        continue;

            
        else:
            print("TerminateInstances Event")
            
        

        self.http = self._build_http_manager()

        if self.batch:
            for chunk in utils.chunks(resources, self.batch_size):
                resource_data = self.lookup_data
                resource_data['resources'] = chunk
                self._process_call(resource_data)
        else:
            for r in resources:
                resource_data = self.lookup_data
                resource_data['resource'] = r
                self._process_call(resource_data)

    def _process_call(self, resource):
        prepared_url = self._build_url(resource)
        prepared_body = self._build_body(resource)
        prepared_headers = self._build_headers(resource)

        // SPOT 예외
        if "spotinst" in str(principalId[-1]):
            return

        // ASG 예외
        if "AutoScaling" in str(principalId[-1]):
            return

        if eventName == 'TerminateInstances':
            prepared_body = '{"attachments":[{"color":"#ff0000","blocks":[{"type":"section","text":{"type":"plain_text","text":"TerminateInstances","emoji":true}},{"type": "section","fields":[{"type": "mrkdwn","text": "instanceId"},{"type": "mrkdwn","text": "' + instanceId['instanceId'] + '"}]},{"type": "section","fields":[{"type": "mrkdwn","text": "CreatedBy"},{"type": "mrkdwn","text": "' + principalId[-1]+ '"}]},{"type": "actions","elements":[{"type": "button","text": {"type": "plain_text","text": "' + region + '"}},{"type": "button","text": {"type": "plain_text","text": "' + account + '"}}]}]}]}'
        else:
            prepared_body = '{"attachments":[{"color":"#42bd32","blocks":[{"type":"section","text":{"type":"plain_text","text":"RunInstances","emoji":true}},{"type": "section","fields":[{"type": "mrkdwn","text": "NameTag"},{"type": "mrkdwn","text": "' + serverName+ '"}]},{"type": "section","fields":[{"type": "mrkdwn","text": "CreatedBy"},{"type": "mrkdwn","text": "' + principalId[-1]+ '"}]},{"type": "section","fields":[{"type": "mrkdwn","text": "privateIP"},{"type": "mrkdwn","text": "' + privateIP+ '"}]},{"type": "actions","elements":[{"type": "button","text": {"type": "plain_text","text": "' + region + '"}},{"type": "button","text": {"type": "plain_text","text": "' + account + '"}}]}]}]}'
        
        #prepared_body = '{"attachments":[{"color":"#bd326a","blocks":[{"type":"section","text":{"type":"plain_text","text":"EC2 Created","emoji":true}}]}]}'

        if prepared_body:
            prepared_headers['Content-Type'] = 'application/json'

        try:
            res = self.http.request(
                method=self.method,
                url=prepared_url,
                body=prepared_body,
                headers=prepared_headers)

            self.log.info("%s got response %s with URL %s" %
                          (self.method, res.status, prepared_url))
        except urllib3.exceptions.HTTPError as e:
            self.log.error("Error calling %s. Code: %s" % (prepared_url, e.reason))

    def _build_http_manager(self):
        pool_kwargs = {
            'cert_reqs': 'CERT_REQUIRED',
            'ca_certs': certifi and certifi.where() or None
        }

        proxy_url = utils.get_proxy_url(self.url)
        if proxy_url:
            return urllib3.ProxyManager(proxy_url, **pool_kwargs)
        else:
            return urllib3.PoolManager(**pool_kwargs)

    def _build_headers(self, resource):
        return {k: jmespath.search(v, resource) for k, v in self.headers.items()}

    def _build_url(self, resource):
        """
        Compose URL with query string parameters.

        Will not lose existing static parameters in the URL string
        but does not support 'duplicate' parameter entries
        """

        if not self.query_params:
            return self.url

        evaluated_params = {k: jmespath.search(v, resource) for k, v in self.query_params.items()}

        url_parts = list(parse.urlparse(self.url))
        query = dict(parse.parse_qsl(url_parts[4]))
        query.update(evaluated_params)
        url_parts[4] = parse.urlencode(query)

        return parse.urlunparse(url_parts)

    def _build_body(self, resource):
        """Create a JSON body and dump it to encoded bytes."""

        if not self.body:
            return None

        return utils.dumps(jmespath.search(self.body, resource)).encode('utf-8')


```
