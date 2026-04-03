# ExitPlanModeTool (ExitPlanModeV2Tool)

## 功能

退出计划模式。

## 核心文件

- `ExitPlanModeV2Tool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface ExitPlanModeInput {
  // 无参数
}
```

## 对应命令/用途

ExitPlanModeTool 用于完成计划阶段，返回正常执行模式。

**相关工具**：EnterPlanModeTool
