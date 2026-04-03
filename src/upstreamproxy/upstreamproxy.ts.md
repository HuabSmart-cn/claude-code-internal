# upstreamproxy.ts - CCR 上游代理容器端配置

## 文件概述
**路径**: `src/upstreamproxy/upstreamproxy.ts`
**功能**: CCR 容器内上游代理的初始化和配置，包括 token 读取、CA 证书下载、环境变量设置

---

## 核心概念
- **CCR（Claude Code Remote）**: 远程会话容器环境
- **MITM 代理**: CCR 使用 MITM（中间人）代理注入组织配置的凭据
- **PR_SET_DUMPABLE**: Linux 系统调用，阻止同 UID ptrace 保护 token 安全
- **环境变量继承**: 子进程继承 HTTPS_PROXY 和 SSL_CERT_FILE 配置
- **失败开放**: 任何错误都记录警告并禁用代理，不影响正常会话

## 关键常量

```typescript
export const SESSION_TOKEN_PATH = '/run/ccr/session_token'
const SYSTEM_CA_BUNDLE = '/etc/ssl/certs/ca-certificates.crt'

// 不走代理的 hosts 列表
const NO_PROXY_LIST = [
  'localhost', '127.0.0.1', '::1',
  '169.254.0.0/16', '10.0.0.0/8', '172.16.0.0/12', '192.168.0.0/16',
  'anthropic.com', '.anthropic.com', '*.anthropic.com',
  'github.com', 'api.github.com', '*.github.com', '*.githubusercontent.com',
  'registry.npmjs.org', 'pypi.org', 'files.pythonhosted.org',
  'index.crates.io', 'proxy.golang.org',
]
```

## 核心函数

```typescript
/**
 * 初始化上游代理
 * 在 init.ts 中调用，特性关闭或 token 文件不存在时返回 {enabled: false}
 */
export async function initUpstreamProxy(opts?: {
  tokenPath?: string
  systemCaPath?: string
  caBundlePath?: string
  ccrBaseUrl?: string
}): Promise<UpstreamProxyState>

/**
 * 获取子进程环境变量
 * 包含 HTTPS_PROXY、NO_PROXY、SSL_CERT_FILE 等
 */
export function getUpstreamProxyEnv(): Record<string, string>

/**
 * 测试用：重置模块状态
 */
export function resetUpstreamProxyForTests(): void
```

## 初始化流程

1. 检查 `CLAUDE_CODE_REMOTE` 和 `CCR_UPSTREAM_PROXY_ENABLED` 环境变量
2. 读取 session token 文件
3. 调用 `prctl(PR_SET_DUMPABLE, 0)` 阻止 ptrace
4. 下载 CCR CA 证书并与系统 CA 捆绑
5. 启动 WebSocket CONNECT 中继
6. 删除 token 文件（token 仅保留在内存）
7. 设置子进程环境变量

## 安全措施
- **ptrace 保护**: `prctl(PR_SET_DUMPABLE, 0)` 防止通过 `gdb -p $PPID` 窃取 token
- **文件删除**: token 文件在使用后立即 unlink
- **失败隔离**: 任何步骤失败不影响正常功能

## 中英对照
| English | 中文 |
|---------|------|
| Upstream Proxy | 上游代理 |
| CCR Container | CCR 容器 |
| Session Token | 会话令牌 |
| CA Certificate | CA 证书 |
| MITM Proxy | 中间人代理 |
| PR_SET_DUMPABLE | Linux 进程属性设置 |
| ptrace | 进程追踪 |
| Environment Variable | 环境变量 |
| SSL_CERT_FILE | SSL 证书文件 |
| HTTPS_PROXY | HTTPS 代理 |
| NO_PROXY | 不走代理列表 |
| Fail Open | 失败开放 |
| Cleanup Registry | 清理注册表 |
