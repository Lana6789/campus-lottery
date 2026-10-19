# 校內集章抽獎系統 (Campus Lottery System)

🎉 本專案為校內集章抽獎活動打造，提供線上的扭蛋抽獎體驗與後台現場核銷管理功能。透過學號綁定與鎖定機制，有效防止傳統紙本集點卡一人重複抽獎的問題。

---

## 網頁頁面與功能說明

### 1. 學生身分驗證頁 (`index.html`)
* 學生輸入學號、姓名、年級與系所。
* 發送 API 檢查學號是否已抽過獎，若符合資格則暫存資料並自動前往抽獎頁。

### 2. 扭蛋機抽獎與結果頁 (`draw.html`)
* **扭蛋機動畫**：點擊「開始抽獎」觸發扭蛋機變形擠壓動畫。
* **開獎互動**：彈出立體扭蛋殼，點擊扭蛋殼揭曉獎項。
* **結果展示**：動態載入獎品對應照片、顯示大獎/特別獎標籤及現場領獎須知。

### 3. 管理員後台主控台 (`admin.html`)
* **獎品庫存管理**：線上即時修改獎品總數、剩餘數與抽中權重。
* **現場核銷**：列表顯示學生抽獎紀錄，提供關鍵字搜尋與一鍵核銷按鈕。
* **報表匯出**：整合 SheetJS 套件，一鍵將抽獎紀錄匯出為 Excel (`.xlsx`)。

---

## 系統架構與技術 Stack

* **Frontend**：HTML5 / CSS3 / JavaScript (ES6+), Bootstrap 5, SheetJS
* **Backend**：Google Apps Script (GAS) Web App
* **Database**：Google Sheets (試算表)

---

## 專案檔案目錄結構

```text
├── index.html        # 學生驗證入口頁
├── draw.html         # 扭蛋抽獎與開獎頁
├── admin.html        # 後台管理與核銷主控台
├── appscript.js      # GAS 後端程式碼
├── gachapon.png      # 扭蛋機圖片
├── capsule.png       # 扭蛋殼圖片
└── images/           # 獎品照片目錄
