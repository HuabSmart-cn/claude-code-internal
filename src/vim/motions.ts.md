# motions.ts - Vim 动作函数

## 文件概述
**路径**: `src/vim/motions.ts`
**功能**: 提供将 Vim 动作键解析为光标位置的纯函数

---

## 核心概念
- **纯函数设计**: `resolveMotion` 不修改任何状态，仅计算目标光标位置
- **计数前缀**: 支持重复计数（如 `3w` 前进 3 个单词）
- **包含性/排他性**: 某些动作是包含的（包含目标字符），某些是排他的
- **Vim 词（Vim Word）**: Vim 的词定义与普通单词不同

## 关键类型/接口
```typescript
// 基于 Cursor 工具类
type Cursor = {
  left(): Cursor
  right(): Cursor
  downLogicalLine(): Cursor
  upLogicalLine(): Cursor
  down(): Cursor
  up(): Cursor
  nextVimWord(): Cursor
  prevVimWord(): Cursor
  endOfVimWord(): Cursor
  nextWORD(): Cursor
  prevWORD(): Cursor
  endOfWORD(): Cursor
  startOfLogicalLine(): Cursor
  firstNonBlankInLogicalLine(): Cursor
  endOfLogicalLine(): Cursor
  startOfLastLine(): Cursor
}
```

## 核心函数

```typescript
/**
 * 将动作键解析为目标光标位置（纯函数）
 */
export function resolveMotion(
  key: string,
  cursor: Cursor,
  count: number,
): Cursor

/**
 * 检查动作是否为包含性（inclusive）
 * 包含性动作在配合 operator 使用时包含目标字符
 */
export function isInclusiveMotion(key: string): boolean

/**
 * 检查动作是否为行级（linewise）
 * 行级动作用于 operator 时影响整行
 */
export function isLinewiseMotion(key: string): boolean
```

## 动作映射

| 按键 | 动作类型 | 说明 |
|------|----------|------|
| `h` | 左移 | 左移一个字符 |
| `l` | 右移 | 右移一个字符 |
| `j` | 下移 | 移动到下一逻辑行 |
| `k` | 上移 | 移动到上一逻辑行 |
| `gj` | 下移 | 移动到下一显示行 |
| `gk` | 上移 | 移动到上一显示行 |
| `w` | 词首 | 前进到下一词首 |
| `b` | 词首 | 后退到当前词首 |
| `e` | 词尾 | 前进到当前词尾 |
| `W` | WORD 首 | 前进到下一 WORD 首 |
| `B` | WORD 首 | 后退到当前 WORD 首 |
| `E` | WORD 尾 | 前进到当前 WORD 尾 |
| `0` | 行首 | 逻辑行首 |
| `^` | 非空首 | 行第一个非空白字符 |
| `$` | 行尾 | 逻辑行尾 |
| `G` | 文件尾 | 移动到最后一行首 |

## 中英对照
| English | 中文 |
|---------|------|
| Motion | 动作 |
| Cursor | 光标 |
| Count | 计数 |
| Inclusive Motion | 包含性动作 |
| Exclusive Motion | 排他性动作 |
| Linewise | 行级 |
| Characterwise | 字符级 |
| Vim Word | Vim 词 |
| WORD | Vim WORD（大写词） |
| Logical Line | 逻辑行 |
| Display Line | 显示行 |
| Grapheme | 字素 |
| Resolve Motion | 解析动作 |
