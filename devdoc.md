
```markdown
# URLBalancer 前端開發文檔

## 1. 專案概述

- 名稱：URLBalancer 前端應用
- 目的：提供使用者友好的介面，管理後端 API Endpoint 及其對應的 Target 實例，並發送 HTTP 請求進行 CRUD 操作。

## 2. 技術選型

- 框架：React 18 + Vite
- 語言：JavaScript (ES2021+)（可選 TypeScript）
- 路由：React Router v6
- HTTP 客戶端：Axios（配置於 `src/services/apiClient.js`，baseURL 設為 `/api/v1`）
- 狀態管理：React Context / Redux（可選）
- 樣式：CSS Modules 或 Tailwind CSS
- 測試：Jest + React Testing Library
- Lint：ESLint + Prettier（配置於 `.eslintrc.js`、`prettier.config.js`）

## 3. 專案結構
```text
<project_root>/
├─ public/               # 靜態資源 (index.html, favicon, 圖片)
├─ src/
│  ├─ assets/            # 圖片、SVG、字體
│  ├─ components/        # 可重用元件
│  │   ├ EndpointList.jsx
│  │   └ TargetList.jsx
│  ├─ pages/             # 路由頁面
│  │   └ EndpointDetails.jsx
│  ├─ services/          # API 客戶端封裝
│  │   └ apiClient.js
│  ├─ App.jsx            # 根元件，負責路由與全域設定
  │  └ main.jsx          # 入口：掛載 React app
├─ package.json          # 依賴與腳本定義
├─ vite.config.js        # 開發伺服器與 Proxy 設定
└─ README.md             # 開發與部署說明
```
## 4. API 規格 (後端)

- Base URL: `/api/v1`
- 無需授權

### 4.1 Endpoints 列表

1. GET  `/endpoints`
   - 功能：取得所有 Endpoint (含 Targets)
   - 回傳型別：`Endpoint[]`

2. POST `/endpoints`
   - 功能：新增 Endpoint
   - Request Body：`{ path: string }`
   - 回傳：新增後 `Endpoint` 物件

3. GET  `/endpoints/:id`
   - 功能：取得單一 Endpoint (含 Targets)

4. PUT  `/endpoints/:id`
   - 功能：更新 Endpoint
   - Request Body：`{ path: string }`

5. DELETE `/endpoints/:id`

6. POST `/endpoints/:id/targets`
   - 功能：在指定 Endpoint 下新增 Target
   - Request Body：
```json
     {
       "url": "http://example.com",
       "weight": 1,
       "header_rewrite": {},
       "body_rewrite": {}
     }
```
7. PUT    `/targets/:id` (更新 Target)
8. DELETE `/targets/:id` (刪除 Target)

## 5. 資料模型

- Endpoint:
  - id: number
  - path: string
  - targets: Target[]
- Target:
  - id: number
  - url: string
  - weight: number
  - header_rewrite: object
  - body_rewrite: object

## 6. 開發與運行

- 安裝依賴：`npm install`
- 啟動開發：`npm run dev` (http://localhost:5173)
- Proxy：`/api` 轉發到 `http://localhost:8080`，對應後端 `/api/v1`
- 建置：`npm run build` => `dist/`
- 預覽：`npm run preview`

## 7. 代碼風格與質量

- ESLint + Prettier
- Commit: Conventional Commits
- PR: 通過 CI 測試後合併

## 8. 測試策略

- 單元測試：Jest + React Testing Library
- 指令：`npm run test`、`npm run test:coverage`

## 9. 部署建議

- Docker + Nginx 靜態部署 `dist/`
- CI/CD：GitHub Actions / GitLab CI

## 10. 可擴充功能建議

- 身份驗證與權限
- 全域狀態管理
- 主題切換 (暗黑模式)
- 性能優化 (Code Splitting, Lazy Loading)
```


