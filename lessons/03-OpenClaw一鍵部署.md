# 第 3 課：OpenClaw 一鍵部署

> **課程難度**：⭐⭐ 中級
> **預計學習時間**：45 分鐘
> **來源**：菜鳥教程 OpenClaw 一鍵部署

---

## 部署方式選擇

![一鍵部署截圖](https://www.runoob.com/wp-content/uploads/2026/02/79aa72e4-4b49-46c5-a804-c879c604d348.png)

OpenClaw 支援多種部署方式，本課程介紹如何使用雲伺服器一鍵部署。

---

## 阿里雲部署

### 購買伺服器

套餐已經包含了伺服器與大模型。我們可以使用它們的鏡像，一鍵安裝。

![阿里雲部署](https://www.runoob.com/wp-content/uploads/2026/02/ab4d1d52-43f3-4525-9728-6ae85ee7a304.png)

購買完成後就可以到控制台配置 OpenClaw。

### 配置 OpenClaw

OpenClaw 執行過程中預設調用百煉模型，模型呼叫的主要計費方式有兩種：

#### 方案一：Coding Plan AI 編碼套餐（推薦）

採用固定月費模式，提供月度請求額度，超出時段限額的調用會報錯且不計費用。

支援模型：
- qwen3.5-plus
- kimi-k2.5
- MiniMax-M2.5
- glm-5

#### 方案二：按 Token 用量計費

OpenClaw 2026.2.26 版本預設使用 qwen3.5-plus 模型作為文本和圖像處理模型。

### 開通百煉模型

1. 訪問 [百煉模型服務平台](https://bailian.console.aliyun.com/)
2. 點擊右上角登入
3. 點擊右上角的齒輪⚙️圖標 → 選擇 API key
4. 複製 API key，如果沒有也可以建立 API key

> ⚠️ 開通阿里雲百煉不會產生費用，僅模型調用、模型部署、模型調優會產生相應計費。

### 購買優惠套餐

![優惠套餐](https://www.runoob.com/wp-content/uploads/2026/02/7fdb80c6-7af8-4cb0-8757-638a88cfefe6.png)

OpenClaw 還是比較消耗 token 的，如果要長期使用，建議先購買個最便宜的包：

- [阿里雲百煉大模型服務平台](https://www.aliyun.com/benefit/scene/codingplan)
- [Coding Plan 套餐](https://www.aliyun.com/benefit/scene/codingplan)
- [備用購買連結](https://cn.aliyun.com/benefit?from_alibabacloud=&userCode=i5mn5r7m)

### 配置專屬 API Key

購買完 Coding Plan 套餐，可以在 Coding Plan 頁面，獲取 Coding Plan 專屬 API Key（格式為 `sk-sp-xxxxx`）。

### 配置 Base URL

後續需在 AI 工具中配置以下其中一個 Base URL：

| 協議類型 | Base URL |
|---------|----------|
| OpenAI 兼容協議（OpenClaw 可使用） | `https://coding.dashscope.aliyuncs.com/v1` |
| Anthropic 兼容協議 | `https://coding.dashscope.aliyuncs.com/apps/anthropic` |

> ⚠️ Coding Plan 專屬的 API Key 和 Base URL 與百煉按量計費的不互通，請勿混用。

---

## 騰訊雲部署

騰訊雲同樣支援一鍵部署 OpenClaw。

詳情參考：[騰訊雲部署教程](https://cloud.tencent.com/act/cps/redirect?redirect=37925&cps_key=4537fb0f9e70f157220dafdec0f9c750&from=console)

---

## 伺服器配置

在伺服器頁面，單擊伺服器卡片中的實例 ID，進入伺服器概覽頁面。

### 單擊應用詳情頁簽

![應用詳情](https://www.runoob.com/wp-content/uploads/2026/02/53ea9fb0-d4ea-4582-a16f-38e7d6906880.png)

配置 OpenClaw。

### 端口放通

需要放通對應端口的防火牆，單擊一鍵放通即可。

### 配置 OpenClaw

單擊執行命令，輸入百煉的 API-Key，單擊下一步。

### 存取控制頁面

單擊執行命令可獲取 Clawdbot 對話的地址。

### 查看 Token

在幫助 → Token配置中單擊執行命令，獲取 Token。

### 開啟 ResponseAPI 訪問

後續 AppFlow 會通過 API 訪問 OpenClaw。

---

## 配置 OpenClaw 渠道

在 Clawdbot 頁面左側導航欄，單擊 Setting → Config。

在 Config 頁面左側導航欄單擊 Gateway，切換至 Http 頁簽，在 Responses 區域將 Enabled 切換至開啟，單擊 Save。

---

## （可選）配置聯網搜尋功能

目前中國內地地域（除香港）暫不支援聯網搜尋。香港和海外地域若需使用聯網功能，可參考 OpenClaw 官網配置。

---

## 🦞 總結

一鍵部署讓 OpenClaw 的安裝變得極其簡單，無需手動配置伺服器環境。

**核心步驟**：
1. 購買帶 OpenClaw 鏡像的伺服器
2. 配置 API Key
3. 一鍵部署完成

---

## 下節課預告

> **第 4 課**：OpenClaw 配置目錄詳解 — 深入了解配置文件的結構和作用

---

*本課程內容整理自[菜鳥教程 OpenClaw 一鍵部署](https://www.runoob.com/ai-agent/openclaw-cloud.html)，版權歸原作者所有。*
