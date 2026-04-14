# 第 8 課：OpenClaw Skills 使用指南

> **課程難度**：⭐⭐⭐ 中級
> **預計學習時間**：60 分鐘
> **來源**：菜鳥教程 OpenClaw Skills

---

## 技能系統簡介

![Skills截圖](https://www.runoob.com/wp-content/uploads/2026/03/openclaw-skills-runoob-1.png)

技能（Skills）是 OpenClaw 執行特定任務的"能力模組"。如果把 OpenClaw 比作一個人，技能就是這個人學會的各種本領。

---

## 安裝 ClawHub CLI

```bash
# 使用 npm 安裝
npm i -g clawhub

# 或使用 pnpm
pnpm add -g clawhub
```

### 國內鏡像

國內鏡像地址：`https://skillhub.tencent.com/`

使用這個安裝速度更快：

```bash
curl -fsSL https://skillhub-1388575217.cos.ap-guangzhou.myqcloud.com/install/install.sh | bash
```

---

## 安裝技能

### 基本安裝

```bash
# 安裝單個技能
clawhub install <skill-name>

# 搜索技能
clawhub search "關鍵詞"
```

### 批量安裝

```bash
# 批量更新全部
clawhub update --all
```

---

## 推薦新手安裝的 Skills

![ClawHub截圖](https://www.runoob.com/wp-content/uploads/2026/03/runoob-clawhub-scaled.png)

### 安裝順序建議

1. 先安裝 Skill Vetter 保底安全
2. 再安裝 self-improving-agent 或其變種，讓 AI 開始長記性
3. 根據需求補 Summarize / Agent Browser / Gog / Github / Multi Search Engine 這幾個萬金油

### 批量安裝命令

```bash
clawhub install self-improving-agent
clawhub install summarize
clawhub install agent-browser
clawhub install skill-vetter
clawhub install github
```

---

## 常用 Skills 列表

![Skills列表](https://www.runoob.com/wp-content/uploads/2026/03/openclaw-skills-runoob-2.png)

| # | Skill | 說明 | 適用場景 | 安裝命令 |
|---|-------|------|----------|----------|
| 1 | self-improving-agent | 記錄失敗與糾正並複盤優化 | 失敗複盤 / 多次出錯 / 用戶糾正 | `clawhub install self-improving-agent` |
| 2 | summarize | 多格式內容總結（網頁/PDF/視頻等） | 長文閱讀 / 文檔提煉 | `clawhub install summarize` |
| 3 | agent-browser | 自動瀏覽器操作（點/輸/抓） | 爬取 / 表單 / 自動化 | `clawhub install agent-browser` |
| 4 | skill-vetter | 安裝前安全檢測 | 檢測權限 / 風險插件 | `clawhub install skill-vetter` |
| 5 | github | 通過 gh 操作 GitHub | PR / Issue / CI | `clawhub install github` |
| 6 | gog | Google Workspace 集成 | 郵件 / 文檔 / 表格 | `clawhub install gog` |
| 7 | ontology | 結構化知識圖譜記憶 | 項目 / 多任務管理 | `clawhub install ontology` |
| 8 | proactive-agent | 主動執行與調度 | 定時任務 / 自動執行 | `clawhub install proactive-agent` |
| 9 | multi-search-engine | 多引擎搜索聚合 | 調研 / 對比 | `clawhub install multi-search-engine` |
| 10 | humanizer | 優化文本更自然 | 文案 / 潤色 | `clawhub install humanizer` |
| 11 | nano-pdf | 自然語言編輯 PDF | 合同 / 文檔修改 | `clawhub install nano-pdf` |
| 12 | notion | 管理頁面與數據庫 | 筆記 / 知識庫 | `clawhub install notion` |
| 13 | obsidian | Markdown 筆記自動化 | 整理 / 沉澱 | `clawhub install obsidian` |
| 14 | api-gateway | 連接 100+ API | 系統集成 | `clawhub install api-gateway` |
| 15 | automation-workflows | 設計執行自動化流程 | 副業 / 自動化 | `clawhub install automation-workflows` |
| 16 | auto-updater | 自動更新 Skills | 長期運行 | `clawhub install auto-updater` |
| 17 | openai-whisper | 本地語音轉文字 | 會議記錄 | `clawhub install openai-whisper` |
| 18 | nano-banana-pro | 圖像生成與編輯 | 海報 / 圖片 | `clawhub install nano-banana-pro` |
| 19 | stock-analysis | 股票與加密分析 | 趨勢 / 分析 | `clawhub install stock-analysis` |
| 20 | weather | 天氣查詢與預測 | 日常查詢 | `clawhub install weather` |

---

## 自訂義技能

### 最簡單的 SKILL.md 示例

```markdown
---
name: my-skill
description: Does a thing with an API.
---

# My Skill

## Rules
- Always confirm with the user before making destructive changes.
- Use the credentials from environment variable MY_API_KEY.

## Usage

When the user asks to "do the thing", call the API endpoint at
https://api.example.com/action with the provided payload.
```

### 發布技能

寫好後，執行發布命令：

```bash
clawhub publish ~/.openclaw/skills/my-skill \
  --slug my-skill \
  --name "My Skill" \
  --version 1.0.0 \
  --tags latest
```

> ⚠️ 發布需要一個至少註冊滿一周的 GitHub 帳號。`--slug` 是 Skill 在 ClawHub 上的唯一標識符。

---

## 技能權限和安全

### 權限類型

| 權限 | 說明 |
|------|------|
| `network` | 網絡訪問（查天氣、搜尋網頁） |
| `filesystem` | 檔案系統（讀寫檔案） |
| `email` | 郵箱訪問（發送/接收郵件） |
| `calendar` | 日曆訪問（管理日程） |
| `system` | 系統操作（執行命令） |

### 安全建議

- 安裝前使用 `skill-vetter` 檢測風險
- 不要安裝來源不明的技能
- 定期檢查已安裝技能的權限

---

## 🦞 總結

Skills 系統是 OpenClaw 的核心擴展機制，讓 AI 可以執行各種專業任務。

**快速入門**：
1. 安裝 `clawhub` CLI
2. 安裝 `skill-vetter` 保障安全
3. 安裝 `self-improving-agent` 讓 AI 持續改進
4. 根據需求添加其他技能

---

