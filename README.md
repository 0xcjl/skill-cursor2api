<!--
╔══════════════════════════════════════════════════════════════════════════════╗
║  Language / 语言 / Idioma / भाषा / اللغة / 言語                            ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  🇬🇧 English  |  🇨🇳 中文  |  🇪🇸 Español  |  🇮🇳 हिन्दी  |  🇸🇦 العربية  |  🇯🇵 日本語  ║
╚══════════════════════════════════════════════════════════════════════════════╝
-->

<!-- tabs:start -->

## 🇬🇧 English

### What is cursor2api?

**cursor2api** is a proxy service that converts Cursor IDE's free AI conversations into standard Anthropic Messages API / OpenAI Chat Completions API format.

Use it with [OpenClaw](https://github.com/openclaw/openclaw) or Claude Code to access Cursor's Claude models (e.g., Claude Sonnet 4) through your existing API-compatible tools.

### Features

- 🌐 **Standard API Formats** — Anthropic Messages API + OpenAI Chat Completions
- 🐳 **Docker Deployment** — One-command startup
- 🔄 **Token Auto-Refresh** — Scripts to simplify token renewal
- 📚 **Multi-language Docs** — English, Chinese, Spanish, Hindi, Arabic, Japanese

### Quick Start

#### 1. Get Your Token

1. Open [Cursor IDE](https://cursor.com) and log in
2. Press `Cmd+Option+I` → **Application** → **Cookies** → `https://cursor.com`
3. Copy `WorkosCursorSessionToken` value

#### 2. Start Service

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 3. Configure

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc && openclaw gateway restart
```

### Install via OpenClaw

```bash
clawhub install cursor2api
```

### Documentation

| File | Description |
|------|-------------|
| [SKILL.md](SKILL.md) | OpenClaw Skill entry point |
| [references/installation.md](references/installation.md) | Full installation guide |
| [references/token.md](references/token.md) | Token acquisition & refresh |
| [references/configuration.md](references/configuration.md) | Environment configuration |
| [references/quick-reference.md](references/quick-reference.md) | One-page cheat sheet |

### ⚠️ Notes

- **ToS Risk**: Third-party proxies may violate Cursor's Terms of Service
- **Token Expiry**: Session tokens expire; refresh when needed
- **API Stability**: Cursor's internal API may change

---

## 🇨🇳 中文

### cursor2api 是什么？

**cursor2api** 是一个代理服务，将 Cursor IDE 的 AI 对话转换为标准 Anthropic Messages API / OpenAI Chat Completions API 格式。

配合 [OpenClaw](https://github.com/openclaw/openclaw) 或 Claude Code 使用，通过 API 兼容工具访问 Cursor 的 Claude 模型（如 Claude Sonnet 4）。

### 特性

- 🌐 **标准 API 格式** — 支持 Anthropic Messages API 和 OpenAI Chat Completions
- 🐳 **Docker 部署** — 一键启动
- 🔄 **Token 自动续期** — 脚本简化刷新流程
- 📚 **多语言文档** — 英文、中文、西班牙语、印地语、阿拉伯语、日语

### 快速开始

#### 1. 获取 Token

1. 打开 [Cursor IDE](https://cursor.com) 并登录
2. 按 `Cmd+Option+I` → **Application** → **Cookies** → `https://cursor.com`
3. 复制 `WorkosCursorSessionToken` 的值

#### 2. 启动服务

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=你的Token \
  waitkafuka/cursor-api:latest
```

#### 3. 配置环境

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="你的Token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc && openclaw gateway restart
```

### OpenClaw 安装

```bash
clawhub install cursor2api
```

### 文档

| 文件 | 说明 |
|------|------|
| [SKILL.md](SKILL.md) | OpenClaw Skill 入口 |
| [references/installation.md](references/installation.md) | 完整安装指南 |
| [references/token.md](references/token.md) | Token 获取与续期 |
| [references/configuration.md](references/configuration.md) | 环境配置参考 |
| [references/quick-reference.md](references/quick-reference.md) | 速查表 |

### ⚠️ 注意

- **合规风险**：使用第三方代理可能违反 Cursor 服务条款
- **Token 过期**：需定期刷新
- **API 稳定性**：Cursor 内部 API 可能变化

---

## 🇪🇸 Español

### ¿Qué es cursor2api?

**cursor2api** es un servicio proxy que convierte las conversaciones de IA de Cursor IDE al formato estándar Anthropic Messages API / OpenAI Chat Completions.

Úsalo con [OpenClaw](https://github.com/openclaw/openclaw) o Claude Code para acceder a los modelos Claude de Cursor (ej. Claude Sonnet 4).

### Características

- 🌐 **API Estándar** — Anthropic Messages API + OpenAI Chat Completions
- 🐳 **Docker** — Inicio con un comando
- 🔄 **Auto-renovación de Token** — Scripts para simplificar la renovación
- 📚 **Documentación Multilingüe**

### Inicio Rápido

#### 1. Obtén tu Token

1. Abre [Cursor IDE](https://cursor.com) e inicia sesión
2. Presiona `Cmd+Option+I` → **Application** → **Cookies** → `https://cursor.com`
3. Copia el valor de `WorkosCursorSessionToken`

#### 2. Inicia el Servicio

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=tu_token \
  waitkafuka/cursor-api:latest
```

#### 3. Configura

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="tu_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc && openclaw gateway restart
```

### Instalación

```bash
clawhub install cursor2api
```

---

## 🇮🇳 हिन्दी

### cursor2api क्या है?

**cursor2api** एक प्रॉक्सी सेवा है जो Cursor IDE की AI बातचीत को मानक Anthropic Messages API / OpenAI Chat Completions API फॉर्मेट में बदलती है।

[OpenClaw](https://github.com/openclaw/openclaw) या Claude Code के साथ उपयोग करें।

### विशेषताएं

- 🌐 **मानक API फॉर्मेट** — Anthropic + OpenAI समर्थन
- 🐳 **Docker डिप्लॉयमेंट** — एक कमांड में शुरू
- 🔄 **टोकन ऑटो-रिफ्रेश** — स्क्रिप्ट से आसान नवीनीकरण
- 📚 **बहु-भाषी डॉक्यूमेंटेशन**

### त्वरित शुरू

#### 1. टोकन प्राप्त करें

1. [Cursor IDE](https://cursor.com) खोलें और लॉगिन करें
2. `Cmd+Option+I` दबाएं → **Application** → **Cookies** → `https://cursor.com`
3. `WorkosCursorSessionToken` की वैल्यू कॉपी करें

#### 2. सेवा शुरू करें

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 3. कॉन्फ़िगर करें

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
source ~/.zshrc && openclaw gateway restart
```

### इंस्टॉल

```bash
clawhub install cursor2api
```

---

## 🇸🇦 العربية

### ما هو cursor2api؟

**cursor2api** هو خدمة وسيطة تحوّل محادثات Cursor IDE إلى صيغة Anthropic Messages API / OpenAI Chat Completions القياسية.

استخدمه مع [OpenClaw](https://github.com/openclaw/openclaw) أو Claude Code.

### المميزات

- 🌐 **صيغ API قياسية** — دعم Anthropic + OpenAI
- 🐳 **Docker** — تشغيل بأمر واحد
- 🔄 **تجديد التوكن التلقائي** — سكريبتات للتسهيل
- 📚 **وثائق متعددة اللغات**

### البدء السريع

#### 1. احصل على التوكن

1. افتح [Cursor IDE](https://cursor.com) وسجّل الدخول
2. اضغط `Cmd+Option+I` → **Application** → **Cookies** → `https://cursor.com`
3. انسخ قيمة `WorkosCursorSessionToken`

#### 2. ابدأ الخدمة

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 3. اضبط الإعدادات

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
source ~/.zshrc && openclaw gateway restart
```

### التثبيت

```bash
clawhub install cursor2api
```

---

## 🇯🇵 日本語

### cursor2api とは？

**cursor2api** は、Cursor IDE の AI 対話を標準的な Anthropic Messages API / OpenAI Chat Completions API 形式に変換するプロキシサービス です。

[OpenClaw](https://github.com/openclaw/openclaw) や Claude Code で使用し、Cursor の Claude モデルにアクセスできます。

### 特徴

- 🌐 **標準API形式** — Anthropic Messages API + OpenAI Chat Completions 対応
- 🐳 **Docker対応** — ワンコマンドで起動
- 🔄 **トークン自動更新** — スクリプトで更新を簡略化
- 📚 **多言語ドキュメント** — 6言語対応

### クイックスタート

#### 1. トークンを取得

1. [Cursor IDE](https://cursor.com) を開いてログイン
2. `Cmd+Option+I` → **Application** → **Cookies** → `https://cursor.com`
3. `WorkosCursorSessionToken` の値をコピー

#### 2. サービスを起動

```bash
docker run -d \
  --name cursor-api \
  -p 3010:3000 \
  -e WORKOS_CURSOR_SESSION_TOKEN=your_token \
  waitkafuka/cursor-api:latest
```

#### 3. 環境設定

```bash
export ANTHROPIC_BASE_URL="http://localhost:3010/v1"
export ANTHROPIC_API_KEY="your_token"
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-6"
source ~/.zshrc && openclaw gateway restart
```

### インストール

```bash
clawhub install cursor2api
```

<!-- tabs:end -->

---

## 📜 License

MIT License — see [LICENSE](LICENSE)
