# Credential / Integration 管理 Spec

作者：Sean Peng

## 1. 目的
定義平台 Credential / Integration 管理產品設計，兼顧：
- 使用者可快速連接第三方服務
- MIS 可集中治理企業憑證與 OAuth App
- Flow 執行端不需知道憑證取得細節

適用範圍：
- OAuth Connector（Google / Microsoft / Jira）
- API Key / PAT Connector（BYOK）
- Flowise 底層整合情境

## 2. 背景
### 2.1 現有問題
- Credential 設定過於工程導向
- 假設每位使用者都能自行建立 OAuth App（企業實務不可行）
- Client Secret 分散造成資安風險
- MIS 無法集中控管 Scope / OAuth App

### 2.2 核心挑戰
- 並非所有 Provider 都支援 OAuth
- 部分整合只能用個人 API Key / PAT
- 若完全強制 MIS 管控會降低平台擴充性

## 3. 設計原則
- 集中治理：OAuth App 由 MIS 管控
- 個人彈性：允許 BYOK，清楚責任邊界
- 最小權限：只請求必要 scope
- 來源可辨識：Managed vs Personal
- Run-As 可辨識：User Delegated vs Org Shared
- Execution 無感：執行端不關心憑證來源細節

## 4. 角色與權限
### 4.1 角色
- Admin / MIS：管理 Provider、OAuth App、Scopes、啟用狀態
- 一般使用者：連接/斷開已啟用 Connector；若允許可新增個人 API Key

### 4.2 邊界
- 一般使用者不可查看或修改 Client Secret
- MIS 不可查看個人 API Key 明文

## 5. Connector 分級與策略（Dual Credential Model）
### 5.1 Provider 屬性
- `authType`: `oauth | api_key | pat | mixed`
- `ownership`: `managed | personal | mixed`
- `accountContext`: `user_delegated | org_shared | mixed`

### 5.2 Managed Connector
- OAuth App 與 Secret 屬公司資產
- 由 MIS 維護
- 使用者只進行授權（或使用已配置之 Org Shared）

### 5.3 Personal Connector (BYOK)
- 使用者自行輸入 API Key / PAT
- 系統僅加密保存與驗證
- UI 必須提示個人資產責任邊界

### 5.4 Mixed Connector
- 同時支援 Managed + Personal
- 預設優先顯示 Managed（若存在）
- 使用者可明確選擇連接方式

### 5.5 Run-As / Account Context
- User Delegated：代表使用者本人帳號執行
- Org Shared Account：代表組織公用帳號執行（例如 noreply@company.com）

## 6. Flow 情境 Credential 行為
### 6.1 角色
- Builder：設定 Credential Policy
- Runner：必要時完成個人連接
- MIS：維護組織憑證

### 6.2 Policy
- `組織(Managed/Org Shared)`：僅可用組織帳號
- `個人(Personal/User Delegated)`：僅可用本人帳號
- `皆可`：先組織、再個人

### 6.3 執行判斷
- 組織：有則執行；無則找 MIS
- 個人：有則執行；無則找使用者連接
- 皆可：組織優先；都無時先找使用者，並可提供通知 MIS 入口

### 6.4 Missing Handling
- Personal Missing：阻擋執行 + 立即連接 + 成功後重試
- Managed Missing：告知需管理員配置 + 顯示 Provider 資訊

### 6.5 Builder 設定
- Node Settings：`Credential Policy = 組織 / 個人 / 皆可`

## 7. 使用者流程
### 7.1 Integrations（使用者頁）
每張卡片顯示：
- 名稱 / Icon / 描述
- Connection Type（Managed / Personal / Mixed）
- Status（Not connected / Connected / Error）

### 7.2 OAuth（Managed）
- 使用者按 Connect
- OAuth 授權與 callback
- Token 保存後更新狀態

### 7.3 BYOK（Personal）
- 輸入 API Key / PAT
- Validate
- 成功後加密保存

## 8. Credential Console
### 8.1 功能
- 管理 Provider
- 設定 OAuth App
- 啟用 / 停用 Connector

### 8.2 OAuth 欄位
- Client ID
- Client Secret（masked）
- Redirect URI
- Scopes（checkbox）
- Status Toggle

## 9. 系統資料模型
### 9.1 `connector_providers`
- key / name / authType / ownership / accountContext / enabled

### 9.2 `connector_provider_configs`
- clientId / clientSecretEncrypted / scopes
- （選配）orgSharedTokenEncrypted
- （選配）orgSharedAccountLabel

### 9.3 `user_connector_links`
- userId / workspaceId / providerId
- credentialSource（managed | personal）
- runAs（user_delegated | org_shared）
- tokenEncrypted / status / timestamps
- （選配）accountLabel

## 10. 安全與稽核
- Secret / Token 全部加密保存
- OAuth state 一次性
- 全操作寫入 Audit Log：connect / disconnect / refresh / update config

## 11. 驗收條件
- 使用者不需接觸 Client Secret 即可完成 OAuth 連接
- BYOK 可獨立於 MIS 存在
- 憑證來源可被系統與 Audit Log 清楚識別
- Flow / Agent 可正常使用憑證執行
- Provider 停用後不可新增連接
