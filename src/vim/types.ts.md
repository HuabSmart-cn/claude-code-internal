# types.ts - Vim 模式状态机类型

## 文件概述
**路径**: `src/vim/types.ts`
**功能**: 定义 Vim 模式状态机的完整类型系统，是理解整个 Vim 实现的核心文档

---

## 核心概念
- **VimState**: 两种模式 - INSERT（跟踪输入文本）和 NORMAL（命令状态机）
- **CommandState**: NORMAL 模式下的命令解析状态
- **持久状态**: 跨命令记忆的 vim 内存（lastChange、lastFind、register）
- **操作符类型**: delete、change、yank
- **查找类型**: f、F、t、T

## 关键类型/接口

### 操作符和查找类型
```typescript
type Operator = 'delete' | 'change' | 'yank'
type FindType = 'f' | 'F' | 't' | 'T'
type TextObjScope = 'inner' | 'around'
```

### Vim 状态
```typescript
type VimState =
  | { mode: 'INSERT'; insertedText: string }
  | { mode: 'NORMAL'; command: CommandState }
```

### 命令状态机
```typescript
type CommandState =
  | { type: 'idle' }
  | { type: 'count'; digits: string }
  | { type: 'operator'; op: Operator; count: number }
  | { type: 'operatorCount'; op: Operator; count: number; digits: string }
  | { type: 'operatorFind'; op: Operator; count: number; find: FindType }
  | { type: 'operatorTextObj'; op: Operator; count: number; scope: TextObjScope }
  | { type: 'find'; find: FindType; count: number }
  | { type: 'g'; count: number }
  | { type: 'operatorG'; op: Operator; count: number }
  | { type: 'replace'; count: number }
  | { type: 'indent'; dir: '>' | '<'; count: number }
```

### 持久状态
```typescript
type PersistentState = {
  lastChange: RecordedChange | null
  lastFind: { type: FindType; char: string } | null
  register: string
  registerIsLinewise: boolean
}
```

### 记录变更（用于 . 重复）
```typescript
type RecordedChange =
  | { type: 'insert'; text: string }
  | { type: 'operator'; op: Operator; motion: string; count: number }
  | { type: 'operatorTextObj'; op: Operator; objType: string; scope: TextObjScope; count: number }
  | { type: 'operatorFind'; op: Operator; find: FindType; char: string; count: number }
  | { type: 'replace'; char: string; count: number }
  | { type: 'x'; count: number }
  | { type: 'toggleCase'; count: number }
  | { type: 'indent'; dir: '>' | '<'; count: number }
  | { type: 'openLine'; direction: 'above' | 'below' }
  | { type: 'join'; count: number }
```

## 关键常量

```typescript
// 操作符映射
const OPERATORS = {
  d: 'delete',
  c: 'change',
  y: 'yank',
}

// 简单动作集合
const SIMPLE_MOTIONS = new Set([
  'h', 'l', 'j', 'k',  // 基本移动
  'w', 'b', 'e', 'W', 'B', 'E',  // 词移动
  '0', '^', '$',  // 行位置
])

// 查找按键
const FIND_KEYS = new Set(['f', 'F', 't', 'T'])

// 文本对象范围
const TEXT_OBJ_SCOPES = {
  i: 'inner',
  a: 'around',
}

// 文本对象类型
const TEXT_OBJ_TYPES = new Set([
  'w', 'W', '"', "'", '`',
  '(', ')', 'b', '[', ']', '{', '}', 'B', '<', '>',
])

const MAX_VIM_COUNT = 10000
```

## 中英对照
| English | 中文 |
|---------|------|
| Vim State | Vim 状态 |
| Insert Mode | 插入模式 |
| Normal Mode | 正常模式 |
| Command State | 命令状态 |
| Operator | 操作符 |
| Motion | 动作 |
| Text Object | 文本对象 |
| Find | 查找 |
| Replace | 替换 |
| Indent | 缩进 |
| Count | 计数 |
| Register | 寄存器 |
| Dot Repeat | 点重复 |
| Persistent State | 持久状态 |
| Recorded Change | 记录的变更 |
| Last Change | 上次变更 |
| Last Find | 上次查找 |
| Linewise | 行级 |
| Inner | 内部 |
| Around | 周围 |
