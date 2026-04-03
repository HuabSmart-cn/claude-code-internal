# main.tsx

## 文件概述
**路径**: `src/main.tsx`
**功能**: Claude Code 应用的主入口点，处理命令行参数解析和应用初始化
**重要程度**: ★★★★★

---

## 核心概念
### 应用生命周期
1. **预导入阶段** (Pre-import)
   - `profileCheckpoint` 标记入口
   - MDM 原始读取
   - 密钥链预取

2. **导入阶段** (Import)
   - 加载所有必要的模块
   - 条件导入（特性标志）

3. **初始化阶段** (Init)
   - 设置状态
   - 运行迁移
   - 解析命令行参数

4. **渲染阶段** (Render)
   - 创建 Ink 根
   - 渲染主 UI
   - 等待退出

### 命令行参数
使用 `@commander-js/extra-typings` 解析 CLI 参数。

---

## 主要流程
```typescript
// 1. 预检查
profileCheckpoint('main_tsx_entry')
startMdmRawRead()
startKeychainPrefetch()

// 2. 调试模式检查
if (isBeingDebugged()) {
  process.exit(1)
}

// 3. 迁移
runMigrations()

// 4. 设置加载
loadSettingsFromFlag()
loadSettingSourcesFromFlag()

// 5. 创建根并渲染
const root = await createRoot(options)
await renderAndRun(root, element)

// 6. 延迟预取
startDeferredPrefetches()
```

---

## 重要常量
```typescript
const CURRENT_MIGRATION_VERSION = 11
```

---

## 与其他模块的关系
- 调用：
  - `setup.ts` - 应用设置
  - `ink.ts` - 渲染入口
  - `interactiveHelpers.tsx` - UI 辅助函数
  - `commands.ts` - 命令管理
  - `tools.ts` - 工具管理
- 被调用：CLI 入口点

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Main entry point | 主入口点 |
| Commander | 命令行工具 |
| Pre-fetch | 预取 |
| Migration | 迁移 |
| Startup | 启动 |
| Initialization | 初始化 |
| Debug mode | 调试模式 |
