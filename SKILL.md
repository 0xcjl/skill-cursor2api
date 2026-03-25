---
name: cursor2api
description: cursor2api proxy service management tool that converts Cursor IDE's free AI conversations into Anthropic Messages API / OpenAI Chat Completions API format. Supports Docker deployment, environment configuration, token refresh, and complete uninstallation. Use when user asks to: (1) Install or deploy cursor2api, (2) Configure cursor2api for OpenClaw/Claude Code/CC Switch, (3) Refresh or retrieve Cursor Session Token, (4) Uninstall cursor2api.
---

<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言                                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English (default)    |    🇨🇳 中文                                        ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

# cursor2api

<!-- tabs:start -->

## 🇬🇧 English

### Overview

`cursor2api` bridges Cursor IDE's AI models with OpenClaw/Claude Code by converting Cursor's internal API into standard Anthropic/OpenAI formats. This allows you to use Cursor's Claude subscription through any API-compatible client.

**Architecture:**
```
OpenClaw / Claude Code
         ↓ (ANTHROPIC_BASE_URL)
cursor2api Docker/Node (:3010)
         ↓ (Session Token)
Cursor Official API
```

### Prerequisites

- Docker (for containerized deployment) or Node.js 18+ (for local)
- A Cursor account with active AI subscription
- `WorkosCursorSessionToken` from Cursor

### Quick Start

```bash
# 1. Get your WorkosCursorSessionToken (see references/token.md)

# 2. Start the service
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest

# 3. Configure OpenClaw
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"

# 4. Restart OpenClaw
openclaw gateway restart
```

### Core Operations

| Operation | Command |
|-----------|---------|
| **Install** | `docker run -d --name cursor-api -p 3010:3000 -e WORKOS_CURSOR_SESSION_TOKEN=token waitkafuka/cursor-api:latest` |
| **Status** | `docker ps \| grep cursor-api` |
| **Refresh Token** | See `references/token.md` |
| **Uninstall** | `docker stop cursor-api && docker rm cursor-api` |

### API Endpoints

| Endpoint | Format | Compatible With |
|----------|--------|-----------------|
| `http://localhost:3010/v1/messages` | Anthropic Messages API | OpenClaw, Claude Code |
| `http://localhost:3010/v1/chat/completions` | OpenAI Chat Completions | CC Switch, Universal |

### Documentation

| Document | Description |
|----------|-------------|
| [Installation Guide](references/installation.md) | Docker deployment, verification, troubleshooting |
| [Token Management](references/token.md) | Obtaining and refreshing WorkosCursorSessionToken |
| [Configuration](references/configuration.md) | OpenClaw, Claude Code, CC Switch setup |
| [Quick Reference](references/quick-reference.md) | One-page cheat sheet |

### ⚠️ Important Notes

- **ToS Risk**: Using third-party proxies may violate Cursor's Terms of Service
- **Token Expiry**: Session tokens expire periodically; monitor and refresh as needed
- **API Stability**: Cursor's internal API may change without notice

---

## 🇨🇳 中文

### 概述

`cursor2api` 将 Cursor IDE 的 AI 模型桥接到 OpenClaw/Claude Code。它通过把 Cursor 内部 API 转换为标准 Anthropic/OpenAI 格式，让你可以通过任何兼容 API 的客户端使用 Cursor 的 Claude 订阅。

**架构：**
```
OpenClaw / Claude Code
         ↓ (ANTHROPIC_BASE_URL)
cursor2api Docker/Node (:3010)
         ↓ (Session Token)
Cursor 官方 API
```

### 前置要求

- Docker（容器部署）或 Node.js 18+（本地运行）
- Cursor 账号（需有有效的 AI 订阅）
- Cursor 的 `WorkosCursorSessionToken`

### 快速开始

```bash
# 1. 获取 WorkosCursorSessionToken（见 references/token.md）

# 2. 启动服务
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest

# 3. 配置 OpenClaw
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"

# 4. 重启 OpenClaw
openclaw gateway restart
```

### 核心操作

| 操作 | 命令 |
|------|------|
| **安装** | `docker run -d --name cursor-api -p 3010:3000 -e WORKOS_CURSOR_SESSION_TOKEN=token waitkafuka/cursor-api:latest` |
| **状态** | `docker ps \| grep cursor-api` |
| **续期 Token** | 见 `references/token.md` |
| **卸载** | `docker stop cursor-api && docker rm cursor-api` |

### API 端点

| 端点 | 格式 | 兼容 |
|------|------|------|
| `http://localhost:3010/v1/messages` | Anthropic Messages API | OpenClaw, Claude Code |
| `http://localhost:3010/v1/chat/completions` | OpenAI Chat Completions | CC Switch, 通用 |

### 文档

| 文档 | 说明 |
|------|------|
| [安装指南](references/installation.md) | Docker 部署、验证、故障排查 |
| [Token 管理](references/token.md) | 获取和续期 WorkosCursorSessionToken |
| [配置参考](references/configuration.md) | OpenClaw、Claude Code、CC Switch 配置 |
| [快速参考](references/quick-reference.md) | 一页速查表 |

### ⚠️ 注意事项

- **合规风险**：使用第三方代理可能违反 Cursor 服务条款
- **Token 过期**：Session Token 会过期，需定期检查和刷新
- **API 稳定性**：Cursor 内部 API 可能随时变化

<!-- tabs:end -->
