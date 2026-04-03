# operators.ts - Vim 操作符函数

## 文件概述
**路径**: `src/vim/operators.ts`
**功能**: 实现 Vim 操作符（delete、change、yank 等）的纯函数，执行文本操作

---

## 核心概念
- **操作符（Operator）**: 执行文本修改的命令，如删除(d)、修改(c)、复制(y)
- **动作组合**: 操作符与动作组合形成完整操作（如 `dw` 删除词）
- **寄存器（Register）**: 存储被删除/复制内容的剪贴板
- **行级操作**: `dd`、`cc`、`yy` 等针对整行操作
- **撤销/重复**: 支持 `.` 重复和 `u` 撤销

## 关键类型/接口
```typescript
// 操作符上下文
type OperatorContext = {
  cursor: Cursor
  text: string
  setText: (text: string) => void
  setOffset: (offset: number) => void
  enterInsert: (offset: number) => void
  getRegister: () => string
  setRegister: (content: string, linewise: boolean) => void
  getLastFind: () => { type: FindType; char: string } | null
  setLastFind: (type: FindType, char: string) => void
  recordChange: (change: RecordedChange) => void
}
```

## 核心函数

### 操作符执行
```typescript
/**
 * 执行带动作的操作符
 */
export function executeOperatorMotion(
  op: Operator,
  motion: string,
  count: number,
  ctx: OperatorContext,
): void

/**
 * 执行带查找的操作符（f/F/t/T）
 */
export function executeOperatorFind(
  op: Operator,
  findType: FindType,
  char: string,
  count: number,
  ctx: OperatorContext,
): void

/**
 * 执行带文本对象的操作符（iw、aw 等）
 */
export function executeOperatorTextObj(
  op: Operator,
  scope: TextObjScope,
  objType: string,
  count: number,
  ctx: OperatorContext,
): void
```

### 特殊操作
```typescript
export function executeLineOp(op: Operator, count: number, ctx: OperatorContext): void  // dd, cc, yy
export function executeX(count: number, ctx: OperatorContext): void  // x 命令
export function executeReplace(char: string, count: number, ctx: OperatorContext): void  // r 命令
export function executeToggleCase(count: number, ctx: OperatorContext): void  // ~ 命令
export function executeJoin(count: number, ctx: OperatorContext): void  // J 命令
export function executePaste(after: boolean, count: number, ctx: OperatorContext): void  // p/P 命令
export function executeIndent(dir: '>' | '<', count: number, ctx: OperatorContext): void  // >> 命令
export function executeOpenLine(direction: 'above' | 'below', ctx: OperatorContext): void  // o/O 命令
```

### G 系列操作
```typescript
export function executeOperatorG(op: Operator, count: number, ctx: OperatorContext): void
export function executeOperatorGg(op: Operator, count: number, ctx: OperatorContext): void
```

## 操作细节

### 寄存器行为
- `yank` 将内容存入寄存器
- `delete` 将内容存入寄存器并从文本移除
- `paste` 从寄存器读取内容插入

### 特殊动作处理
- `cw` 特殊处理：改变到词尾而非词首
- `dw` 特殊处理：删除到下一词首

### 行级操作
- `dd/cc/yy` 影响 count 指定的行数
- 行级内容粘贴时自动添加换行符

## 中英对照
| English | 中文 |
|---------|------|
| Operator | 操作符 |
| Motion | 动作 |
| Text Object | 文本对象 |
| Delete | 删除 |
| Change | 修改 |
| Yank | 复制 |
| Paste | 粘贴 |
| Register | 寄存器 |
| Linewise | 行级 |
| Characterwise | 字符级 |
| Dot Repeat | 点重复 |
| Undo | 撤销 |
| Replace | 替换 |
| Toggle Case | 大小写切换 |
| Join | 合并行 |
| Indent | 缩进 |
| Open Line | 打开新行 |
