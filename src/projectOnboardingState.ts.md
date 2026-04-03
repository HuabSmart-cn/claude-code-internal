# projectOnboardingState.ts

## 文件概述
**路径**: `src/projectOnboardingState.ts`
**功能**: 管理项目入职状态，跟踪用户是否完成初始设置
**重要程度**: ★★★☆☆

---

## 核心概念
### 项目入职步骤
1. **workspace**: 询问 Claude 创建新应用或克隆仓库
2. **claudemd**: 运行 /init 创建 CLAUDE.md 文件

### 入职完成条件
- workspace 目录非空时才能完成 claudemd 步骤
- claudemd 步骤完成后整个入职才算完成

---

## 主要类型/接口
```typescript
type Step = {
  key: string
  text: string
  isComplete: boolean
  isCompletable: boolean
  isEnabled: boolean
}
```

---

## 关键函数
```typescript
/**
 * 获取所有入职步骤
 */
function getSteps(): Step[]

/**
 * 检查项目入职是否完成
 */
function isProjectOnboardingComplete(): boolean

/**
 * 标记项目入职完成
 */
function maybeMarkProjectOnboardingComplete(): void

/**
 * 检查是否应该显示项目入职提示
 * 条件：
 * - 未完成入职
 * - 显示次数 < 4
 * - 非演示模式
 */
function shouldShowProjectOnboarding(): boolean

/**
 * 增加入职提示显示计数
 */
function incrementProjectOnboardingSeenCount(): void
```

---

## 与其他模块的关系
- 调用：`utils/config.js` - 项目配置读写
- 被调用：`REPL.tsx` - 渲染前检查

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Project onboarding | 项目入职 |
| Onboarding step | 入职步骤 |
| CLAUDE.md | 项目配置文件 |
| Workspace | 工作区 |
| Complete | 完成 |
