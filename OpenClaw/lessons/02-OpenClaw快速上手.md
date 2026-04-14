# 第 2 課：OpenClaw 快速上手

> **課程難度**：⭐ 入門
> **預計學習時間**：30 分鐘
> **來源**：菜鳥教程 OpenClaw 快速上手

---

## 前置準備

![快速上手截圖](https://www.runoob.com/wp-content/uploads/2026/03/fa28850c-9178-4d8b-a42e-c29c79d18eb9.png)

在開始使用 OpenClaw 之前，需要確保環境滿足以下條件。

### 環境要求

- **作業系統**：支援 macOS、Windows、Linux
- **硬體**：極低，2GB RAM 即可運行
- **依賴**：Node.js ≥ 22（使用 nvm 或官網安裝包）

### 檢查 Node.js 版本

```bash
node --version
# 確認版本 ≥ 22.x
```

### 安裝或升級 Node.js

```bash
# 使用 nvm（推薦）
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 22
nvm use 22

# 或直接下載安裝包
# https://nodejs.org/
```

---

## 安裝 OpenClaw

### 方法一：一鍵腳本（推薦）

```bash
# macOS / Linux
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows (PowerShell)
iwr -useb https://openclaw.ai/install.ps1 | iex
```

### 方法二：使用 npm / pnpm

```bash
# 使用 npm
npm i -g openclaw

# 使用 pnpm
pnpm add -g openclaw

# 國內鏡像
npm i -g openclaw --registry=https://registry.npmmirror.com
```

---

## 首次啟動向導

安裝完成後，執行 `openclaw onboard` 進入初始化向導。

### 選擇語言

![語言選擇](https://www.runoob.com/wp-content/uploads/2026/03/375ed222-f099-417a-874c-f7299a9f9537.png)

選擇偏好的語言環境。

### 選擇配置方式

![配置方式](https://www.runoob.com/wp-content/uploads/2026/03/3f1213fb-93d4-49f2-8b01-b952c7e2326e.png)

- **快速配置（QuickStart）**：適合新手，一鍵完成
- **自訂配置（Manual）**：適合進階用戶

### 配置 AI 模型

![AI 模型配置](https://www.runoob.com/wp-content/uploads/2026/03/a203baa1-51f1-4f70-8182-45c9a6793484.png)

選擇 AI 供應商和模型：

| 供應商 | 模型示例 | 特色 |
|--------|----------|------|
| Anthropic | Claude Sonnet 4 | 平衡、安全、多語言 |
| OpenAI | GPT-4 | 專業、知識廣 |
| DeepSeek | DeepSeek-V3 | 代碼能力強、便宜 |
| 阿里雲 | Qwen | 國內友好 |

### 配置聊天渠道

![聊天渠道](https://www.runoob.com/wp-content/uploads/2026/03/7e905c64-8183-41cc-8b8b-aa5686c14ad5.png)

選擇要連接的聊天平台：

- 💬 Discord
- 💬 Telegram
- 💬 WhatsApp
- 💬 飛書（中國）
- 💬 釘釘（中國）

### 啟動成功

![啟動成功](https://www.runoob.com/wp-content/uploads/2026/03/a1604c55-c0e0-4810-963a-8c922d8d1ecc.png)

完成後，系統會顯示存取網址。

---

## 訪問 Web UI

![Web UI](https://www.runoob.com/wp-content/uploads/2026/03/44798f20-6d3b-44a2-95e7-dfd6b97b7c38.png)

啟動後，存取以下網址：

```
http://127.0.0.1:18789/chat
```

或在瀏覽器中直接打開 OpenClaw 控制面板。

---

## 快速驗證

### 發送第一個指令

在 Web UI 中輸入：

```
幫我搜尋今天的科技新聞
```

OpenClaw 會自動搜尋並總結結果。

### 使用 CLI 命令

```bash
# 查看狀態
openclaw status

# 查看幫助
openclaw --help
```

---

## 疑難排解

### 常見問題

| 問題 | 解決方案 |
|------|----------|
| 安裝失敗 | 確認 Node.js 版本 ≥ 22 |
| 無法啟動 | 執行 `openclaw doctor` 健康檢查 |
| 無法連接 | 檢查端口 18789 是否被佔用 |

### 健康檢查

```bash
openclaw doctor
```

---

## 下節課預告

> **第 3 課**：OpenClaw 配置目錄詳解 — 深入了解配置文件的結構和作用

---

*本課程內容整理自[菜鳥教程 OpenClaw 快速上手](https://www.runoob.com/ai-agent/openclaw-quickstart.html)，版權歸原作者所有。*
