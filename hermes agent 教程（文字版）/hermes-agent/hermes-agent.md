# Hermes Agent

> **課程難度**：⭐⭐⭐ 中級
> **預計學習時間**：60 分鐘
> **來源**：菜鳥教程 Hermes Agent

---

## 簡介

![Hermes Agent](https://www.runoob.com/wp-content/uploads/2026/04/hermes-agent.png)

近年來，AI 智能體（AI Agent）領域發展迅猛，從單純的聊天機器人進化到能真正做事、持久記憶並自主成長的智能體。

**Hermes Agent** 是 Nous Research 開源的自主 AI Agent 框架。

- 🌐 **GitHub**：https://github.com/nousresearch/hermes-agent
- 🌐 **官網**：https://hermes-agent.nousresearch.com/

---

## 核心理念

官方定義：

> The agent that grows with you.
> 一個會隨著使用不斷成長的 Agent。

它是一個自主智能體，**運行時間越長，能力就越強**。

Hermes Agent 的核心理念是：

> 讓 AI 成為長期在線的數字員工，而非一次性聊天機器人。

Hermes Agent 是業內少見的**原生內置學習閉環的 AI Agent**，可從執行經驗中沉澱技能、自主優化能力、持久化知識、檢索歷史對話，並在跨會話中持續完善用戶認知模型。

---

## 支援的大模型

Hermes Agent 支持自由切換任意大模型，包括 Nous Portal、OpenRouter（200+ 模型）、OpenAI、GLM、Kimi、MiniMax 等，執行 `hermes model` 即可切換，無需改代碼、無廠商鎖定。

| 提供商 | 說明 | 設置方式 |
|--------|------|----------|
| Nous Portal | 訂閱制，零配置 | 通過 `hermes model` 進行 OAuth 登錄 |
| OpenAI Codex | ChatGPT OAuth，使用 Codex 模型 | 通過 `hermes model` 進行設備代碼認證 |
| Anthropic | 直接使用 Claude 模型 | 通過 Claude Code 認證或 Anthropic API 密鑰 |
| OpenRouter | 多提供商路由 | 輸入您的 API 密鑰 |
| DeepSeek | 直接 DeepSeek API 訪問 | 設置 `DEEPSEEK_API_KEY` |
| Hugging Face | 通過統一路由器訪問 20+ 開放模型 | 設置 `HF_TOKEN` |
| 自定義端點 | VLLM、SGLang、Ollama 或任何 OpenAI 兼容 API | 設置基礎 URL 和 API 密鑰 |

---

## 核心特性

![特性截圖](https://www.runoob.com/wp-content/uploads/2026/04/9eecf986-5c45-4099-8221-4ef1b2b98d9c.png)

| 特性 | 能力說明 |
|------|----------|
| 原生終端交互 | 完整 TUI 界面，支援多行編輯、命令補全、歷史回溯、流式輸出等 |
| 全平台接入 | 一個網關接入 CLI、Telegram、Discord、Slack、WhatsApp 等多端 |
| 閉環學習體系 | 自主管理記憶、技能生成與優化、跨會話召回、用戶建模 |
| 定時自動化 | 內置 Cron 調度，支援日報、備份、審計等 7×24 自動任務 |
| 並行任務處理 | 支援子 Agent 並行執行、多工作流拆分與 RPC 工具調用 |
| 多環境運行 | 支援本地、Docker、SSH、Daytona、Modal 等 6 種後端 |
| 科研級能力 | 支援軌跡生成，強化學習環境、訓練數據壓縮 |

---

## 快速安裝

### 自動安裝（Linux、macOS、WSL2）

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

安裝程序會自動處理所有依賴項：
- `uv` — 快速 Python 包管理器
- Python 3.11 — 通過 uv 安裝，無需 sudo
- Node.js v22 — 用於瀏覽器自動化和 WhatsApp 橋接
- `ripgrep` — 快速文件搜索
- `ffmpeg` — TTS 音頻格式轉換

> ⚠️ Windows 系統不支援原生 Windows 環境，請先安裝 WSL2。

### 配置模型

![模型配置](https://www.runoob.com/wp-content/uploads/2026/04/f3520566-450f-4e5b-b94a-64e62fa6c777.png)

選擇倒數第二項的 **More providers**：

![更多提供商](https://www.runoob.com/wp-content/uploads/2026/04/d186a7cf-fe80-4ea7-8631-dd3f9e425cc5.png)

本文使用百煉的 Coding Plan，選擇 **Customer endpoint**（自定義 API 地址與 API key）。

**Base URL 設置百煉兼容 OpenAI 接口協議工具**：
```
https://coding.dashscope.aliyuncs.com/v1
```

### 啟動

```bash
source ~/.bashrc    # 重載shell配置（若使用zsh，執行：source ~/.zshrc）
hermes              # 開啟智能體對話！
```

---

## 常用命令

| 命令 | 說明 |
|------|------|
| `hermes` | 交互式命令列界面 — 開啟對話 |
| `hermes model` | 選擇大語言模型服務商與對應模型 |
| `hermes tools` | 配置啟用的工具集 |
| `hermes config set` | 設置單項配置項 |
| `hermes gateway` | 啟動消息網關（支援Telegram、Discord等平台） |
| `hermes setup` | 運行全量配置向導（一站式完成所有配置） |
| `hermes claw migrate` | 從OpenClaw遷移數據（適用於原OpenClaw用戶） |
| `hermes update` | 更新至最新版本 |
| `hermes doctor` | 診斷運行環境與配置問題 |

---

## 手動安裝

### 步驟 1：克隆倉庫

```bash
git clone --recurse-submodules https://github.com/NousResearch/hermes-agent.git
cd hermes-agent
```

如果已經克隆但沒有子模組：
```bash
git submodule update --init --recursive
```

### 步驟 2：安裝 uv 並創建虛擬環境

```bash
# 安裝 uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# 創建 Python 3.11 的虛擬環境
uv venv venv --python 3.11
```

### 步驟 3：安裝 Python 依賴

```bash
# 告訴 uv 要安裝到哪個虛擬環境
export VIRTUAL_ENV="$(pwd)/venv"

# 安裝所有擴展
uv pip install -e ".[all]"
```

**可選擴展說明**：

| 擴展 | 功能 | 安裝命令 |
|------|------|----------|
| `all` | 包含以下所有功能 | `uv pip install -e ".[all]"` |
| `messaging` | Telegram 和 Discord 網關 | `uv pip install -e ".[messaging]"` |
| `cron` | 定時任務的 Cron 表達式解析 | `uv pip install -e ".[cron]"` |
| `voice` | CLI 麥克風輸入和音頻播放 | `uv pip install -e ".[voice]"` |
| `mcp` | 模型上下文協議支援 | `uv pip install -e ".[mcp]"` |
| `honcho` | AI 原生記憶（Honcho 集成） | `uv pip install -e ".[honcho]"` |

### 步驟 4：創建配置目錄

```bash
# 創建目錄結構
mkdir -p ~/.hermes/{cron,sessions,logs,memories,skills,pairing,hooks,image_cache,audio_cache,whatsapp/session}

# 複製示例配置檔案
cp cli-config.yaml.example ~/.hermes/config.yaml

# 創建空的 .env 文件
touch ~/.hermes/.env
```

### 步驟 5：添加 API 密鑰

打開 `~/.hermes/.env` 並添加至少一個 LLM 提供商密鑰：

```bash
# 必需 — 至少一個 LLM 提供商：
OPENROUTER_API_KEY=sk-or-v1-your-key-here

# 可選 — 啟用其他工具：
FIRECRAWL_API_KEY=fc-your-key          # 網頁搜索和抓取
FAL_KEY=your-fal-key                   # 圖像生成（FLUX）
```

或通過 CLI 設置：
```bash
hermes config set OPENROUTER_API_KEY sk-or-v1-your-key-here
```

### 步驟 6：將 hermes 添加到 PATH

```bash
mkdir -p ~/.local/bin
ln -sf "$(pwd)/venv/bin/hermes" ~/.local/bin/hermes
```

### 步驟 7：驗證安裝

```bash
hermes version    # 檢查命令是否可用
hermes doctor     # 運行診斷以驗證一切正常
hermes status     # 檢查您的配置
hermes chat -q "Hello! What tools do you have available?"
```

---

## 消息網關

![消息網關](https://www.runoob.com/wp-content/uploads/2026/04/edee3a65-14bf-4633-9da3-9b40d1109385.png)

Hermes Agent 消息網關允許您通過多個平台與智能體交互——Telegram、Discord、Slack、WhatsApp、Signal、Email、Home Assistant 等。

從一個網關向 **15+ 個平台**發送消息。無論您身在何處，都可以與 Hermes 保持聯繫。

| 平台 | 說明 | 狀態 |
|------|------|------|
| Telegram | 即時消息 | ✅ |
| Discord | 社群平台 | ✅ |
| Slack | 企業溝通 | ✅ |
| WhatsApp | 社交消息 | ✅ |
| Signal | 私密通信 | ✅ |
| Email | 郵件 | ✅ |
| Home Assistant | 智能家居 | ✅ |

---

## 故障排除

| 問題 | 解決方案 |
|------|----------|
| `hermes: command not found` | 重新載入 shell（`source ~/.bashrc`）或檢查 PATH |
| API 密鑰未設置 | 運行 `hermes model` 配置提供商 |
| 更新後配置丟失 | 運行 `hermes config check` 然後 `hermes config migrate` |

---

## 🦞 總結

Hermes Agent 是一個會隨著使用不斷成長的 AI Agent。

**核心優勢**：
- 原生內置學習閉環
- 支援 200+ 大模型自由切換
- 多平台接入（15+ 平台）
- 定時自動化任務
- 從 OpenClaw 輕鬆遷移

---

## 相關連結

- 🌐 [Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent)
- 🌐 [Hermes Agent 官網](https://hermes-agent.nousresearch.com/)
- 📚 [菜鳥教程首頁](https://www.runoob.com/ai-agent/hermes-agent.html)

---

*本課程內容整理自[菜鳥教程 Hermes Agent](https://www.runoob.com/ai-agent/hermes-agent.html)，版權歸原作者所有。*
