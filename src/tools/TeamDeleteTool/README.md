# TeamDeleteTool

## 功能

删除 agent 团队（Swarm 模式）。

## 核心文件

- `TeamDeleteTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface TeamDeleteInput {}
// 无参数 - 删除当前团队
```

## 对应命令/用途

TeamDeleteTool 用于完成团队工作后清理资源。

**条件**：仅在 `isAgentSwarmsEnabled()` 时可用。

**相关工具**：TeamCreateTool
