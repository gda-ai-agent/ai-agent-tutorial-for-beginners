# 第 1 課：OpenClaw 是什麼？快速上手

> **課程難度**：⭐ 入門
> **預計學習時間**：30 分鐘
> **來源**：菜鳥教程 OpenClaw (Clawdbot) 教程

---

## OpenClaw 簡介

OpenClaw（原名 Clawdbot，過渡名 Moltbot）是 **2026 年 1 月突然爆火**的開源個人 AI 助手項目，由 Peter Steinberger（PSPDFKit 創始人）開發。

### 為什麼叫 OpenClaw？

- **Clawdbot**：最初項目名，靈感來自 Claude 和 claw（龍蝦爪）梗
- **Moltbot**：2026 年 1 月 27 日因 Anthropic 律師函被要求更名（脫皮龍蝦之意）
- **OpenClaw**：2026 年 1 月 30 日之後拋棄版權衝突，強調開源性，是目前最終官方名稱

### OpenClaw 能做什麼？

OpenClaw 是一個**可執行任務的智能體**，我們給指令，它不僅回答，還能：

- 🖥️ 主動操作系統
- 🌐 訪問網頁
- 📧 處理郵件
- 📁 整理文件
- ⏰ 發起提醒
- 💻 **自動編寫代碼**

**核心理念**：讓 AI 不只是給建議，而是**直接完成完整工程任務**。

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

### 設定流程

1. **選擇快速啟動**：選 `QuickStart`
2. **配置大模型**：選擇 AI 供應商（支援 Qwen、MiniMax、智譜等國內 API）
3. **配置聊天工具**：選擇聊天通道
4. **配置技能（Skills）**：可用 `空格` 選擇或跳過
5. **開啟鉤子**：建議開啟內容引導日誌和會話記錄
6. **打開 Web UI**：瀏覽器訪問 `http://127.0.0.1:18789/chat`

### 認證配置文件位置

```
~/.openclaw/agents/<agentId>/agent/auth-profiles.json
```

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

*本課程內容整理自[菜鳥教程 OpenClaw (Clawdbot) 教程](https://www.runoob.com/ai-agent/openclaw-clawdbot-tutorial.html)，版權歸原作者所有。*
