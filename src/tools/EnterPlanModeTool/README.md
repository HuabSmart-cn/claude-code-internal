# EnterPlanModeTool

## 功能

请求进入计划模式，用于复杂任务的探索和设计。

## 核心文件

- `EnterPlanModeTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface EnterPlanModeInput {}
// 无参数 - 进入计划模式不需要参数
```

## 特性

- **延迟加载** - shouldDefer: true
- **权限检查** - 检查是否允许进入计划模式

## 对应命令/用途

EnterPlanModeTool 用于切换到计划模式，先设计方法再执行。

**相关工具**：ExitPlanModeTool
