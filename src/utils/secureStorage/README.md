# secureStorage/ - 安全存储

## 功能概述

`secureStorage/` 目录提供敏感数据的安全存储功能。

## 文件列表

```
secureStorage/
├── fallbackStorage.ts       # 回退存储
├── index.ts               # 入口
├── keychainPrefetch.ts    # 钥匙串预取
├── macOsKeychainHelpers.ts # macOS 钥匙串辅助
├── macOsKeychainStorage.ts # macOS 钥匙串存储
└── plainTextStorage.ts    # 明文存储
```

## 存储后端

### macOS 钥匙串
`macOsKeychainStorage.ts` - 使用 macOS Keychain 存储敏感数据。

### 跨平台回退
`fallbackStorage.ts` - 不支持 Keychain 时的回退方案。

### 明文存储
`plainTextStorage.ts` - 非敏感配置存储。

## 使用场景

- API 密钥存储
- OAuth 令牌存储
- 认证凭据
