# github/ - GitHub 集成

## 功能概述

`github/` 目录处理 GitHub 认证和 API 交互。

## 文件列表

```
github/
├── ghAuthStatus.ts       # GitHub 认证状态
├── fallbackStorage.ts    # 回退存储
├── index.ts             # 入口
├── keychainPrefetch.ts  # 钥匙串预取
├── macOsKeychainHelpers.ts  # macOS 钥匙串辅助
├── macOsKeychainStorage.ts  # 钥匙串存储
└── plainTextStorage.ts  # 明文存储
```

## 认证

### GitHub OAuth
处理 GitHub OAuth 流程。

### 令牌管理
使用 Keychain 安全存储 GitHub 令牌。
