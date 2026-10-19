# 校內集章抽獎系統 (Campus Lottery System) - 專案說明書

## 1. 專案背景與目的
本專案旨在為校內集章抽獎活動提供一個線上的獎品抽籤與現場核銷系統。
由於實體集點卡無法辨識學生真實身分，容易發生一人持多張卡重複抽獎的情況。本系統透過學生學號綁定與 GAS 後端鎖定機制，確保「一學號限抽一次」，並提供扭蛋機互動體驗與後台現場核銷功能。

---

## 2. 系統架構與技術棧

* **前端 (Frontend)**：HTML5 / CSS3 / JavaScript (ES6+), Bootstrap 5, SheetJS (xlsx)
* **後端 (Backend)**：Google Apps Script (GAS) Web App (`doGet` / `doPost`)
* **資料庫 (Database)**：Google Sheets (試算表)
  * `DrawRecords` 工作表：儲存學生抽獎與核銷紀錄
  * `Prizes` 工作表：儲存獎品清單、剩餘數量與機率權重

---

## 3. 核心功能與頁面流程

### 3.1 學生端頁面
1. **資格驗證頁 (`index.html`)**：
   * 學生輸入學號、姓名、年級與科系。
   * 發送 `checkStudent` 請求至後端驗證是否已抽過獎。
   * 通過後將學生資訊暫存於 `sessionStorage` 並自動跳轉至抽獎頁面。
2. **扭蛋抽獎與結果頁 (`draw.html`)**：
   * 展示互動扭蛋機介面，點擊後觸發扭蛋機擠壓變形動畫 (`squash-animation`)。
   * 發送 `executeDraw` 請求，由後端執行加權隨機抽獎與扣減庫存。
   * 繪製彈出扭蛋殼，學生點擊扭蛋殼開獎。
   * 顯示中獎畫面（包含學生資料、獎品名稱、大獎/特別獎標籤、動態載入獎品照片及現場領獎須知）。

### 3.2 管理員後台 (`admin.html`)
1. **庫存與機率設定**：
   * 即時載入並顯示所有獎品之總數量、剩餘數量與權重。
   * 支援線上修改並儲存更新至後端 (`updatePrize`)。
2. **學生抽獎紀錄與現場核銷**：
   * 列表顯示學生學號、姓名、年級/科系、抽中獎項 ID、抽獎時間與領取狀態。
   * 提供即時關鍵字搜尋（學號、姓名）。
   * 提供單鍵「現場核銷 / 標示為未領取」切換功能 (`toggleClaim`)。
3. **數據報表匯出**：
   * 使用 SheetJS 匯出全部抽獎與核銷紀錄為 Excel (`.xlsx`) 檔案。

---

## 4. 檔案結構說明

* `index.html`：學生驗證與資料輸入入口頁面
* `draw.html`：扭蛋機動畫與抽獎結果展示頁面
* `admin.html`：管理員主控台頁面
* `appscript.js`：Google Apps Script 後端處理邏輯
* `gachapon.png`：扭蛋機圖片資材
* `capsule.png`：扭蛋殼圖片資材
* `images/{prize_id}.{jpg|webp|png}`：動態載入之獎品圖片目錄