# Token Management / Token 管理

<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言                                                             ║
�══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English (default)    |    🇨🇳 中文                                        ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇬🇧 English

### Overview

`WorkosCursorSessionToken` is Cursor's session cookie that validates your subscription. It grants access to models included in your Cursor plan (e.g., Claude Sonnet 4).

**Characteristics:**
- Inherits your account's subscription benefits
- Expires periodically (hours to weeks)
- Must be refreshed when expired

### Obtaining Your Token

#### Method 1: Browser DevTools (Recommended)

**Open DevTools:**

| Method | Action |
|--------|--------|
| Menu | Three-dot menu → More tools → Developer tools |
| Right-click | Right-click anywhere → Inspect |
| Command menu | `Cmd+Shift+P` → Search "Show DevTools" |
| Shortcut | `Cmd+Option+I` (Mac) / `F12` (Windows/Linux) |

**Steps:**

1. Ensure you're logged into https://cursor.com
2. Open DevTools using any method above
3. Click the **Application** tab in DevTools
4. In the left sidebar, expand **Cookies** → select `https://cursor.com`
5. Find `WorkosCursorSessionToken`
6. Copy the full **Value** (it's a long string)

#### Method 2: CLI Verification

```bash
# Test if your token is valid
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=your_token" \
  https://api2.cursor.com/v1/me
```
- Returns `200` = Valid
- Returns `401` = Expired

### Token Refresh Flow

**Step 1: Check if expired**
```bash
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=your_token" \
  https://api2.cursor.com/v1/me
```

**Step 2: Refresh (if expired)**

1. Open https://cursor.com in your browser
2. Log out completely
3. Log back in
4. Refresh the page
5. Retrieve the new token from DevTools

**Step 3: Update Docker container**

```bash
# Stop old container
docker stop cursor-api
docker rm cursor-api

# Start with new token
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=new_token \
  waitkafuka/cursor-api:latest
```

### Auto-Refresh Script

Create `~/scripts/cursor-token-refresh.sh`:

```bash
#!/bin/bash
# cursor-token-refresh.sh - Auto-refresh cursor2api token

set -e

CONTAINER_NAME="cursor-api"
NEW_TOKEN="$1"

if [ -z "$NEW_TOKEN" ]; then
    echo "❌ Usage: ./cursor-token-refresh.sh <new_token>"
    exit 1
fi

echo "🔄 Stopping existing container..."
docker stop $CONTAINER_NAME 2>/dev/null || true
docker rm $CONTAINER_NAME 2>/dev/null || true

echo "🚀 Starting new container..."
docker run -d \
  --name $CONTAINER_NAME \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN="$NEW_TOKEN" \
  waitkafuka/cursor-api:latest

echo "✅ Token updated, container restarted"
```

Usage:
```bash
chmod +x ~/scripts/cursor-token-refresh.sh
~/scripts/cursor-token-refresh.sh "new_token"
```

### Token Expiry Monitoring

Add to crontab for hourly health checks:
```bash
0 * * * * curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=$(cat ~/.cursor_token)" \
  https://api2.cursor.com/v1/me | grep -q "200" || \
  echo "⚠️ Cursor Token may be expired"
```

### ⚠️ Security Notes

- **Never share your token** — anyone with it can access your Cursor account
- **Store securely** — use a password manager (1Password, etc.), never plaintext scripts
- **Handle expiry proactively** — expired tokens result in 401 errors

---

## 🇨🇳 中文

### 概述

`WorkosCursorSessionToken` 是 Cursor 的会话 Cookie，用于验证你的订阅资格。它授权访问你 Cursor 套餐中包含的模型（如 Claude Sonnet 4）。

**特点：**
- 继承你账号的订阅权益
- 会过期（数小时到数周不等）
- 过期后需要刷新

### 获取 Token

#### 方式 1：浏览器开发者工具（推荐）

**打开 DevTools：**

| 方式 | 操作 |
|------|------|
| 菜单栏 | 三点菜单 → 更多工具 → 开发者工具 |
| 右键 | 页面任意位置右键 → 检查 |
| 命令菜单 | `Cmd+Shift+P` → 搜索 "Show DevTools" |
| 快捷键 | `Cmd+Option+I` (Mac) / `F12` (Windows/Linux) |

**步骤：**

1. 确保已登录 https://cursor.com
2. 用上述任一方式打开 DevTools
3. 点击 DevTools 顶部的 **Application** 标签
4. 左侧展开 **Cookies** → 选择 `https://cursor.com`
5. 滚动找到 `WorkosCursorSessionToken`
6. 复制 **Value** 列的完整值（一长串字符）

#### 方式 2：命令行验证

```bash
# 测试 Token 是否有效
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=your_token" \
  https://api2.cursor.com/v1/me
```
- 返回 `200` = 有效
- 返回 `401` = 已过期

### Token 续期流程

**第一步：检查是否过期**
```bash
curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=your_token" \
  https://api2.cursor.com/v1/me
```

**第二步：刷新（如已过期）**

1. 在浏览器中打开 https://cursor.com
2. 完全退出登录
3. 重新登录
4. 刷新页面
5. 从 DevTools 重新获取 Token

**第三步：更新 Docker 容器**

```bash
# 停止旧容器
docker stop cursor-api
docker rm cursor-api

# 用新 Token 启动
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=new_token \
  waitkafuka/cursor-api:latest
```

### 自动续期脚本

创建 `~/scripts/cursor-token-refresh.sh`：

```bash
#!/bin/bash
# cursor-token-refresh.sh - 自动续期 cursor2api Token

set -e

CONTAINER_NAME="cursor-api"
NEW_TOKEN="$1"

if [ -z "$NEW_TOKEN" ]; then
    echo "❌ 用法: ./cursor-token-refresh.sh <新Token>"
    exit 1
fi

echo "🔄 停止现有容器..."
docker stop $CONTAINER_NAME 2>/dev/null || true
docker rm $CONTAINER_NAME 2>/dev/null || true

echo "🚀 启动新容器..."
docker run -d \
  --name $CONTAINER_NAME \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN="$NEW_TOKEN" \
  waitkafuka/cursor-api:latest

echo "✅ Token 已更新，容器已重启"
```

使用：
```bash
chmod +x ~/scripts/cursor-token-refresh.sh
~/scripts/cursor-token-refresh.sh "新Token"
```

### Token 有效期监控

添加到 crontab，每小时检查一次：
```bash
0 * * * * curl -s -o /dev/null -w "%{http_code}" \
  -H "Cookie: WorkosCursorSessionToken=$(cat ~/.cursor_token)" \
  https://api2.cursor.com/v1/me | grep -q "200" || \
  echo "⚠️ Cursor Token 可能已过期"
```

### ⚠️ 安全注意事项

- **不要分享你的 Token** — 任何人可用此 Token 访问你的 Cursor 账号
- **安全存储** — 建议使用密码管理器（如 1Password），不要明文写在脚本中
- **主动处理过期** — Token 过期后 API 请求会返回 401

<!-- tabs:end -->
