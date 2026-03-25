<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  🇨🇳 中文说明 (Chinese)  |  🇬🇧 English                                        ║
║  Language toggle: Use the tabs below / 使用下方标签切换                       ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇨🇳 中文说明

### 这是什么？

**cursor2api** 是一个代理服务，将 Cursor IDE 的免费 AI 对话转换为标准 Anthropic Messages API / OpenAI Chat Completions API 格式。

配合 [OpenClaw](https://github.com/openclaw/openclaw) 或 Claude Code 使用，让你可以用 Cursor 订阅的 Claude 模型（如 Claude Sonnet 4）。

### 主要特性

- 🌐 **标准 API 格式** — 支持 Anthropic Messages API 和 OpenAI Chat Completions
- 🐳 **Docker 部署** — 一键启动，开箱即用
- 🔄 **Token 自动续期** — 提供脚本简化 Token 刷新流程
- 📝 **双语文档** — 英文为主，支持中文切换

### 快速开始

#### 1. 获取 Token

1. 打开 [Cursor IDE](https://cursor.com) 并登录
2. 按 `Cmd+Option+I` 打开开发者工具
3. 切换到 **Application** → **Cookies** → `https://cursor.com`
4. 复制 `WorkosCursorSessionToken` 的值

#### 2. 启动服务

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=你的Token \
  waitkafuka/cursor-api:latest
```

#### 3. 配置环境变量

```bash
# 添加到 ~/.zshrc
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="你的Token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"

source ~/.zshrc
openclaw gateway restart
```

### OpenClaw 安装

```bash
# 使用 ClawHub 安装
clawhub install cursor2api
```

### 文档目录

| 文档 | 说明 |
|------|------|
| [SKILL.md](SKILL.md) | OpenClaw Skill 入口（含双语导航） |
| [references/installation.md](references/installation.md) | 完整安装指南 |
| [references/token.md](references/token.md) | Token 获取与续期详解 |
| [references/configuration.md](references/configuration.md) | 环境配置参考 |
| [references/quick-reference.md](references/quick-reference.md) | 速查表 |

### ⚠️ 注意事项

- **合规风险**：使用第三方代理可能违反 Cursor 服务条款，风险自担
- **Token 过期**：Session Token 会过期，过期后需重新获取
- **API 稳定性**：Cursor 内部 API 可能随时变化

---

## 🇬🇧 English

### What is this?

**cursor2api** is a proxy service that converts Cursor IDE's free AI conversations into standard Anthropic Messages API / OpenAI Chat Completions API format.

Use it with [OpenClaw](https://github.com/openclaw/openclaw) or Claude Code to access Cursor's Claude models (e.g., Claude Sonnet 4) through your existing API-compatible tools.

### Key Features

- 🌐 **Standard API Formats** — Supports both Anthropic Messages API and OpenAI Chat Completions
- 🐳 **Docker Deployment** — One-command startup
- 🔄 **Token Auto-Refresh** — Script to simplify token renewal
- 📝 **Bilingual Docs** — English primary with Chinese toggle

### Quick Start

#### 1. Get Your Token

1. Open [Cursor IDE](https://cursor.com) and log in
2. Press `Cmd+Option+I` to open DevTools
3. Go to **Application** → **Cookies** → `https://cursor.com`
4. Copy the value of `WorkosCursorSessionToken`

#### 2. Start the Service

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 3. Configure Environment

```bash
# Add to ~/.zshrc
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"

source ~/.zshrc
openclaw gateway restart
```

### OpenClaw Installation

```bash
# Via ClawHub
clawhub install cursor2api
```

### Documentation

| File | Description |
|------|-------------|
| [SKILL.md](SKILL.md) | OpenClaw Skill entry point (bilingual) |
| [references/installation.md](references/installation.md) | Full installation guide |
| [references/token.md](references/token.md) | Token acquisition & refresh |
| [references/configuration.md](references/configuration.md) | Environment configuration |
| [references/quick-reference.md](references/quick-reference.md) | One-page cheat sheet |

### ⚠️ Important Notes

- **ToS Risk**: Using third-party proxies may violate Cursor's Terms of Service
- **Token Expiry**: Session tokens expire; refresh when needed
- **API Stability**: Cursor's internal API may change without notice

<!-- tabs:end -->

---

## 📜 License

MIT License — see [LICENSE](LICENSE)
