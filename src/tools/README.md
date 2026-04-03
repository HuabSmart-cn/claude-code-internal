# tools/ - 工具模块总览

## 目录结构

```
tools/
├── utils.ts                 # 工具辅助函数
├── tools.ts                 # 工具注册中心（主入口）
├── AgentTool/              # 代理工具
├── BashTool/               # Bash 命令工具
├── FileReadTool/           # 文件读取工具
├── FileEditTool/           # 文件编辑工具
├── FileWriteTool/          # 文件写入工具
├── GlobTool/               # 文件名匹配工具
├── GrepTool/               # 内容搜索工具
├── WebSearchTool/          # 网络搜索工具
├── WebFetchTool/           # 网页获取工具
├── NotebookEditTool/       # Jupyter Notebook 编辑工具
├── TodoWriteTool/          # Todo 列表管理
├── TaskCreateTool/         # 任务创建
├── TaskGetTool/            # 任务获取
├── TaskUpdateTool/         # 任务更新
├── TaskListTool/          # 任务列表
├── TaskStopTool/          # 任务停止
├── TaskOutputTool/        # 任务输出
├── EnterPlanModeTool/     # 进入计划模式
├── ExitPlanModeTool/      # 退出计划模式
├── EnterWorktreeTool/     # 进入 Git Worktree
├── ExitWorktreeTool/      # 退出 Git Worktree
├── SkillTool/             # Skill 执行工具
├── AskUserQuestionTool/   # 用户提问工具
├── BriefTool/             # 消息发送工具
├── LSPTool/               # 语言服务器协议工具
├── MCPTool/               # MCP 服务器工具包装
├── ListMcpResourcesTool/  # MCP 资源列表
├── ReadMcpResourceTool/   # MCP 资源读取
├── McpAuthTool/           # MCP OAuth 认证
├── TeamCreateTool/        # 团队创建
├── TeamDeleteTool/        # 团队删除
├── SendMessageTool/       # 发送消息
├── ScheduleCronTool/      # 定时任务
├── RemoteTriggerTool/     # 远程触发器
├── SleepTool/             # 延迟工具
├── SyntheticOutputTool/   # 结构化输出
├── PowerShellTool/        # PowerShell 工具
├── REPLTool/             # REPL 包装器
├── ToolSearchTool/        # 工具搜索
├── ConfigTool/            # 配置工具
├── shared/                # 共享模块
└── testing/               # 测试工具
```

## 工具分类

### 核心工具（无条件加载）

- AgentTool, BashTool, FileReadTool, FileEditTool, FileWriteTool
- GlobTool, GrepTool, WebSearchTool, WebFetchTool
- TodoWriteTool, TaskStopTool, BriefTool, AskUserQuestionTool
- SkillTool, EnterPlanModeTool, ExitPlanModeTool
- ListMcpResourcesTool, ReadMcpResourceTool, ToolSearchTool

### 文件操作工具

- FileReadTool, FileEditTool, FileWriteTool, GlobTool, GrepTool
- NotebookEditTool

### 网络工具

- WebSearchTool, WebFetchTool

### 任务管理工具

- TodoWriteTool, TaskCreateTool, TaskGetTool, TaskUpdateTool
- TaskListTool, TaskStopTool, TaskOutputTool

### 模式工具

- EnterPlanModeTool, ExitPlanModeTool

### Worktree 工具

- EnterWorktreeTool, ExitWorktreeTool

### 团队协作工具

- TeamCreateTool, TeamDeleteTool, SendMessageTool

### 定时任务工具

- ScheduleCronTool, RemoteTriggerTool

### 条件性工具

根据环境变量和功能标志可用：
- ConfigTool, REPLTool, LSPTool, PowerShellTool
- SleepTool, SyntheticOutputTool

## 核心接口

所有工具实现 `Tool` 接口（定义在 `src/Tool.ts`），主要方法：
- `call()` - 执行工具
- `description()` - 获取描述
- `prompt()` - 获取提示词

## 工具工厂

使用 `buildTool()` 工厂函数创建工具，自动填充默认值。
