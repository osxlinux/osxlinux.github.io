---
layout: post
title:  zabbix_gethost_01
date:   2015-08-13 12:55:11
category: "monitor"
---
<p>操作系统环境：</p>
<pre>CentOS 5.5 x84_64位
Zabbix版本2.2.3
</pre>
<p>
环境部署，建议官方文档。
</p>
<p>zabbix api 使用</p>

<pre><code>
#!/usr/bin/env python
#auth:seraphico
#email:
import json
import urllib2
from urllib2 import URLError
import os
import sys

class login_get(object):

    def __init__(self):
        self.url = "http://x.x.x.x/api_jsonrpc.php"
        self.user = "xxxxxxx"
        self.password="xxxxxxxxx" 
        self.header = {"Content-Type": "application/json"}
        self.authID = self.user_login()

    def user_login(self):
        data = json.dumps({
            "jsonrpc": "2.0",
            "method": "user.login",
            "params": {
                "user": self.user,
                "password": self.password
                      },
            "id": 0
		})
        request = urllib2.Request(self.url,data)
        for key in self.header:
            request.add_header(key,self.header[key])
        try:
            result = urllib2.urlopen(request)
        except Exception as e:
            print "Auth Failed, Please Check Your Name And Password:",e.code
        else:
            response = json.loads(result.read())
            result.close()
            authID = response['result']
            return authID
    def get_data(self,data,hostip=""):
        request = urllib2.Request(self.url,data,self.header)
        try:
            result = urllib2.urlopen(request)
        except Exception as e:
            if hasattr(e, "reason"):
                print "Failed to reach a server."
                print "Reason:", e.reason
            elif hasattr(e, "reason"):
                print 'The server could not fulfill the request.'
                print 'Error code: ', e.code
            return 0
        else:
            response = json.loads(result.read())
            result.close()
            return response

login = login_get()
def main():
    userid = login.user_login()
    return  userid
def ReData(data):
    re_data = login.get_data(data)
    return re_data
if __name__ == "__main__":
    main()
</code></pre>
<h2> 如何调用</h2>
<code><pre>
#!/usr/bin/python
#coding:utf8

import os
import sys
import json
import urllib2
import zablogin

class get_infor(object):
    def __init__(self):
        self.auid = zablogin.main()
    def get_test(self):
        data = json.dumps({
            "jsonrpc": "2.0",
            "method": "host.get",
            "params": {
                 "output": "extend",
             },
            "auth": self.auid,
            "id": 1
            })
        self.re = zablogin.ReData(data)
        for x in self.re['result']:
            print x['host'],x['hostid'],x['status'],x['name']

def main():
    result = get_infor()
    return result.get_test()
if __name__ == "__main__":
    main()
</code></pre>
