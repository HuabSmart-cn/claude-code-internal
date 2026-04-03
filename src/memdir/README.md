# memdir

## 功能
内存目录（Memory Directory）系统为 Claude Code 提供持久化、文件-based 的记忆功能。系统支持四种记忆类型（user、feedback、project、reference），并区分私有记忆和团队共享记忆。

## 文件列表

- `memdir.ts` - 核心内存目录管理
  - 定义 `isAutoMemoryEnabled()` 和 `isExtractModeActive()` 等功能开关
  - 提供 `getAutoMemPath()` 获取自动记忆目录路径
  - 提供 `isAutoMemPath()` 检查路径是否在自动记忆目录内
  - `loadMemoryPrompt()` 构建系统提示词中的记忆部分
  - 支持 KAIROS 每日日志模式和 TEAMMEM 团队记忆模式

- `memoryTypes.ts` - 记忆类型定义
  - 定义四种记忆类型常量: `MEMORY_TYPES = ['user', 'feedback', 'project', 'reference']`
  - `MemoryType` 类型别名
  - `parseMemoryType()` 解析原始 frontmatter 值为 MemoryType
  - `TYPES_SECTION_COMBINED` / `TYPES_SECTION_INDIVIDUAL` - 记忆类型的说明文本模板
  - `WHAT_NOT_TO_SAVE_SECTION` - 不应保存的内容说明
  - `WHEN_TO_ACCESS_SECTION` - 何时访问记忆的指导
  - `TRUSTING_RECALL_SECTION` - 如何信任回忆内容的指导

- `paths.ts` - 记忆目录路径解析
  - `getMemoryBaseDir()` 获取记忆存储基础目录（`~/.claude`）
  - `getAutoMemPath()` 获取项目自动记忆目录
  - `getAutoMemEntrypoint()` 获取 MEMORY.md 入口文件路径
  - `getAutoMemDailyLogPath()` 获取每日日志文件路径（KAIROS 模式）
  - `isAutoMemPath()` 检查路径是否在自动记忆目录内
  - 支持 `CLAUDE_COWORK_MEMORY_PATH_OVERRIDE` 和 settings.json 配置覆盖

- `teamMemPaths.ts` - 团队记忆路径管理
  - `isTeamMemoryEnabled()` 检查团队记忆是否启用
  - `getTeamMemPath()` / `getTeamMemEntrypoint()` 获取团队记忆路径
  - `isTeamMemPath()` / `isTeamMemFile()` 检查路径是否属于团队记忆
  - `validateTeamMemWritePath()` / `validateTeamMemKey()` 验证写入路径安全性
  - `PathTraversalError` 用于防止路径遍历攻击

- `findRelevantMemories.ts` - 相关记忆查找
  - `findRelevantMemories()` 扫描记忆文件并使用 Sonnet 模型选择最相关的记忆
  - `scanMemoryFiles()` 扫描目录下所有 .md 记忆文件
  - 支持 `recentTools` 过滤和 `alreadySurfaced` 排除列表
  - 返回最多 5 个相关记忆的绝对路径和 mtime

- `memoryScan.ts` - 记忆文件扫描工具
  - `scanMemoryFiles()` 扫描记忆目录，返回 MemoryHeader 列表
  - `formatMemoryManifest()` 格式化记忆清单用于提示词
  - 支持 frontmatter 解析提取 description 和 type
  - 按修改时间排序，最多返回 200 个文件

- `teamMemPrompts.ts` - 团队记忆提示词构建
  - `buildCombinedMemoryPrompt()` 构建同时包含私有和团队记忆的提示词
  - 区分 private 和 team 两种作用域
  - 包含敏感数据警告（不保存 API keys 等）

- `memoryAge.ts` - 记忆文件年龄相关功能

## 核心概念

### 记忆类型 (Memory Types)
1. **user** - 用户角色、偏好、知识相关记忆（始终私有）
2. **feedback** - 用户给出的指导/反馈（默认私有，团队共识可设为团队）
3. **project** - 项目上下文、目标、bug、决策（强烈建议团队共享）
4. **reference** - 外部系统指针（通常团队共享）

### 目录结构
```
~/.claude/
└── projects/
    └── <sanitized-project-root>/
        └── memory/
            ├── MEMORY.md (索引入口)
            ├── user_role.md
            ├── feedback_testing.md
            └── team/ (团队共享记忆)
                ├── MEMORY.md
                └── ...

```

### 安全特性
- 路径验证防止符号链接逃逸
- Unicode 规范化攻击防护
- null byte 拒绝
- 相对路径强制解析为绝对路径
