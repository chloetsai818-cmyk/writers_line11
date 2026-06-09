# 作家群組聊天 — 部署說明

## 檔案結構

```
writer-chat-deploy/
├── index.html       ← 主網站（所有前端邏輯）
├── api/
│   └── chat.js      ← Vercel serverless function（呼叫 Anthropic API）
├── vercel.json      ← Vercel 設定
└── README.md
```

---

## 部署步驟

### Step 1：申請帳號

- [github.com](https://github.com) — 存放程式碼（免費）
- [vercel.com](https://vercel.com) — 部署網站（免費）
- [console.anthropic.com](https://console.anthropic.com) — 取得 API Key

### Step 2：取得 Anthropic API Key

1. 登入 [console.anthropic.com](https://console.anthropic.com)
2. 點選左側 **API Keys**
3. 點 **Create Key**，複製 `sk-ant-...` 開頭的金鑰
4. 先存到記事本備用

### Step 3：上傳到 GitHub

1. 登入 GitHub，點右上角 **+** → **New repository**
2. 名稱填 `writer-chat`，選 **Public**，按 **Create repository**
3. 把這個資料夾裡的所有檔案上傳：
   - 點 **uploading an existing file**
   - 把 `index.html`、`vercel.json`、`api/chat.js` 拖進去
   - 注意：`api/chat.js` 要放在 `api/` 資料夾內
   - 按 **Commit changes**

### Step 4：連結 Vercel

1. 登入 [vercel.com](https://vercel.com)
2. 點 **Add New** → **Project**
3. 選 **Import Git Repository**，選你剛建的 `writer-chat`
4. 按 **Import**

### Step 5：設定 API Key（重要！）

在 Vercel 部署設定頁：
1. 找到 **Environment Variables**
2. 填入：
   - **Name**: `ANTHROPIC_API_KEY`
   - **Value**: 貼上你的 `sk-ant-...` 金鑰
3. 按 **Add**
4. 按 **Deploy**

### Step 6：完成！

部署完成後 Vercel 會給你一個網址，例如：
`https://writer-chat-xxx.vercel.app`

分享這個網址給任何人就能使用。

---

## 注意事項

- API Key 只存在 Vercel 的環境變數，不會出現在程式碼裡
- 免費的 Vercel 方案完全夠用（每月 100GB 頻寬）
- Anthropic API 按使用量計費，每次對話約 $0.001–0.003 USD
- 如果想關閉網站，在 Vercel dashboard 刪除 project 即可
