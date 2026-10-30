# 新聞資訊上架申請表（BC03）

國立高雄科技大學秘書室公關中心「新聞資訊上架申請表」線上版，依 BC03 新聞稿發佈及新媒體整合應用作業程序（115.10.28）及新聞稿撰寫指引建置。

網址：https://szu1104.github.io/NKUSTPR/

## Repository 內的檔案
- `index.html`：申請表網頁
- `BC03-writing-guide.pdf`：新聞稿撰寫指引（網頁上的下載連結指向此檔名）
- `README.md`：本說明

`nkust-pr-backend.gs` 不放在 repository，它是貼到 Google Apps Script 使用的，裡面不含任何 key。

## 後端設定（照片上傳＋內建高科iAI，bcoffice03 帳號）

1. 以 bcoffice03@nkust.edu.tw 登入 Google Drive，建立資料夾「新聞資訊上架申請_照片」。
   - 右鍵 → 共用，把公關中心同仁加為「編輯者」。
   - 開啟資料夾，複製網址 `drive.google.com/drive/folders/` 後面那一串（資料夾 ID）。
2. 同一帳號前往 https://script.google.com → 新專案，命名「新聞上架申請後端」。
   - 刪除預設內容，貼上 `nkust-pr-backend.gs` 全文。
   - 把 `請貼上根資料夾ID` 換成步驟 1 的資料夾 ID，按儲存。
3. 存入高科iAI API key（key 只存在這裡，不會出現在網頁）：
   - 左側齒輪「專案設定」→ 最下方「指令碼屬性」→「新增指令碼屬性」
   - 屬性：`IAI_KEY`　值：貼上你的高科iAI API key → 儲存
4. 回到編輯器，上方函式選 `testSetup` → 執行 → 依提示授權（出現「Google 尚未驗證這個應用程式」時按「進階」→「前往」）。
   - 執行記錄應依序出現：根資料夾名稱、可用模型、iAI 測試回覆。
   - 若卡在 iAI 測試（逾時或連線錯誤），代表 Google 的伺服器連不到高科iAI（可能只開放校園網路），請洽電算中心。
5. 右上「部署」→「新增部署作業」→ 齒輪選「網頁應用程式」。
   - 執行身分：我（bcoffice03@nkust.edu.tw）；誰可以存取：**任何人** → 部署
   - 複製「網頁應用程式網址」（`https://script.google.com/macros/s/…/exec`）。
6. 打開 `index.html`，找到 `BACKEND_URL: ''`，把網址貼在兩個單引號中間，存檔後上傳到 GitHub 覆蓋。
7. 到申請網頁測試：AI 撰稿不需要再輸入 key；上傳一張照片，確認 Drive 出現「日期_單位_活動名稱」子資料夾。

注意：
- 若步驟 5 沒有「任何人」可選，代表學校 Google Workspace 管理設定不允許，需請電算中心開放。
- 之後修改程式要沿用同一個網址：部署 → 管理部署作業 → 鉛筆圖示 → 版本選「新版本」→ 部署。
- 更換 iAI key 只要改指令碼屬性 `IAI_KEY`，不用重新部署。
- 全站 AI 每日上限 300 次（程式內 `AI_DAILY_LIMIT` 可調整），避免額度被耗盡。
- 照片會佔用 bcoffice03 的雲端空間，請定期整理。

## 修改規則
期限天數、收件人、圖說字數、照片張數與大小上限，集中在 `index.html` 的 `CONFIG` 區塊。

## 高科iAI
後端設定完成後，AI 功能使用指令碼屬性中的 key，申請人只需在「AI 設定」選擇模型。後端未設定時，申請人需自行貼上 API key（網址與模型已預設為 `https://www.iai.nkust.edu.tw/aihub/v1`、`Furen-large`）。
