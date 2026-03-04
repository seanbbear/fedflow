# 企業常見 Workflow Task 清單

本文件盤點各部門在日常營運中最常見、最具標準化潛力的任務（Task），作為未來 Flow / Template Store 的主要來源。

## 🧭 產品定位與設計原則

### 1️⃣ 分層模型

產品以 Task → Action → Node 三層結構組成：

- 使用者在 Builder 中只會接觸到 Action
- Node 屬於底層技術實作與編排細節，對一般使用者隱藏

### 2️⃣ 設計哲學

FedFlow 核心目標：簡潔、可理解、可快速上手

Phase 1 原則：

- 優先移除過度彈性、工程導向的設定方式
- 不鼓勵使用者直接面對大量參數或客製 Node
- 將常見需求收斂為「標準化 Action」

未來擴充策略：

- ✅ 以新的 Action 形式加入
- ❌ 不回到自由拼裝 Node

### 3️⃣ 與既有 Flowise 的關係

FedFlow 為新一代產品，將與既有 Flowise 並存一段時間。

並存策略：

- 後端 refactor 盡量維持相容
- 既有流程可持續運作
- 主要改動集中在前端 Builder 體驗與抽象模型

目標：

- 提供更簡潔
- 更可治理
- 更可產品化的操作方式

當 FedFlow 能完整覆蓋既有功能後，再逐步完成遷移。

## ⚙️ 系統前提

- 每一個 Task 由多個 Action 組成
- 每一個 Action 底層由 Node 實作（對 Builder 隱藏）

Tool Provider（工具來源）在特定 Action 中，實際提供能力的後端來源，例如：

- RAG
- LLM

Builder 僅需：

- 選擇 Action
- 指定 Provider

## 🚩 Phase 規劃總覽

| 範圍 | Phase 1（先落地） | Phase 2（平台化） |
| --- | --- | --- |
| Flow 建立方式 | 使用既有 Action 組裝 | 可自行用 Node 封裝新 Action |
| 通知能力 | 使用者寄信 | 系統通知（服務帳號） |
| Action 來源 | 平台預先定義 | 團隊可擴充、可發佈 |
| Builder 能力 | 使用 / 組合 | 建立 / 分享 / 重用 |

## 🔐 服務帳號 vs 使用者帳號

| 面向 | 系統通知 | 使用者寄信 |
| --- | --- | --- |
| 發信身份 | 平台服務帳號 | Flow 執行者 |
| OAuth 需求 | 不需要 | 需要使用者授權 |
| 稽核紀錄 | 系統行為 | 個人行為 |
| 適用場景 | 通知 / 提醒 / 流程結果 | 對客戶 / 對外窗口 |
| MIS 控制 | 統一管理 | 需額外權限策略 |
| 信件內容來源 | 系統模板 / Builder 自訂 | 使用者自訂 |

## 🧑‍💼 人資（HR）

| Task | 流程 |
| --- | --- |
| 新員工入職 | 表單 → 審核（HR） → （Phase 2）建立 jira ticket → 審核（IT） → 使用者寄信 |
| 員工離職 | 表單 → 審核（主管） → （Phase 2）建立 jira ticket → 審核（IT/行政） → 使用者寄信 |
| 請假申請 | 表單 → 判斷 → 審核（主管） → 使用者寄信 |
| 加班申請 | 表單 → 審核（主管） |
| 出勤異常 | 表單 → 審核（主管） |
| 招聘流程 | 表單 → 審核（HR） → 判斷 → 審核（用人主管） → 判斷 |
| 績效考核 | 表單 → 判斷 → 審核（主管） → 判斷 |
| 人事異動 | 表單 → 審核 → 判斷 |
| 教育訓練申請 | 表單 → 審核 |
| 員工證明申請 | 表單 → 審核 |

## 💰 財務（Finance）

| Task | 流程 |
| --- | --- |
| 費用報銷 | 表單 → 判斷（金額） → 審核（主管） → 審核（財務） → 使用者寄信 |
| 付款申請 | 表單 → 審核（財務） |
| 採購申請 | 表單 → 判斷（預算） → 審核（主管/財務） |
| 預算審批 | 表單 → 審核（財務） → 審核（高層） → 判斷 |
| 發票處理 | 表單 → 審核（財務） |
| 收款確認 | 表單 → 判斷（是否一致） |
| 零用金申請 | 表單 → 審核（主管） |
| 合約付款里程碑 | 表單 → 審核（主管/財務） |

## 🏢 行政（Admin / Ops）

| Task | 流程 |
| --- | --- |
| 用印申請 | 表單 → 審核（主管/法務） |
| 訪客申請 | 表單 → 審核（受訪者/行政） |
| 差旅申請 | 表單 → 判斷（預算） → 審核（主管） |
| 辦公用品申請 | 表單 → 審核（主管/行政） |
| 會議室預約 | 表單 → 判斷（是否衝突） → 審核（管理者） |
| 活動申請 | 表單 → 審核（主管） |

## ⚖️ 法務（Legal / Compliance）

| Task | 流程 |
| --- | --- |
| 合約審查 | 表單 → 審核（法務） |
| NDA 簽署 | 表單 → 審核（法務） |
| 合規確認 | 表單 → 審核（合規） |
| 風險評估 | 表單 → 審核（風控） |

## 🧑‍💻 IT / MIS / Infra

| Task | 流程 |
| --- | --- |
| 權限申請 | 表單 → 審核（資安） |
| 開通帳號 | 表單 → 審核（管理員） |
| 權限變更 | 表單 → 審核（管理員） |
| 資產領用 | 表單 → 審核（IT/行政） |
| 事件通報 | 表單 → Agent（判斷嚴重度）→ 審核 |
| 變更管理 | 表單 → 審核（主管） |
| 軟體安裝 | 表單 → 審核（IT） → 判斷 |
| 信件自動處理 | 表單 → 讀取信件 → 判斷 → Agent |
| 告警自動判讀 | 表單（或事件） → Agent → 判斷 → 審核 |
| SOP 查詢輔助 | 表單 → 使用工具 → 使用者寄信 |

## 📈 業務 / 營運（Sales / Operation）

| Task | 流程 |
| --- | --- |
| 報價申請 | 表單 → 判斷（折扣） → 審核（主管） → 使用者寄信 |
| 客戶資料建立 | 表單 → 審核（主管） |
| 專案立案 | 表單 → 審核（主管） |
| 合約走簽 | 表單 → 審核（法務） |
| 客戶來信自動分類 | 讀取信件 → Agent → 判斷 |
| 客戶問答自動回覆 | 讀取信件 → 使用工具 → 使用者寄信 |
| 商機資格預審 | 表單 → Agent → 判斷 → 審核（業務主管） |

## 🔧 本文件使用的 Action 類型

- 表單
- 判斷
- 審核
- 使用者寄信（Send as User）
- Agent
- 讀取信件
- 使用工具（選擇 Tool Provider）

## 🧩 Action 設定欄位（Builder）

本區為 UI/UX 畫面設計依據版。每個欄位皆對應具體元件，設計師可直接依此畫右側設定面板。

### ✅ Action 清單（供 Palette 與設定面板使用）

| Action | 用途 | 使用的 Type |
| --- | --- | --- |
| 表單（Form） | 收集資料並產生 form.* 變數 | text / password / number / date / checkbox / file / select / list |
| 判斷（Condition） | 依條件分流（True/False） | text / number / date / checkbox / select / list |
| 審核（Approval） | 發起人工審核並取得 approve/reject | text / date / checkbox / select / list |
| 使用者寄信（Send as User） | 以執行者身份寄信 | text / file / list |
| Agent | 用 LLM 做摘要/分類/擷取/生成 | text / number / select / list |
| 使用工具（Tool Provider） | 用 RAG/FAQ/KB 查詢或產生草稿 | text / number / select / list |
| 讀取信件（Mail Reader） | 從信箱讀取信件成 mail.* 變數 | text / number / checkbox / select |

## 📝 表單（Form）

### 🎨 區塊 A：基本設定（固定顯示）

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 標題 | text | ✅ | 單行輸入，置頂 |
| 指派對象 | select | ✅ | 成員/角色 picker |
| 截止時間 | date | ❌ | 日期時間選擇器 |
| 描述 | text | ❌ | 多行輸入（表單說明） |

### 🧱 區塊 B：表單欄位（動態新增區）

設計概念：

- 上方「基本設定」為固定顯示
- 此區為可由使用者動態新增的表單題目
- 預設為空
- 使用者透過「＋新增欄位」逐筆加入

#### 🔘 區塊入口

| 元件 | Type | UI/UX 行為 |
| --- | --- | --- |
| ＋ 新增欄位 | button | 點擊後新增一筆欄位設定卡片 |

#### 🧾 單一欄位卡片（可重複）

| 子欄位 | Type | 必填 | UI 建議 |
| --- | --- | --- | --- |
| 顯示名稱 | text | ✅ | 使用者可見名稱 |
| 欄位類型 | select | ✅ | 下拉選單（text / password / number / date / checkbox / file / select / list） |
| 是否必填 | checkbox | ✅ | toggle |
| 預設值 | text | ❌ | 支援變數插入 |
| Placeholder | text | ❌ | 灰字提示 |
| 說明文字 | text | ❌ | help text |
| 選項 | list | ❌ | 僅 type = select 時顯示 |
| 驗證規則 | list | ❌ | 進階區（可折疊） |

### 🧠 欄位卡片動態行為（依 type 顯示）

共用欄位（所有 type 都顯示）：

- 顯示名稱
- 欄位類型（type: text, password, number, date, checkbox, file, select, list）
- 是否必填
- 說明文字

#### 📝 text（長文字）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| Placeholder | text | 輸入提示 |
| 預設值 | text | 預設文字 |
| 最大長度 | number | 選填 |

#### 🔢 number（數字）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 預設值 | number | 預設數字 |
| 最小值 | number | 驗證 |
| 最大值 | number | 驗證 |

#### ☑️ checkbox（勾選）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 預設勾選 | checkbox | 預設 true/false |

#### 🔽 select（下拉選單）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 選項清單 | list | label/value 結構 |
| 是否允許其他 | checkbox | 是否可輸入自訂 |
| 預設選項 | text | 對應 value |

#### 📅 date（日期時間）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 是否包含時間 | checkbox | date vs datetime |
| 預設值 | date | 預設日期 |
| 最早日期 | date | 驗證 |
| 最晚日期 | date | 驗證 |

#### 📎 file（檔案上傳）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 檔案類型限制 | text | 例如 pdf,jpg |
| 檔案大小上限（MB） | number | 上傳限制 |

#### 🧾 list（表格）

| 欄位 | Type | 說明 |
| --- | --- | --- |
| 子欄位 schema | list | 巢狀欄位定義 |
| 最少筆數 | number | 驗證 |
| 最多筆數 | number | 驗證 |

目標體驗：使用者選擇不同欄位類型，卡片即時變形（類似 Google 表單）。

## 🔀 判斷（Condition）

條件設定邏輯：

1. 先選擇資料來源的表單
2. 再選擇該表單中的欄位變數
3. 選擇與另一個變數或手動輸入值做比較

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 表單來源 | select | ✅ | 列出流程中已出現的 Form Action |
| 表單欄位 | select | ✅ | 依選擇的表單動態列出 form.* 欄位 |
| 判斷方式 | select | ✅ | = / ≠ / > / < / 包含 |
| 比較來源 | select | ✅ | 手動輸入 / 另一個變數 |
| 比較值 | text | ❌ | 當「手動輸入」時顯示 |
| 比較變數 | select | ❌ | 當「另一個變數」時顯示 |

UX 建議：預設顯示單一條件。

## ✅ 審核（Approval）

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 審核標題 | text | ✅ | 卡片標題 |
| 審核人 | select | ✅ | 成員/角色 picker |
| 申請人 | text | ✅ | 預設帶入 |
| 審核說明 | text | ❌ | 多行輸入 |
| SLA | date | ❌ | 到期提醒用 |

## ✉️ 使用者寄信（Send as User）

### 🎨 收件設定

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 收件人 | list | ✅ | email chips |
| 副本 CC | list | ❌ | 可收合 |
| 密件 BCC | list | ❌ | 可收合 |

### 🎨 信件內容

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 主旨 | text | ✅ | 支援變數 |
| 內容 | text | ✅ | 文字 |
| 附件 | file | ❌ | upload |

## 🤖 Agent

- 先參考現有的 agent node

## 🧰 使用工具（Tool Provider）— 右側面板規格

### 🎨 工具設定

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 任務名稱 | text | ❌ | Action 名稱 |
| Tool Provider | select | ✅ | 五種固定選項（Agentic RAG / Simple RAG / KBToolkit / FedGPT FAQ / gmail tool） |
| 任務類型 | select | ✅ | 查詢 / 草稿 / 摘要 |
| 輸入內容 | text | ✅ | 支援變數 |

### 🧩 Provider 專屬欄位（依 Tool 動態顯示）

#### 🤖 FedGPT Agentic RAG

| 欄位 | Type | 必填 | 說明 |
| --- | --- | --- | --- |
| KB 選擇 | select | ✅ | 知識庫來源 |
| 相似度門檻 | number | ❌ | 0–1 |
| 查無處理 | select | ❌ | fallback / 人工 |
| 輸出格式 | select | ❌ | text / JSON |

#### 📚 FedGPT Simple RAG

| 欄位 | Type | 必填 | 說明 |
| --- | --- | --- | --- |
| KB 選擇 | select | ✅ | 知識庫來源 |
| 相似度門檻 | number | ❌ | 0–1 |
| 查無處理 | select | ❌ | fallback |
| 輸出格式 | select | ❌ | text / JSON |

#### 🧾 KB Toolkit

| 欄位 | Type | 必填 | 說明 |
| --- | --- | --- | --- |
| KB 選擇 | select | ✅ | 指定知識庫 |
| 查詢模式 | select | ❌ | 精準 / 模糊 |
| 輸出格式 | select | ❌ | text / JSON |

#### ❓ FedGPT FAQ

| 欄位 | Type | 必填 | 說明 |
| --- | --- | --- | --- |
| FAQ 集合 | select | ✅ | FAQ 資料來源 |
| 未命中處理 | select | ❌ | fallback / 人工 |
| 輸出格式 | select | ❌ | text |

#### 📬 Gmail Tool

| 欄位 | Type | 必填 | 說明 |
| --- | --- | --- | --- |
| Gmail 帳號 | select | ✅ | OAuth 綁定帳號 |
| Query 模式 | select | ✅ | 基礎 / Gmail Query |
| from | text | ❌ | 寄件者 |
| to | text | ❌ | 收件者 |
| subject | text | ❌ | 主旨關鍵字 |
| Gmail Query | text | ❌ | 進階語法 |
| 讀取範圍 | select | ❌ | 最新一封 / N 封 |
| 是否下載附件 | checkbox | ❌ | toggle |
| 輸出格式 | select | ❌ | text / JSON |

## 📥 讀取信件（Mail Reader）— 右側面板規格

### 🎨 信箱設定

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 信箱帳號 | select | ✅ | service account |
| 篩選模式 | select | ✅ | 基礎 / Gmail Query |

### 🎨 篩選條件

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 寄件者 from | text | ❌ | 可多值（Phase2） |
| 收件者 to | text | ❌ | — |
| 主旨關鍵字 | text | ❌ | — |
| Gmail Query | text | ❌ | 大欄位 |

### 🎨 讀取控制

| 欄位 | Type | 必填 | UI/UX 行為 |
| --- | --- | --- | --- |
| 讀取範圍 | select | ✅ | 最新一封 / 最新 N 封 |
| N | number | ❌ | 條件顯示 |
| 是否下載附件 | checkbox | ❌ | toggle |
| 標記為已讀 | checkbox | ❌ | toggle |

## 🧱 基礎欄位型別（Field Types 定義）

Phase 1 Builder 僅支援以下 8 種型別：

| Type | UI 元件建議 | 資料型態 | 使用情境 | 說明 |
| --- | --- | --- | --- | --- |
| text | 單行輸入框 | string | 名稱、標題、Email、關鍵字 | 最通用文字輸入 |
| password | 密碼輸入框 | string | 憑證、密碼 | UI 需遮罩顯示 |
| number | 數字輸入框 | number | 金額、天數、Top K | 僅允許數值 |
| date | 日期時間選擇器 | datetime | 截止日、SLA | 建議支援時區 |
| checkbox | 勾選框 | boolean | 是否啟用、是否必填 | true / false |
| file | 檔案上傳 | file/blob | 附件、證明文件 | 需支援多檔（未來可擴） |
| select | 下拉選單（單選） | string | 狀態、角色、類型 | 需搭配 options |
| list | 動態清單 / 可新增多筆 | array | Email 清單、條件群組、欄位定義 | Phase 1 關鍵複合型別 |

## 🔍 型別設計原則

### 1️⃣ 極度收斂（Phase 1）

目標：

- 降低 Builder 複雜度
- 提升設計一致性
- 減少前端元件爆炸
- 有利企業治理

### 2️⃣ list 為關鍵複合型別 ⚠️

list 不只是 array，而是可展開子表單的容器元件。常見情境：

- 表單欄位定義
- Email 收件人清單
- 多條件判斷
- 顯示資料欄位選擇

前端需支援：

- 新增一筆
- 刪除一筆
- 拖曳排序（Phase 2 可選）
- 巢狀欄位 schema

### 3️⃣ select 必須支援 options

select 型別必須搭配：

- options[]
- label/value

Phase 2 可擴充：

- async options
- 搜尋式下拉
- 多選模式（可能獨立成 multiselect）

### 4️⃣ 型別自動轉換（Condition 專用）

在「判斷」Action 中由系統依來源欄位型別轉換：

- number → 數值比較
- date → 時間比較
- text → 字串比較
- checkbox → boolean
