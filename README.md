# 🏸 羽球公平輪轉排隊系統

純前端單頁 HTML，無需後端，可直接部署到 GitHub Pages。

## 功能

- **計次優先演算法**：已打次數最少的人優先上場，次數相同則先加入者優先（FIFO）
- **QR Code 加入**：玩家掃碼後輸入名字即可加入等待隊列
- **手動加入**：管理員直接輸入名字加入
- **多場地管理**：支援 1–10 個場地，每場可設定人數
- **自動排輪**：按「開始下一輪」自動填滿所有空場地
- **場地計時**：顯示每場進行時間
- **次數排行榜**：即時顯示所有玩家已打次數與狀態

## URL 參數

| 網址 | 模式 |
|------|------|
| `index.html` | 管理員模式（完整控制） |
| `index.html?admin=1` | 管理員模式（同上） |
| `index.html?join=1` | 加入模式（QR Code 掃碼後的畫面） |

## 部署到 GitHub Pages

1. 建立 GitHub repo（e.g. `badminton-queue`）
2. 將 `index.html` push 到 `main` branch
3. 到 repo Settings → Pages → Source 選 `main` branch
4. 網址即為 `https://<username>.github.io/badminton-queue/`

## 單機限制說明

此系統使用 `localStorage` 儲存資料：

- **同一瀏覽器**（不同分頁）：透過 `BroadcastChannel` 即時同步，掃碼加入可自動通知管理員頁面
- **不同裝置**（手機掃碼）：玩家加入後系統會顯示「待確認」通知，管理員點擊確認即可批次加入；或直接由管理員手動輸入名字
