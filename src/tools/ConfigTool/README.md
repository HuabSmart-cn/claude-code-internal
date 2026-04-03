# ConfigTool

## 功能

读取和写入 Claude Code 配置。

## 核心文件

- `ConfigTool.ts` - 主工具实现
- `supportedSettings.ts` - 支持的设置列表
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface ConfigInput {
  setting: string            // 设置键（如 "theme", "model"）
  value?: string | boolean | number  // 新值（省略则获取当前值）
}
```

## 对应命令/用途

ConfigTool 用于动态修改 Claude Code 设置。

**注意**：这是 Ant-only 工具（`USER_TYPE === 'ant'`）。
