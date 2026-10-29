# 新聞資訊上架申請表（BC03）

國立高雄科技大學秘書室公關中心「新聞資訊上架申請表」線上版，依 BC03 新聞稿發佈及新媒體整合應用作業程序（115.10.28）及新聞稿撰寫指引建置。

## 檔案
- `index.html`：申請表網頁（放在 GitHub Pages）
- `apps-script.gs`：送出後依類別分流寄信、寄確認信、寫入試算表（放在 Google Apps Script）

## 上線步驟
1. 把 `index.html` 放到 GitHub repo 根目錄，Settings → Pages → Branch 選 `main` / root，存檔。
2. 尚未設定 Apps Script 前，送出按鈕會改為「下載填妥的申請表（Word）＋開啟郵件」，可先試用。
3. 依 `apps-script.gs` 檔頭說明部署，取得網址後填入 `index.html` 的 `CONFIG.SUBMIT_URL`，即改為一鍵送出。

## 修改規則
期限天數、收件人、圖說字數、照片張數集中在 `index.html` 的 `CONFIG` 區塊；收件人也要同步修改 `apps-script.gs` 的 `ROUTES`。

## 高科iAI
申請人在「設定 iAI」填入自己的 API 網址、模型名稱與 key，資料只存在其瀏覽器，費用扣個人額度。若出現連線錯誤，多半是 iAI 未開放從外部網頁直接呼叫（CORS）或需在校園網路內使用，請洽電算中心。
