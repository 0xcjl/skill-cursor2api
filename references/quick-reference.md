# Quick Reference / 快速参考

<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言                                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English (default)    |    🇨🇳 中文                                        ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇬🇧 English

### One-Command Install

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=YOUR_TOKEN \
  waitkafuka/cursor-api:latest
```

### Environment Setup

```bash
# Add to ~/.zshrc
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="YOUR_TOKEN"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc
openclaw gateway restart
```

### Token Refresh

```bash
# Check validity
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=YOUR_TOKEN" \
  https://api2.cursor.com/v1/me

# If expired: log out/in on cursor.com, get new token, restart container
docker stop cursor-api && docker rm cursor-api
docker run -d --name cursor-api -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=NEW_TOKEN \
  waitkafuka/cursor-api:latest
```

### Status Check

| Check | Command |
|-------|---------|
| Container | `docker ps \| grep cursor-api` |
| Logs | `docker logs cursor-api` |
| API test | `curl http://localhost:3010/health` |

### Endpoints

| Use Case | Endpoint |
|----------|----------|
| OpenClaw / Claude Code | `http://localhost:3010/v1/messages` |
| CC Switch / Universal | `http://localhost:3010/v1/chat/completions` |

### Uninstall

```bash
docker stop cursor-api && docker rm cursor-api
# Remove env vars from ~/.zshrc
```

---

## 🇨🇳 中文

### 一键安装

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=你的TOKEN \
  waitkafuka/cursor-api:latest
```

### 环境配置

```bash
# 添加到 ~/.zshrc
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="你的TOKEN"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc
openclaw gateway restart
```

### Token 续期

```bash
# 检查有效性
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=你的TOKEN" \
  https://api2.cursor.com/v1/me

# 如过期：退出/重新登录 cursor.com，获取新 token，重启容器
docker stop cursor-api && docker rm cursor-api
docker run -d --name cursor-api -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=新TOKEN \
  waitkafuka/cursor-api:latest
```

### 状态检查

| 检查项 | 命令 |
|--------|------|
| 容器 | `docker ps \| grep cursor-api` |
| 日志 | `docker logs cursor-api` |
| API 测试 | `curl http://localhost:3010/health` |

### 端点

| 使用场景 | 端点 |
|----------|------|
| OpenClaw / Claude Code | `http://localhost:3010/v1/messages` |
| CC Switch / 通用 | `http://localhost:3010/v1/chat/completions` |

### 卸载

```bash
docker stop cursor-api && docker rm cursor-api
# 从 ~/.zshrc 中移除环境变量
```

<!-- tabs:end -->
