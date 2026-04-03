# costHook.ts

## 文件概述
**路径**: `src/costHook.ts`
**功能**: React Hook，用于在应用退出时显示和保存成本摘要
**重要程度**: ★★★☆☆

---

## 核心概念
### useCostSummary
一个简单的 React Hook，在进程退出时：
1. 检查用户是否有控制台计费访问权限
2. 输出总成本到 stdout
3. 保存当前会话成本到配置

---

## 关键函数
```typescript
function useCostSummary(
  getFpsMetrics?: () => FpsMetrics | undefined,
): void
```

---

## 实现细节
```typescript
function useCostSummary() {
  useEffect(() => {
    const f = () => {
      if (hasConsoleBillingAccess()) {
        process.stdout.write('\n' + formatTotalCost() + '\n')
      }
      saveCurrentSessionCosts(getFpsMetrics?.())
    }
    process.on('exit', f)
    return () => { process.off('exit', f) }
  }, [])
}
```

---

## 与其他模块的关系
- 调用：
  - `cost-tracker.ts` - formatTotalCost, saveCurrentSessionCosts
  - `utils/billing.js` - hasConsoleBillingAccess
- 被调用：`main.tsx` - 用于 REPL 组件

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Cost hook | 成本钩子 |
| Console billing | 控制台计费 |
| Exit | 退出 |
| Summary | 摘要 |
