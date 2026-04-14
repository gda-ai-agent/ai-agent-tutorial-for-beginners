# 第 5 課：OpenClaw 工作原理

> **課程難度**：⭐⭐⭐⭐ 高級
> **預計學習時間**：60 分鐘
> **來源**：菜鳥教程 OpenClaw 工作原理

---

## 整體架構

![工作原理圖](https://www.runoob.com/wp-content/uploads/2026/03/1_eZX31-3n0KTJ2MY1RB0JBg.png)

OpenClaw 採用經典的三層架構設計：

---

## 三層架構

### 外層：用戶接口（Channels）

負責跟 WhatsApp、Telegram 等聊天軟件"握手"。比如用 Baileys 庫連接 WhatsApp。

**支援的平台**：
- 💬 Discord
- 💬 Telegram
- 💬 WhatsApp
- 💬 飛書
- 💬 釘釘

### 中層：網關（Gateway）

唯一運行的進程（佔用一個端口，預設 18789），像總機接線員，把消息轉發給 AI。

**Gateway 的三大職責**：
1. **認證（Authentication）** - 確保只有你授權的平台才能連接
2. **路由（Routing）** - 把消息送到正確的工作空間
3. **日誌記錄（Logging）** - 記錄所有交互，方便調試和審計

### 內層：能力層

- **AI 大腦** - 真正思考的是外部大模型（你提供 API Key）
- **工具 & 技能** - AI 的手腳，比如打開瀏覽器、讀寫檔案、發郵件
- **記憶系統** - 像筆記本，AI 不會忘掉你上次說的話

---

## 消息處理流程

### 完整消息流程圖

![消息流程圖](https://www.runoob.com/wp-content/uploads/2026/03/openclaw-how-it-works-runoob-2.png)

讓我們用一個真實例子："在 WhatsApp 裡說：幫我整理今天的郵件發給我"。

### 詳細拆解

#### 步驟 1-3：消息接收與標準化

用戶在 Telegram 發送消息後，Telegram Channel 會將其轉換為 OpenClaw 的標準格式：

```json
{
  "platform": "telegram",
  "channel_id": "telegram_123",
  "user": {
    "id": "user_456",
    "name": "Alice"
  },
  "message": {
    "type": "text",
    "content": "上海明天天氣?",
    "timestamp": "2024-03-09T10:30:00Z"
  }
}
```

#### 步驟 4-5：認證與路由

Gateway 檢查這個消息：
- 來源是否已授權？
- 應該路由到哪個 Workspace？
- 用戶是否有權限？

#### 步驟 6-8：AI 理解與決策

Workspace 準備完整的上下文發送給 LLM：

```
[系統提示]
你是一個個人助理，可以使用以下技能：
- weather: 查詢天氣
- calendar: 管理日程

[對話歷史]
用戶: 你好
助理: 你好！有什麼可以幫你的？

[當前消息]
用戶: 上海明天天氣?
```

#### 步驟 9-12：技能執行

LLM 決定調用 weather skill，Workspace 執行並獲取結果：

```json
{
  "location": "上海",
  "date": "2024-03-10",
  "weather": "晴轉多雲",
  "temperature": "18-26°C",
  "humidity": "60%",
  "wind": "東風 3-4級"
}
```

#### 步驟 13-17：生成回復並返回

LLM 根據天氣數據生成自然語言回復，通過原路返回給用戶。

---

## 核心組件詳解

### Workspace：你的私人辦公室

Workspace（工作空間）是實際處理任務的地方。你可以有多個工作空間，每個負責不同的事情。

**一個典型的 Workspace 配置**：

```yaml
name: "個人助理"
llm:
  provider: "anthropic"
  model: "claude-sonnet-4"
  apiKey: "sk-ant-xxx"

skills:
  - weather
  - calendar
  - email
  - web-search

settings:
  language: "zh-CN"
  temperature: 0.7
  max_tokens: 4000
```

### LLM：AI 的大腦

LLM（Large Language Model，大語言模型）是 OpenClaw 的智能大腦。

| 提供商 | 模型示例 | 特點 | 適用場景 |
|--------|----------|------|----------|
| Anthropic | Claude Sonnet 4 | 平衡、安全、多語言好 | 日常對話、寫作 |
| OpenAI | GPT-4 | 專業、知識廣 | 專業任務、分析 |
| DeepSeek | DeepSeek-V3 | 代碼能力強、便宜 | 編程輔助 |
| 本地部署 | Ollama | 完全私有、免費 | 隱私敏感場景 |

### Channels：連接外部世界

Channels（渠道）是連接各種消息平台的"適配器"。

**每個 Channel 的工作**：
1. 接收消息：從平台獲取用戶消息
2. 格式轉換：統一轉換為 OpenClaw 內部格式
3. 發送回復：把 OpenClaw 的回復發回平台

---

## 技能系統

### 什麼是技能（Skills）？

技能是 OpenClaw 執行特定任務的"能力模組"。如果把 OpenClaw 比作一個人，技能就是這個人學會的各種本領。

### 技能調用的安全機制

OpenClaw 對技能有嚴格的安全控制：

| 權限類型 | 說明 | 示例 |
|----------|------|------|
| `network` | 網絡訪問 | 查天氣、搜尋網頁 |
| `filesystem` | 檔案系統 | 讀寫檔案 |
| `email` | 郵箱訪問 | 發送/接收郵件 |
| `calendar` | 日曆訪問 | 管理日程 |
| `system` | 系統操作 | 執行命令 |

---

## 數據流與狀態管理

### 數據如何存儲？

| 數據類型 | 存儲方式 | 保留時間 | 示例 |
|----------|----------|----------|------|
| 當前會話狀態 | 內存 | 直到會話結束 | 正在進行的對話上下文 |
| 對話歷史 | 本地數據庫 | 可配置（如30天） | 過去的聊天記錄 |
| 用戶配置 | 配置檔案 | 永久 | API密鑰、偏好設置 |
| 技能數據 | 技能自己管理 | 取決於技能 | 日程、郵件草稿 |
| 系統日誌 | 日誌檔案 | 可配置 | 錯誤、調試信息 |

---

## 擴展性與插件生態

### 如何添加新功能？

OpenClaw 的設計允許輕鬆擴展：

1. 從 ClawHub 安裝技能
2. 開發自訂技能
3. 整合第三方 API

---

## 🦞 總結

OpenClaw 的三層架構設計使其既強大又靈活：

- **Channels** 處理外部通信
- **Gateway** 負責認證、路由和日誌
- **Workspace + LLM + Skills** 完成實際任務

理解這個流程有助於故障排查和優化 OpenClaw 的使用體驗。

---

## 下節課預告

> **第 6 課**：OpenClaw 接入微信 — 詳細教學如何將 OpenClaw 連接到微信

---

