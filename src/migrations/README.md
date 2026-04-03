# migrations

## 功能
数据迁移脚本，用于在版本升级时迁移用户配置和数据。

## 文件说明

- `migrateAutoUpdatesToSettings.ts` - 自动更新迁移到设置
- `migrateBypassPermissionsAcceptedToSettings.ts` - 绕过权限接受迁移
- `migrateEnableAllProjectMcpServersToSettings.ts` - MCP 服务器启用迁移
- `migrateFennecToOpus.ts` - Fennec 到 Opus 迁移
- `migrateLegacyOpusToCurrent.ts` - 旧版 Opus 迁移
- `migrateOpusToOpus1m.ts` - Opus 到 Opus 1m 迁移
- `migrateReplBridgeEnabledToRemoteControlAtStartup.ts` - REPL 桥接迁移
- `migrateSonnet1mToSonnet45.ts` - Sonnet 1m 到 4.5 迁移
- `migrateSonnet45ToSonnet46.ts` - Sonnet 4.5 到 4.6 迁移
- `resetAutoModeOptInForDefaultOffer.ts` - 自动模式重置
- `resetProToOpusDefault.ts` - Pro 到 Opus 默认重置

## 核心概念

### 版本迁移
当用户从旧版本升级到新版本时，执行相应迁移脚本：

1. **模型迁移** - 更新模型名称和配置
   - `migrateFennecToOpus`
   - `migrateOpusToOpus1m`
   - `migrateSonnet1mToSonnet45`
   - `migrateSonnet45ToSonnet46`

2. **功能迁移** - 更新功能开关和设置
   - `migrateAutoUpdatesToSettings`
   - `migrateEnableAllProjectMcpServersToSettings`

3. **权限迁移** - 更新权限相关配置
   - `migrateBypassPermissionsAcceptedToSettings`

4. **配置重置** - 重置特定设置为默认值
   - `resetAutoModeOptInForDefaultOffer`
   - `resetProToOpusDefault`

### 迁移模式
- 向前兼容：确保旧版本数据能正确迁移到新版本
- 幂等性：重复执行迁移不会造成问题
