# 第 1 課：OpenClaw 是什麼？快速上手

> **課程難度**：⭐ 入門
> **預計學習時間**：30 分鐘
> **來源**：菜鳥教程 OpenClaw (Clawdbot) 教程

---

## OpenClaw 簡介

OpenClaw（原名 Clawdbot，過渡名 Moltbot）是 **2026 年 1 月突然爆火**的開源個人 AI 助手項目，由 Peter Steinberger（PSPDFKit 創始人）開發。

![OpenClaw](https://www.runoob.com/wp-content/uploads/2026/01/Moltbot-Clawdbot-runoob3.webp)

OpenClaw 是一個**可執行任務的智能體**，我們給指令，它不僅回答，還能：

- 🖥️ 主動操作系統
- 🌐 訪問網頁
- 📧 處理郵件
- 📁 整理文件
- ⏰ 發起提醒
- 💻 **自動編寫代碼**

**核心理念**：讓 AI 不只是給建議，而是**直接完成完整工程任務**。

---

## 名字演進史

![Clawdbot 到 OpenClaw](https://www.runoob.com/wp-content/uploads/2026/01/Moltbot-Clawdbot-runoob2.png)

- **Clawdbot**：最初項目名，靈感來自 Claude 和 claw（龍蝦爪）梗
- **Moltbot**：2026 年 1 月 27 日因 Anthropic 律師函被要求更名（脫皮龍蝦之意）
- **OpenClaw**：2026 年 1 月 30 日之後拋棄版權衝突，強調開源性，是目前最終官方名稱

| 名稱 | 時間線 | 背景/原因 |
|------|--------|----------|
| Clawdbot | 2025年末至2026年1月初 | 最初項目名；靈感來自 Claude 和 claw（龍蝦爪）梗 |
| Moltbot | 2026年1月27日 | 因 Anthropic 律師函被要求更名 |
| OpenClaw | 2026年1月30日之後 | 拋棄版權衝突，強調開源性/長線品牌 |

---

## 安裝 OpenClaw

### 系統要求

硬體要求極低，**2GB RAM 即可運行**。

支援：Mac、Windows、Linux
需要：Node.js (pnpm) 或使用 Docker

### 方法一：一鍵腳本（推薦）

**macOS / Linux：**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell)：**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### 方法二：手動安裝

需要 Node.js ≥ 22

```bash
# 使用 npm
npm i -g openclaw

# 國內鏡像
npm i -g openclaw --registry=https://registry.npmmirror.com

# 或使用 pnpm
pnpm add -g openclaw
```

### 方法三：從原始碼安裝（開發模式）

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
pnpm install
pnpm ui:build
pnpm build
pnpm openclaw onboard --install-daemon
```

---

## 初始化設定（onboard）

安裝完成後，執行初始化向導：

```bash
openclaw onboard
```

### 設定流程截圖

![QuickStart 選項](https://www.runoob.com/wp-content/uploads/2026/01/fe0e8572-f35b-4e20-8b00-7723e48ec498.png)

1. **選擇快速啟動**：選 `QuickStart`

![配置大模型](https://www.runoob.com/wp-content/uploads/2026/01/e1de4820-039c-42f8-9189-761ca9baa593.png)

2. **配置大模型**：選擇 AI 供應商（支援 Qwen、MiniMax、智譜等國內 API）

![選擇聊天工具](https://www.runoob.com/wp-content/uploads/2026/01/aca86b08-25b3-4b9b-80ae-efb6eced5252.png)

3. **配置聊天工具**：選擇聊天通道

4. **配置技能（Skills）**：可用 `空格` 選擇或跳過

5. **開啟鉤子**：建議開啟內容引導日誌和會話記錄

6. **打開 Web UI**：瀏覽器訪問 `http://127.0.0.1:18789/chat`

### 認證配置文件位置

```
~/.openclaw/agents/<agentId>/agent/auth-profiles.json
```

---

## 啟動後的使用

![OpenClaw Web UI](https://www.runoob.com/wp-content/uploads/2026/01/c6da4d06-b50f-4b11-aebc-bdea5c5db859-scaled.png)

安裝完後，就會自動訪問 `http://127.0.0.1:18789/chat`，就可以打開聊天界面讓它開始工作。

比如搜索最新的科技新聞：

![搜索示例](https://www.runoob.com/wp-content/uploads/2026/01/78ba08f8-9c17-476d-9c01-fecf9741bc57.png)

啟動後，我們可以使用 `openclaw status` 命令查看狀態：

![狀態查看](https://www.runoob.com/wp-content/uploads/2026/01/4fddc7d3-e0c0-44fc-98f8-e81cd32faf5b.png)

---

## 常用命令

| 命令 | 說明 |
|------|------|
| `openclaw onboard` | 初始化向導 |
| `openclaw doctor` | 健康檢查 |
| `openclaw status` | 查看狀態 |
| `openclaw gateway status` | 查看網關服務狀態 |
| `openclaw dashboard` | 開啟控制面板 |
| `openclaw logs` | 查看實時日誌 |
| `openclaw uninstall` | 卸載 OpenClaw |

---

## 技能（Skills）系統

技能是包含 `SKILL.md` 文件的獨立文件夾。

### ClawHub 技能市場

- 官網：https://clawhub.ai/
- 國內鏡像：https://skillhub.tencent.com/

### 安裝 ClawHub

```bash
# 推薦方式（npx）
npx clawhub@latest --version

# 全局安裝
npm install -g clawhub
```

### 常用命令

```bash
clawhub login                    # 登錄
clawhub search "postgres backups"  # 搜索技能
clawhub install my-skill-pack    # 安裝技能
clawhub update --all            # 批量更新
```

![ClawHub 搜索](https://www.runoob.com/wp-content/uploads/2026/01/f0249b24-068d-472a-8182-594c35703c9b.png)

---

## 插件系統

插件是輕量代碼模塊，可擴展 OpenClaw 功能。

```bash
# 查看已加載插件
openclaw plugins list

# 安裝官方插件（示例：語音通話）
openclaw plugins install @openclaw/voice-call

# 重啟網關生效
openclaw gateway restart
```

---

## 🦞 總結

OpenClaw 是一個把 **本地算力 + 大模型 Agent 自動化** 玩到極致的開發者效率工具。

**核心優勢**：
- 安裝簡單，一鍵腳本搞定
- 系統要求低，2GB RAM 就能跑
- 不只是聊天，能真正執行任務
- 開源免費，社群活躍

---

## 下節課預告

> **第 2 課**：OpenClaw 一鍵部署 — 詳細教學如何在各種環境部署 OpenClaw

---

