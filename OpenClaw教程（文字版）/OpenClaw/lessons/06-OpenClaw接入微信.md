# 第 6 課：OpenClaw 接入微信

> **課程難度**：⭐⭐⭐ 中級
> **預計學習時間**：45 分鐘
> **來源**：菜鳥教程 OpenClaw 接入微信

---

## 前置準備

![微信接入截圖](https://www.runoob.com/wp-content/uploads/2026/03/c026e_69bf6427b575d_69.png)

在開始之前，你需要準備：

1. 已安裝 OpenClaw
2. 一個微信公眾號或個人微信（需使用特殊插件）
3. 基本的命令行操作能力

---

## 安裝微信插件

### 使用騰訊雲市場插件

騰訊雲市場提供了一鍵安裝的 OpenClaw 微信插件。

### 手動安裝插件

```bash
# 安裝微信插件
openclaw plugins install "@tencent-weixin/openclaw-weixin"
```

### 插件工作原理

微信插件通過以下方式連接：

```
微信消息 → 插件接收 → Gateway → AI 處理 → Gateway → 插件發送 → 微信
```

---

## 配置微信渠道

### 1. 獲取微信 API 憑證

你需要從微信公眾平台獲取：
- AppID
- AppSecret
- Token
- EncodingAESKey

### 2. 在 openclaw.json 中配置

```json
{
  "channels": {
    "weixin": {
      "enabled": true,
      "appId": "your-app-id",
      "appSecret": "your-app-secret",
      "token": "your-token",
      "encodingAESKey": "your-aes-key"
    }
  }
}
```

### 3. 重啟網關

```bash
openclaw gateway restart
```

---

## 接入模式選擇

### 訂閱號（公眾平台）

適合有公眾號的用戶：
- 每天可發送消息
- 支援自動回覆
- 支援自定義選單

### 個人微信（Hook 模式）

⚠️ 個人微信接入需要使用 Hook 技術，可能違反微信服務條款，請謹慎使用。

---

## 測試連接

### 發送測試消息

在微信中向你的機器人發送：

```
@機器人 你好
```

### 檢查日志

```bash
# 查看網關日志
openclaw logs

# 查看微信插件日志
tail -f /tmp/openclaw/weixin.log
```

---

## 常見問題

| 問題 | 解決方案 |
|------|----------|
| 消息無回覆 | 檢查插件是否正確安裝 |
| 認證失敗 | 確認 AppID 和 AppSecret 正確 |
| 連接超時 | 檢查網絡防火牆設置 |

---

## 安全性注意事項

> ⚠️ 微信接入涉及個人隱私和商業秘密，請確保：
> - Token 和 AES Key 不要洩露
> - 定期更換 API 憑證
> - 設置適當的訪問權限

---

## 🦞 總結

微信接入讓 OpenClaw 可以通過微信與用戶互動。

**核心步驟**：
1. 安裝微信插件
2. 配置 API 憑證
3. 重啟網關生效
4. 測試連接

---

## 下節課預告

> **第 7 課**：OpenClaw 接入飛書 — 詳細教學如何將 OpenClaw 連接到飛書

---

