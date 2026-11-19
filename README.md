# 🇹🇼 台灣旅行共同記帳：獨立靜態網站

**不使用 Google Sheet。** 網站只讀取同一資料夾的 `data.json`。

## 正式發布到 GitHub Pages

1. 連接 ChatGPT 的 GitHub 插件，授權建立和更新一個 repository。
2. 將這個資料夾的 `index.html`、`data.json` 和 `.nojekyll` 提交到 repository 根目錄。
3. Repo Settings → Pages → Source: Deploy from a branch → Branch: `main` → `/(root)`。
4. GitHub Pages 會產生 `https://<username>.github.io/<repository>/` 網址（必須以實際帳號和 repo 名稱為準）。
5. 將網站網址傳給旅伴；他們只讀，刷新後讀取最新 `data.json`。

## 更新流程

- 你在同一個 ChatGPT 對話輸入一筆費用和參與者。
- 當 GitHub 插件連接且具寫入 repo 權限，我們可以將新紀錄 `commit/push` 到 `data.json`。
- GitHub Pages 更新部署後，朋友刷新網站便可看見（可能有短暫部署及 CDN 延遲）。
- 若 ChatGPT 只回覆文字，沒有成功推送 GitHub，網站不會更新。每次應確認 commit 成功。

## 資料格式

- `amountCents` 是新台幣**分**，例如 NT$229 → 22900，避免小數浮點誤差。
- `expenses` 記錄每筆消費，`participants` 各人按一份分攤。
- `settlements` 記錄旅伴之間的結算付款，不代表誰代墊原始消費。
- LamEC 與 Carrie 各佔一個分攤份額，但顯示為 `LamEC + Carrie` 同一結算帳戶。
- 每筆分攤尾數按 travelers 固定排序分配，逐筆總額保持一致。
- 支出新增後，即使 LamEC + Carrie 曾經付清，新支出仍會產生新的差額，直到再次付清。

## 資料保護

GitHub Pages 公開網站任何知道連結的人都能查看網站資料（公開 repo 也可被搜尋）。目前不應放銀行帳戶、護照或敏感個資。

## 本機測試

在網站資料夾執行 `python -m http.server 8000`，打開 http://localhost:8000。直接用 `file://` 開啟會觸發離線預覽（瀏覽器通常不讓檔案讀取本地 JSON）。
