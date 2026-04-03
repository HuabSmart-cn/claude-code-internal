# state

## 功能
状态管理模块，使用 React Context 和 useReducer 管理全局应用状态。

## 文件说明

- `AppState.tsx` - 应用状态组件 (23KB)
- `AppStateStore.ts` - 状态存储 (21KB)
- `onChangeAppState.ts` - 状态变更处理
- `selectors.ts` - 状态选择器
- `store.ts` - Store 入口
- `teammateViewHelpers.ts` - 队友视图辅助

## 核心概念

### 状态存储
基于 React Context 的全局状态管理，使用 useReducer 管理复杂状态。

### 状态结构
- 应用级配置状态
- UI 状态
- 会话状态
- 队友视图状态

### 状态选择器
提供类型安全的状态选择函数，用于在组件中获取特定状态切片。

### 变更通知
状态变更时的回调机制，用于同步外部系统或执行副作用。
