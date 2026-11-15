# RenewHelper 繁體中文版

此版本新增繁體中文（台灣）介面，並讓新設定預設使用繁體中文。繁簡轉換採用 OpenCC 的台灣詞彙模式；原有資料、設定格式與 `RENEW_KV` 綁定維持相容。既有設定中已儲存的語言偏好會保留，可從右上角語言按鈕切換。

## 本機建置

需要 Node.js。於專案根目錄執行：

```bash
npm install
npm run build
```

建置完成後，根目錄的 `_worker.js` 會包含最新介面與後端。建置腳本會自動增加版本號。

## 部署到 Cloudflare

### 手動更新現有 Worker

1. 在 Cloudflare Dashboard 開啟 `renewhelper2`。
2. 先完成上述建置。
3. 將根目錄 `_worker.js` 的完整內容放入 Worker 編輯器的 `worker.js`，再按 Deploy。
4. 確認原本的 KV Namespace 綁定仍使用變數名稱 `RENEW_KV`，並選擇原有的命名空間。保留原有登入密碼與 Cron Trigger。

### 使用 GitHub Actions

此 Fork 的部署工作流程會先執行建置，再部署到 `renewhelper2`。在 GitHub 儲存庫的 Actions secrets 設定 `CF_API_TOKEN`、`CF_ACCOUNT_ID`、`CF_KV_ID` 與 `AUTH_PASSWORD`。`CF_KV_ID` 必須指向目前 Worker 正在使用的 KV 命名空間。

## 切換語言

登入後使用右上角的語言按鈕循環切換簡體中文、繁體中文與英文。所選語言會保存在系統設定中。
