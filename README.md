# FedFlow Prototype

靜態前端原型，使用 GitHub Pages 自動部署。

線上網址：
- https://seanbbear.github.io/fedflow/

## 專案檔案

- `index.html`：Console 首頁（Flow 列表 / 權限整合 / 我的 Flow）
- `builder.html`：Flow Canvas Builder
- `chat.html`：對話執行頁
- `run.html`：流程執行頁（模擬）
- `.github/workflows/deploy-pages.yml`：GitHub Pages 部署流程

## 本機開啟

```bash
cd /Users/sean.peng/Desktop/fedflow
open index.html
```

或使用本機伺服器：

```bash
cd /Users/sean.peng/Desktop/fedflow
python3 -m http.server 8080
```

打開 `http://localhost:8080`

## 修改後重新部署（GitHub Pages）

每次改完只要 push 到 `main`，GitHub Actions 會自動部署。

```bash
cd /Users/sean.peng/Desktop/fedflow
git add .
git commit -m "feat: your change"
git push origin main
```

## 查看部署狀態

- Actions：  
  https://github.com/seanbbear/fedflow/actions

- Pages 設定：  
  https://github.com/seanbbear/fedflow/settings/pages

Pages `Source` 需為 `GitHub Actions`。

## 常見問題

1. 網站 404  
   確認你開的是 `https://seanbbear.github.io/fedflow/`（要有 repo 名稱路徑）。

2. 已部署但看起來沒更新  
   等 1-2 分鐘後重新整理，或用無痕視窗開啟避免快取。

3. Actions 失敗  
   到 Actions 點開該次 run 檢查失敗 step，通常是 Pages Source 尚未設成 GitHub Actions。
