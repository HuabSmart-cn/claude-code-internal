# history.ts

## 文件概述
**路径**: `src/history.ts`
**功能**: 管理命令行历史记录，包括粘贴内容引用和历史条目持久化
**重要程度**: ★★★★☆

---

## 核心概念
### PastedContent (粘贴内容)
Claude Code 解析历史中的粘贴内容引用，格式：
- 文本: `[Pasted text #1 +10 lines]`
- 图片: `[Image #2]`
数字在单个提示内唯一，不跨提示。

### StoredPastedContent (存储的粘贴内容)
```typescript
type StoredPastedContent = {
  id: number
  type: 'text' | 'image'
  content?: string        // 小型粘贴的内联内容
  contentHash?: string   // 大型粘贴的外部存储哈希引用
  mediaType?: string
  filename?: string
}
```

### 历史记录存储
- 历史存储在 `~/.claude/history.jsonl` (跨项目共享)
- 大型粘贴内容 (>1024字符) 存储在粘贴存储区，小型内联存储
- 异步刷新机制，带重试和锁文件

---

## 主要类型/接口
```typescript
type LogEntry = {
  display: string
  pastedContents: Record<number, StoredPastedContent>
  timestamp: number
  project: string
  sessionId?: string
}

type TimestampedHistoryEntry = {
  display: string
  timestamp: number
  resolve: () => Promise<HistoryEntry>
}
```

---

## 关键函数
```typescript
/**
 * 解析粘贴引用，返回引用的ID、匹配文本和位置
 */
function parseReferences(input: string): Array<{ id: number; match: string; index: number }>

/**
 * 展开 [Pasted text #N] 占位符为实际内容
 */
function expandPastedTextRefs(
  input: string,
  pastedContents: Record<number, PastedContent>
): string

/**
 * 获取当前项目历史（当前会话优先）
 */
async function* getHistory(): AsyncGenerator<HistoryEntry>

/**
 * 获取带时间戳的历史条目（用于 ctrl+r 选择器）
 */
async function* getTimestampedHistory(): AsyncGenerator<TimestampedHistoryEntry>

/**
 * 添加到历史记录
 */
function addToHistory(command: HistoryEntry | string): void

/**
 * 撤销最近一次添加到历史记录的操作
 */
function removeLastFromHistory(): void
```

---

## 与其他模块的关系
- 调用：
  - `pasteStore.ts` - 粘贴内容存储
  - `config.ts` - HistoryEntry 类型
  - `bootstrap/state.js` - getSessionId, getProjectRoot
- 被调用：
  - `main.tsx` - 添加到历史
  - REPL 组件 - 读取历史

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| History | 历史记录 |
| PastedContent | 粘贴内容 |
| StoredPastedContent | 存储的粘贴内容 |
| Reference | 引用 |
| LogEntry | 日志条目 |
| HistoryEntry | 历史条目 |
| Timestamp | 时间戳 |
| expand | 展开 |
| reverse | 反向 |
