# Configuration / 配置参考

<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言                                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English (default)    |    🇨🇳 中文                                        ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇬🇧 English

### Scenario A: OpenClaw & cursor2api on Same Machine (Current)

> ⚠️ Note: Local Node.js version defaults to port **3010** (not Docker's 3000)

Add to `~/.zshrc` or `~/.bashrc`:

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_workos_cursor_session_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
```

Verify config:
```bash
# Restart OpenClaw
openclaw gateway restart

# Check logs
openclaw logs --tail 50
```

### Scenario B: cursor2api in Docker on Desktop, OpenClaw on Host

Docker Desktop's localhost points to the container itself. Use `host.docker.internal`:

```bash
export ANTHROPIC_BASE_URL="http://host.docker.internal:3010/v1"
export ANTHROPIC_API_KEY="your_workos_cursor_session_token"
```

### Scenario C: cursor2api on Remote Server

```bash
export ANTHROPIC_BASE_URL="http://your-server-ip:3010/v1"
export ANTHROPIC_API_KEY="your_workos_cursor_session_token"
```

### Claude Code Configuration

Create shell functions for provider switching:

```bash
# ~/.zshrc

cursor-proxy() {
  export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
  export ANTHROPIC_AUTH_TOKEN="your_token"
  export ANTHROPIC_API_KEY="your_token"
  export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
  echo "✅ Claude Code → cursor2api"
}

cursor-reset() {
  unset ANTHROPIC_BASE_URL ANTHROPIC_AUTH_TOKEN ANTHROPIC_API_KEY
  echo "✅ Claude Code → Official Anthropic API"
}

# Convenience aliases
alias cursor-up='docker start cursor-api && cursor-proxy'
alias cursor-down='docker stop cursor-api && cursor-reset'
```

```bash
source ~/.zshrc
cursor-proxy     # Enable proxy
cursor-reset     # Switch back to official
```

### CC Switch Configuration

Add in CC Switch UI:

| Config Key | Value |
|------------|-------|
| **Provider Name** | `cursor2api` |
| **API Type** | `Anthropic` |
| **Base URL** | `http://localhost:3010/v1` |
| **API Key** | `WorkosCursorSessionToken` |
| **Model** | `claude-sonnet-4-6` |

JSON config format:

```json
{
  "providers": {
    "cursor2api": {
      "type": "anthropic",
      "baseURL": "http://localhost:3010/v1",
      "apiKey": "your_token",
      "models": {
        "sonnet": "claude-sonnet-4-6",
        "opus": "claude-opus-4-20250514"
      }
    }
  },
  "activeProvider": "cursor2api"
}
```

### Environment File (~/.cursor2apirc)

Create `~/.cursor2apirc` for persistent config:

```bash
CURSOR_API_URL="http://localhost:3010/v1"
CURSOR_TOKEN="your_workos_cursor_session_token"
CURSOR_MODEL="claude-sonnet-4-6"
```

Load with:
```bash
source ~/.cursor2apirc
```

### Available Endpoints

> ⚠️ Local Node.js version uses port **3010**, Docker version uses port 3000

| Endpoint | Format | Compatible With |
|----------|--------|-----------------|
| `http://localhost:3010/v1/messages` | Anthropic Messages API | OpenClaw, Claude Code |
| `http://localhost:3010/v1/chat/completions` | OpenAI Chat Completions | CC Switch, Universal |

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Connection refused | Verify container: `docker ps \| grep cursor-api` |
| 401 Unauthorized | Token expired, refresh needed |
| 502 Bad Gateway | Container error, check: `docker logs cursor-api` |

---

## 🇨🇳 中文

### 场景 A：OpenClaw 与 cursor2api 在同一机器（当前）

> ⚠️ 注意：本地 Node.js 版本默认端口为 **3010**（非 Docker 的 3000）

添加到 `~/.zshrc` 或 `~/.bashrc`：

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="你的WorkosCursorSessionToken"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
```

验证配置：
```bash
# 重启 OpenClaw
openclaw gateway restart

# 检查日志
openclaw logs --tail 50
```

### 场景 B：cursor2api 在 Docker Desktop，OpenClaw 在宿主机

Docker Desktop 的 localhost 指向容器自己，需用 `host.docker.internal`：

```bash
export ANTHROPIC_BASE_URL="http://host.docker.internal:3010/v1"
export ANTHROPIC_API_KEY="你的WorkosCursorSessionToken"
```

### 场景 C：cursor2api 在远程服务器

```bash
export ANTHROPIC_BASE_URL="http://你的服务器IP:3010/v1"
export ANTHROPIC_API_KEY="你的WorkosCursorSessionToken"
```

### Claude Code 配置

创建 shell 函数切换 Provider：

```bash
# ~/.zshrc

cursor-proxy() {
  export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
  export ANTHROPIC_AUTH_TOKEN="你的Token"
  export ANTHROPIC_API_KEY="你的Token"
  export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
  echo "✅ Claude Code → cursor2api"
}

cursor-reset() {
  unset ANTHROPIC_BASE_URL ANTHROPIC_AUTH_TOKEN ANTHROPIC_API_KEY
  echo "✅ Claude Code → 官方 Anthropic API"
}

# 便捷别名
alias cursor-up='docker start cursor-api && cursor-proxy'
alias cursor-down='docker stop cursor-api && cursor-reset'
```

```bash
source ~/.zshrc
cursor-proxy     # 启用代理
cursor-reset     # 切回官方
```

### CC Switch 配置

在 CC Switch 界面中配置：

| 配置项 | 值 |
|--------|-----|
| **Provider Name** | `cursor2api` |
| **API Type** | `Anthropic` |
| **Base URL** | `http://localhost:3010/v1` |
| **API Key** | `WorkosCursorSessionToken` |
| **Model** | `claude-sonnet-4-6` |

JSON 配置格式：

```json
{
  "providers": {
    "cursor2api": {
      "type": "anthropic",
      "baseURL": "http://localhost:3010/v1",
      "apiKey": "你的Token",
      "models": {
        "sonnet": "claude-sonnet-4-6",
        "opus": "claude-opus-4-20250514"
      }
    }
  },
  "activeProvider": "cursor2api"
}
```

### 环境文件 (~/.cursor2apirc)

创建 `~/.cursor2apirc` 持久化配置：

```bash
CURSOR_API_URL="http://localhost:3010/v1"
CURSOR_TOKEN="你的WorkosCursorSessionToken"
CURSOR_MODEL="claude-sonnet-4-6"
```

加载：
```bash
source ~/.cursor2apirc
```

### 可用端点

> ⚠️ 本地 Node.js 版本端口为 **3010**，Docker 版本端口为 3000

| 端点 | 格式 | 兼容 |
|------|------|------|
| `http://localhost:3010/v1/messages` | Anthropic Messages API | OpenClaw, Claude Code |
| `http://localhost:3010/v1/chat/completions` | OpenAI Chat Completions | CC Switch, 通用 |

### 故障排查

| 问题 | 解决方案 |
|------|---------|
| 连接被拒绝 | 确认容器运行：`docker ps \| grep cursor-api` |
| 401 Unauthorized | Token 过期，需要刷新 |
| 502 Bad Gateway | 容器内部错误，检查：`docker logs cursor-api` |

<!-- tabs:end -->
