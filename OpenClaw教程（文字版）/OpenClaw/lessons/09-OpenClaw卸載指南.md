# 第 9 課：OpenClaw 卸載指南

> **課程難度**：⭐ 入門
> **預計學習時間**：20 分鐘
> **來源**：菜鳥教程 OpenClaw 卸載指南

---

## 卸載方式選擇

OpenClaw 提供了多種卸載方式，根據你的安裝方式選擇對應的卸載步驟。

---

## 推薦卸載方式（適用大多數用戶）

### 步驟一：卸載 CLI

根據安裝方式選擇對應命令：

```bash
# npm 安裝
npm rm -g openclaw

# pnpm 安裝
pnpm remove -g openclaw

# bun 安裝
bun remove -g openclaw
```

### 步驟二：卸載 Gateway 服務

```bash
# 停止並卸載服務
openclaw uninstall
```

### 步驟三：清理配置目錄

```bash
# 刪除配置目錄
rm -rf ~/.openclaw/
```

> ⚠️ 這會刪除所有配置、記憶和技能數據，如有需要請提前備份。

### 步驟四：清理殘留檔案

檢查並刪除以下可能殘留的目錄：

```bash
# 主配置目錄
rm -rf ~/.openclaw

# 工作區目錄
rm -rf ~/.openclaw/workspace

# macOS Launch Agents
rm -f ~/Library/LaunchAgents/bot.molt.gateway.plist
rm -f ~/Library/LaunchAgents/ai.openclaw.gateway.plist

# Linux systemd 用戶服務
rm -f ~/.config/systemd/user/openclaw-gateway.service
```

---

## 手動清理（進階用戶）

### macOS（launchd 服務）

```bash
# 停止並卸載服務
launchctl bootout gui/$UID/bot.molt.gateway

# 刪除服務配置文件
rm -f ~/Library/LaunchAgents/bot.molt.gateway.plist

# 多配置場景
launchctl bootout gui/$UID/bot.molt.<profile>
rm -f ~/Library/LaunchAgents/bot.molt.<profile>.plist
```

### Linux（systemd 用戶服務）

```bash
# 停止並禁用服務
systemctl --user disable --now openclaw-gateway.service

# 刪除服務配置文件
rm -f ~/.config/systemd/user/openclaw-gateway.service

# 刷新 systemd 配置
systemctl --user daemon-reload
```

### Windows（計劃任務）

```bash
# 刪除計劃任務
schtasks /Delete /F /TN "OpenClaw Gateway"

# 刪除任務腳本
Remove-Item -Force "$env:USERPROFILE\.openclaw\gateway.cmd"
```

---

## Docker 安裝的卸載方式

如果 OpenClaw 運行在 Docker 中：

```bash
docker stop openclaw
docker rm openclaw
docker volume rm openclaw-data
```

或使用 docker-compose：

```bash
docker-compose down -v
```

---

## 源碼安裝卸載

若通過 `git clone` 源碼方式安裝：

```bash
# 1. 先停止並卸載網關服務
openclaw uninstall

# 2. 刪除源碼倉庫目錄
rm -rf /path/to/openclaw-repo

# 3. 按前文步驟刪除狀態、配置與工作區目錄
```

---

## 卸載前建議備份

如果需要保留數據，可以先創建備份：

```bash
# 創建備份
openclaw backup create

# 或手動備份關鍵目錄
cp -r ~/.openclaw ~/backups/openclaw-backup-$(date +%Y%m%d)
```

---

## 卸載驗證

卸載完成後，可通過以下方式驗證是否徹底清理：

```bash
# 執行版本命令，提示「命令未找到」則 CLI 卸載成功
openclaw --version

# 檢查系統服務
# macOS
launchctl list | grep molt

# Linux
systemctl --user list-units | grep openclaw

# 檢查目錄
ls ~/.openclaw  # 應該提示不存在
```

---

## 常見殘留目錄

徹底卸載時建議檢查以下目錄：

| 目錄 | 說明 |
|------|------|
| `~/.openclaw` | 主配置目錄 |
| `~/.openclaw/workspace` | 工作區 |
| `~/Library/LaunchAgents/bot.molt.gateway.plist` | macOS 服務 |
| `~/.config/systemd/user/openclaw-gateway.service` | Linux 服務 |

---

## 🦞 總結

卸載 OpenClaw 的核心步驟：

1. **卸載 CLI**：`npm rm -g openclaw`
2. **卸載服務**：`openclaw uninstall`
3. **清理配置**：`rm -rf ~/.openclaw/`
4. **驗證清理**：確認目錄和服務已刪除

---

## 🎓 系列課程總結

恭喜！你已完成 OpenClaw 全系列課程：

| # | 課程 | 狀態 |
|---|------|------|
| 1 | OpenClaw 是什麼？快速上手 | ✅ |
| 2 | OpenClaw 快速上手 | ✅ |
| 3 | OpenClaw 一鍵部署 | ✅ |
| 4 | OpenClaw 配置目錄詳解 | ✅ |
| 5 | OpenClaw 工作原理 | ✅ |
| 6 | OpenClaw 接入微信 | ✅ |
| 7 | OpenClaw 接入飛書 | ✅ |
| 8 | OpenClaw Skills 使用指南 | ✅ |
| 9 | OpenClaw 卸載指南 | ✅ |

---

