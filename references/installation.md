# Installation Guide / 安装指南

<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言                                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English (default)    |    🇨🇳 中文                                        ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇬🇧 English

### Prerequisites

- Docker installed and running
- Cursor account with active AI subscription
- Valid `WorkosCursorSessionToken`

### Docker Deployment

#### Option A: Docker Run (Recommended)

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### Option B: Docker Compose (For Long-term Use)

Create `docker-compose.yml`:

```yaml
version: '3.8'
services:
  cursor-api:
    image: waitkafuka/cursor-api:latest
    container_name: cursor-api
    ports:
      - "3010:3000"
    environment:
      WORKOS_CURSOR_SESSION_TOKEN: your_token
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```

Start:
```bash
docker compose up -d
```

### Verify Deployment

**Check container status:**
```bash
docker ps | grep cursor-api
```

**Test API endpoints:**

OpenAI format:
```bash
curl -X POST http://localhost:3010/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_token" \
  -d '{
    "model": "claude-sonnet-4",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Anthropic Messages API format:
```bash
curl -X POST http://localhost:3010/v1/messages \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_token" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "claude-sonnet-4-20250514",
    "max_tokens": 1024,
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Container won't start | Run `docker logs cursor-api` — usually invalid token |
| API returns 401 | Token expired, retrieve new one |
| Port conflict | Change `-p 3011:3000` and update config accordingly |

---

## 🇨🇳 中文

### 前置要求

- Docker 已安装并运行
- Cursor 账号（需有有效的 AI 订阅）
- 有效的 `WorkosCursorSessionToken`

### Docker 部署

#### 方式 A：Docker Run（推荐快速启动）

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 方式 B：Docker Compose（适合长期使用）

创建 `docker-compose.yml`：

```yaml
version: '3.8'
services:
  cursor-api:
    image: waitkafuka/cursor-api:latest
    container_name: cursor-api
    ports:
      - "3010:3000"
    environment:
      WORKOS_CURSOR_SESSION_TOKEN: your_token
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```

启动：
```bash
docker compose up -d
```

### 验证部署

**检查容器状态：**
```bash
docker ps | grep cursor-api
```

**测试 API 端点：**

OpenAI 格式：
```bash
curl -X POST http://localhost:3010/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_token" \
  -d '{
    "model": "claude-sonnet-4",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

Anthropic Messages API 格式：
```bash
curl -X POST http://localhost:3010/v1/messages \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_token" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "claude-sonnet-4-20250514",
    "max_tokens": 1024,
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

### 故障排查

| 问题 | 解决方案 |
|------|---------|
| 容器启动失败 | 运行 `docker logs cursor-api` — 通常是 Token 无效 |
| API 返回 401 | Token 已过期，需要重新获取 |
| 端口冲突 | 改为 `-p 3011:3000` 并相应更新配置 |

<!-- tabs:end -->
