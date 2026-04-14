# 第 7 課：OpenClaw 接入飛書

> **課程難度**：⭐⭐⭐ 中級
> **預計學習時間**：60 分鐘
> **來源**：菜鳥教程 OpenClaw 接入飛書

---

## 前置準備

![飛書接入截圖](https://www.runoob.com/wp-content/uploads/2026/03/d2db3e7d-b9e2-4f8e-927a-a9cf8e852c8c.png)

在開始之前，你需要：

1. 已安裝 OpenClaw
2. 一個飛書開發者帳號
3. 一個飛書應用

---

## 創建飛書應用

### 1. 進入飛書開放平台

訪問 [飛書開放平台](https://open.feishu.cn/)，創建一個新應用。

### 2. 獲取應用憑證

在應用詳情頁，獲取：
- App ID
- App Secret

---

## 配置權限

### 添加應用能力

在左側菜單 → 添加應用能力 → 機器人，點擊"添加"按鈕，開啟機器人能力。

### 配置權限

左側 → 權限管理 → 批量導入/導出權限：

粘貼以下 JSON：

```json
{
  "scopes": {
    "tenant": [
      "aily:file:read",
      "aily:file:write",
      "application:application.app_message_stats.overview:readonly",
      "application:application:self_manage",
      "application:bot.menu:write",
      "cardkit:card:read",
      "cardkit:card:write",
      "contact:user.employee_id:readonly",
      "corehr:file:download",
      "event:ip_list",
      "im:chat.access_event.bot_p2p_chat:read",
      "im:chat.members:bot_access",
      "im:message",
      "im:message.group_at_msg:readonly",
      "im:message.p2p_msg:readonly",
      "im:message:readonly",
      "im:message:send_as_bot",
      "im:resource"
    ],
    "user": ["aily:file:read", "aily:file:write", "im:chat.access_event.bot_p2p_chat:read"]
  }
}
```

---

## 配置事件訂閱

### 添加事件

在左側菜單選擇事件與回調 → 事件配置：

1. 訂閱方式使用長連接接收事件（WebSocket），然後保存
2. 添加以下事件：
   - `im.message.receive_v1` - 接收消息
   - `im.message.message_read_v1` - 消息已讀回執
   - `im.chat.member.bot.added_v1` - 機器人進群
   - `im.chat.member.bot.deleted_v1` - 機器人被移出群

---

## 發布應用

### 創建版本

左側 → 版本管理與發布 → 創建版本 → 提交審核 → 發布。

---

## 配置 OpenClaw

### 群聊策略選擇

接下來的群聊策略選擇 Open，這樣可以響應所有的群聊：

- 如果選擇 Allowlist，只會在白名單的群聊可以響應
- 選擇往後，回到菜單選擇 Finished

![群聊策略](https://www.runoob.com/wp-content/uploads/2026/03/e3245f89-0e1d-40ec-8af5-fd40b6489d54.png)

### 查看頻道選項

回到網頁端，查看頻道選項，可以看到飛書已經啟用。

---

## 啟動並測試

### 啟動 OpenClaw

```bash
openclaw gateway
# 或
openclaw gateway --port 18789
```

### 創建測試群

使用飛書創建一個測試群，在群組的設置中添加我們剛才創建的機器人。

### 測試對話

接下來我們就可以和 OpenClaw 開始聊天，可以 @ 它讓它介紹下自己，正常回覆說明流程跑通了。

---

## 常用技能配置

![飛書配置截圖](https://www.runoob.com/wp-content/uploads/2026/03/5661b9b0-93a9-48b2-97ea-7f4c7614ea70.png)

### 開啟機器人能力

確保在飛書應用中開啟了機器人能力。

### 配置權限清單

![權限配置](https://www.runoob.com/wp-content/uploads/2026/03/b578b9ef-2e2b-4316-b78c-1c5dddf9bf1d.png)

---

## 常見問題

| 問題 | 解決方案 |
|------|----------|
| 無法接收消息 | 檢查事件訂閱是否正確配置 |
| 權限不足 | 確認已添加所有必要權限 |
| 發布失敗 | 檢查應用審核狀態 |

---

## 🦞 總結

飛書接入讓 OpenClaw 可以通過飛書與團隊成員互動。

**核心步驟**：
1. 創建飛書應用並獲取憑證
2. 配置機器人能力和權限
3. 設置事件訂閱
4. 發布應用並測試

---

## 下節課預告

> **第 8 課**：OpenClaw Skills 使用指南 — 學習如何使用和創建技能

---

