# 第 4 課：OpenClaw 配置目錄詳解

> **課程難度**：⭐⭐⭐ 中級
> **預計學習時間**：60 分鐘
> **來源**：菜鳥教程 OpenClaw 配置目錄

---

## 目錄結構總覽

OpenClaw 的配置和數據主要存儲在 `~/.openclaw/` 目錄下。讓我們詳細了解每個目錄的作用。

---

## 核心配置目錄

### 1. 主配置文件

**路徑**：`~/.openclaw/openclaw.json`

這是 OpenClaw 的核心配置文件，包含所有系統級設置。

```json
{
  "gateway": {
    "mode": "local",
    "port": 18789,
    "bind": "127.0.0.1",
    "token": "c9917c5a066beeb26266d09baed99495e7563b33c771e89a"
  },
  "models": {
    "default": "claude-sonnet-4"
  }
}
```

**主要配置項**：
- `gateway` - 網關服務配置
- `models` - AI 模型配置
- `messages` - 消息處理配置

> 💡 首次安裝後通過 `openclaw onboard` 向導自動生成。

### 2. 工作區目錄

**路徑**：`~/.openclaw/workspace/`

這是 OpenClaw 的預設工作目錄，所有 AI 生成的檔案、臨時檔案和用戶請求的輸出檔案都保存在此。

**主要用途**：
- AI 智能體讀寫檔案的預設位置
- 代碼執行輸出存儲
- 文檔生成和編輯
- 臨時數據存儲

### 3. 智能體狀態目錄

**路徑**：`~/.openclaw/agents/<cid>/`

每個會話的智能體狀態和配置存儲目錄。

```
~/.openclaw/agents/<cid>/
├── agent/
│   ├── auth-profiles.json    # 該會話的 OAuth 和 API 密鑰
│   └── ...
```

### 4. 認證憑證目錄（舊版）

**路徑**：`~/.openclaw/credentials/`

舊版本 OpenClaw 的憑證存儲位置。

> ⚠️ 新版本已遷移至 `~/.openclaw/agents/<agentId>/agent/auth-profiles.json`

### 5. 記憶存儲目錄

**路徑**：`~/.openclaw/memory/`

OpenClaw 的持久化記憶系統存儲位置。

**主要檔案**：
- `<cid>.sqlite` - 向量索引數據庫
- `YYYY-MM-DD.md` - 每日對話日誌

**記憶功能**：
- 向量搜尋：使用 `memory search "關鍵詞"` 搜尋歷史對話
- 上下文關聯：支援跨會話的上下文理解
- 長期記憶：智能體會"記住"用戶的偏好和習慣

### 6. 技能目錄

**路徑**：`~/.openclaw/skills/`

全局共享技能（Skills）的安裝位置。

```
~/.openclaw/skills/
├── filesystem-mcp/
├── github/
├── weather/
└── ...
```

**技能管理**：
```bash
# 安裝技能
npx clawhub install <skill-name>

# 列出技能
openclaw skills list

# 搜尋技能
npx clawhub search <關鍵詞>
```

### 7. 網關日誌目錄

**路徑**：`/tmp/openclaw/*.log`

網關服務的運行日誌，存儲在系統臨時目錄。

**日誌管理**：
```bash
# 查看詳細日誌
openclaw gateway --verbose
```

---

## 重要的配置檔案

### USER.md

**說明**：用戶信息檔案，包含關於用戶的個性化信息，幫助 AI 更好地理解用戶需求。

**內容示例**：
- 用戶偏好設置
- 常用工作流程
- 項目背景信息
- 自定義指令

### SOUL.md 系列

| 檔案 | 說明 |
|------|------|
| `SOUL.md` | AI 人格/語氣設定 |
| `USER.md` | 你的個人偏好和背景 |
| `MEMORY.md` | 長期記憶記錄 |
| `AGENTS.md` | 指令說明 |
| `IDENTITY.md` | 名稱/主題 |
| `BOOT.md` | 啟動配置 |
| `HEARTBEAT.md` | 定期檢查清單 |

---

## 配置檔案管理最佳實踐

### 1. 備份策略

```bash
# 備份整個配置目錄
tar -czf openclaw-backup-$(date +%Y%m%d).tar.gz ~/.openclaw/

# 僅備份核心配置
cp ~/.openclaw/openclaw.json ~/backups/
cp -r ~/.openclaw/memory/ ~/backups/memory-backup/
```

### 2. 安全建議

```bash
# 確保配置目錄僅用戶可訪問
chmod 700 ~/.openclaw/
chmod 600 ~/.openclaw/openclaw.json
chmod 600 ~/.openclaw/agents/*/agent/auth-profiles.json
```

> ⚠️ `openclaw.json` 包含網關 token，`auth-profiles.json` 包含 API 密鑰，需妥善保護。

### 3. 遷移和升級

**版本升級注意事項**：
- 升級前備份整個 `~/.openclaw/` 目錄
- 檢查 release notes 了解配置變更
- 舊版本憑證可能需要遷移

### 4. 故障排查

```bash
# 檢查配置文件語法
cat ~/.openclaw/openclaw.json | json_pp

# 深度檢查
openclaw doctor --deep

# 查看網關狀態
openclaw gateway status
```

---

## 環境變量配置

OpenClaw 支援通過環境變量進行配置：

```bash
# API 密鑰環境變量
export ANTHROPIC_API_KEY="your-key-here"
export OPENAI_API_KEY="your-key-here"
export DEEPSEEK_API_KEY="your-key-here"

# 自定義配置目錄
export OPENCLAW_HOME="~/custom-path/.openclaw"
```

---

## 網絡和部署配置

### 本地部署

- 綁定地址：`127.0.0.1`（僅本機訪問）
- 網關端口：`18789`
- 存取方式：`http://127.0.0.1:18789/#token=<your-token>`

### 雲端部署

支援平台：
- 阿里雲
- 騰訊雲
- 1Panel
- Docker 容器

---

## 🦞 總結

理解 OpenClaw 的目錄結構對於故障排查、定製化和安全管理至關重要。

**核心目錄**：
| 目錄 | 用途 |
|------|------|
| `~/.openclaw/` | 主配置目錄 |
| `~/.openclaw/workspace/` | 工作區 |
| `~/.openclaw/memory/` | 記憶存儲 |
| `~/.openclaw/skills/` | 技能 |
| `/tmp/openclaw/*.log` | 日誌 |

---

## 下節課預告

> **第 5 課**：OpenClaw 工作原理 — 深入了解 OpenClaw 的內部架構和工作流程

---

*本課程內容整理自[菜鳥教程 OpenClaw 配置目錄](https://www.runoob.com/ai-agent/openclaw-setup.html)，版權歸原作者所有。*
