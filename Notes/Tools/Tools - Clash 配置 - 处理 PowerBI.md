


```
rules:
  # 为 PowerBI 添加直连规则 - 放在最前面确保生效
  - DOMAIN-SUFFIX,powerbi.com,🎯 直连
  - DOMAIN-SUFFIX,analysis.windows.net,🎯 直连
  - DOMAIN-SUFFIX,pbidedicated.windows.net,🎯 直连
  - DOMAIN-SUFFIX,powerbi.cn,🎯 直连
  - DOMAIN-SUFFIX,msit.powerbi.com,🎯 直连
  - DOMAIN-SUFFIX,powerbi.microsoft.com,🎯 直连
  
  # 微软相关服务直连，确保 Power BI 认证和数据连接正常
  - DOMAIN-SUFFIX,microsoft.com,🎯 直连
  - DOMAIN-SUFFIX,microsoftonline.com,🎯 直连
  - DOMAIN-SUFFIX,msauth.net,🎯 直连
  - DOMAIN-SUFFIX,msftauth.net,🎯 直连
  - DOMAIN-SUFFIX,windows.net,🎯 直连
  - DOMAIN-SUFFIX,live.com,🎯 直连
  - DOMAIN-SUFFIX,azure.com,🎯 直连
  - DOMAIN-SUFFIX,azure.net,🎯 直连
  - DOMAIN-SUFFIX,azureedge.net,🎯 直连
  - DOMAIN-SUFFIX,login.partner.microsoftonline.cn,🎯 直连  # 中国区认证服务
  
  # 如果使用本地数据网关
  - DOMAIN-SUFFIX,servicebus.windows.net,🎯 直连
```

其实只有这条是我手动加入的

```
  - DOMAIN-SUFFIX,login.partner.microsoftonline.cn,🎯 直连  # 中国区认证服务
```