# 校內集章抽獎系統 (Campus Lottery System) - 系統規格書 (Specification)

## 1. 系統概述

### 1.1 專案簡介
本系統為校內集章抽獎活動之線上抽獎與核銷管理平台。透過前端響應式網頁與 Google Apps Script 後端服務結合，達到防重複抽獎、加權庫存扣減以及現場即時核銷之目的。

### 1.2 系統使用者
* **學生**：進行資格驗證、體驗線上扭蛋抽獎並出示領獎頁面。
* **現場工作人員 / 管理員**：核對學生身分並核銷獎品、調整獎品庫存、匯出統計報表。

---

## 2. API 介面規格 (Google Apps Script API)

### 2.1 檢查學生抽獎資格 (GET)
* **請求範例**：`GET ?action=checkStudent&student_id=S112001`
* **回應格式**：
  * **可抽獎**：`{ "status": "eligible", "message": "符合資格" }`
  * **已抽過**：`{ "status": "already_drawn", "message": "您已經參加過抽獎了！" }`

### 2.2 執行抽獎 (POST)
* **請求 Payload**：
  ```json
  {
    "action": "executeDraw",
    "student_id": "S112001",
    "name": "王小明",
    "grade": "大一",
    "department": "資訊管理學系"
  }