# transitions.ts - Vim 状态转换表

## 文件概述
**路径**: `src/vim/transitions.ts`
**功能**: 实现 Vim 输入处理的状态机，根据当前状态和输入决定下一状态和执行动作

---

## 核心概念
- **状态机设计**: NORMAL 模式下使用状态机解析命令序列
- **状态类型**: idle、count、operator、find、g、replace、indent 等
- **转换函数**: 每个状态有专门的转换函数处理输入
- **执行 vs 状态转换**: 某些输入立即执行，某些触发状态转换

## 状态转换图

```
                              VimState
  ┌──────────────────────────────┬──────────────────────────────────────┐
  │  INSERT                      │  NORMAL                               │
  │  (tracks insertedText)       │  (CommandState machine)               │
  │                              │                                       │
  │                              │  idle ──┬─[d/c/y]──► operator         │
  │                              │         ├─[1-9]────► count            │
  │                              │         ├─[fFtT]───► find            │
  │                              │         ├─[g]──────► g                │
  │                              │         ├─[r]──────► replace          │
  │                              │         └─[><]─────► indent           │
  │                              │                                       │
  │                              │  operator ─┬─[motion]──► execute      │
  │                              │            ├─[0-9]────► operatorCount │
  │                              │            ├─[ia]─────► operatorTextObj
  │                              │            └─[fFtT]───► operatorFind  │
  └──────────────────────────────┴──────────────────────────────────────┘
```

## 关键类型/接口
```typescript
// 转换上下文
type TransitionContext = OperatorContext & {
  onUndo?: () => void
  onDotRepeat?: () => void
}

// 转换结果
type TransitionResult = {
  next?: CommandState      // 下一状态
  execute?: () => void     // 立即执行的函数
}
```

## 核心函数

```typescript
/**
 * 主转换函数，根据当前状态分发到对应的转换函数
 */
export function transition(
  state: CommandState,
  input: string,
  ctx: TransitionContext,
): TransitionResult
```

## 状态转换函数

```typescript
function fromIdle(input: string, ctx: TransitionContext): TransitionResult
function fromCount(state: { type: 'count'; digits: string }, input: string, ctx: TransitionContext): TransitionResult
function fromOperator(state: { type: 'operator'; op: Operator; count: number }, input: string, ctx: TransitionContext): TransitionResult
function fromOperatorCount(state: { type: 'operatorCount'; op: Operator; count: number; digits: string }, input: string, ctx: TransitionContext): TransitionResult
function fromOperatorFind(state: { type: 'operatorFind'; op: Operator; count: number; find: FindType }, input: string, ctx: TransitionContext): TransitionResult
function fromOperatorTextObj(state: { type: 'operatorTextObj'; op: Operator; count: number; scope: TextObjScope }, input: string, ctx: TransitionContext): TransitionResult
function fromFind(state: { type: 'find'; find: FindType; count: number }, input: string, ctx: TransitionContext): TransitionResult
function fromG(state: { type: 'g'; count: number }, input: string, ctx: TransitionContext): TransitionResult
function fromOperatorG(state: { type: 'operatorG'; op: Operator; count: number }, input: string, ctx: TransitionContext): TransitionResult
function fromReplace(state: { type: 'replace'; count: number }, input: string, ctx: TransitionContext): TransitionResult
function fromIndent(state: { type: 'indent'; dir: '>' | '<'; count: number }, input: string, ctx: TransitionContext): TransitionResult
```

## 命令解析示例

| 输入序列 | 状态转换 | 执行 |
|----------|----------|------|
| `d` | idle → operator | - |
| `w` (在 operator 状态) | operator → execute | executeOperatorMotion('delete', 'w') |
| `3` | idle → count | - |
| `d` (在 count 状态) | count → idle | executeOperatorMotion('delete', '', 3) |
| `fx` | idle → find | - |
| `;` (在 find 状态) | find → execute | 执行重复查找 |

## 中英对照
| English | 中文 |
|---------|------|
| State Machine | 状态机 |
| Transition | 转换 |
| Command State | 命令状态 |
| Idle | 空闲状态 |
| Count | 计数状态 |
| Operator | 操作符状态 |
| Find | 查找状态 |
| Replace | 替换状态 |
| Indent | 缩进状态 |
| Dispatch | 分发 |
| Execute | 执行 |
| Digit | 数字 |
| Motion | 动作 |
| Text Object | 文本对象 |
