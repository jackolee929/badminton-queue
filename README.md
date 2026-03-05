# 🏸 羽球公平輪轉排隊系統

單頁 HTML，部署於 GitHub Pages，資料儲存在 Firebase Realtime Database，支援多裝置即時同步。

🔗 **線上網址**：https://jackolee929.github.io/badminton-queue/

---

## 快速開始

1. 開啟網址 → 輸入自訂房間代碼（例如 `jacko-wed`）→ 進入房間
2. 球員掃 QR Code → 輸入名字 → 自動加入等待隊列
3. 管理員按「開始下一輪」→ 系統自動排場
4. 每場結束按「結束」→ 次數 +1，自動排下一輪
5. 球局結束後 ⚙️ 設定 → 結束並刪除房間

---

## 主要功能

### 排隊演算法
- 已打次數最少的人優先上場
- 次數相同則先加入者優先（FIFO）
- 可選擇「打亂同局數順序」避免永遠同組

### 房間機制
- 每個球隊建立獨立房間代碼，資料完全隔離
- 房間結束後可一鍵刪除 Firebase 資料，不累積歷史

### 跨裝置同步
- Firebase Realtime Database 即時同步
- 球員手機掃碼加入 → 管理員畫面立即顯示
- 多台裝置同時開啟同一房間，任何操作即時反映

### 手動干預
- **手動指定上場**：約戰、固定搭檔不受演算法限制
- **預排下場**（指定場地）：場地結束後優先上場，人數不足自動補齊
- **候補預排**（不指定場地）：任意空場地出現時優先上場
- 取消預排、移除玩家（在場玩家需二次確認）

---

## URL 格式

| 網址 | 說明 |
|------|------|
| `/?room=房間代碼` | 管理員模式（完整控制） |
| `/?room=房間代碼&join=1` | 球員加入模式（QR Code 掃碼後的畫面） |
| `/`（無參數）| 房間選擇畫面 |

---

## 部署到 GitHub Pages

1. Fork 或 clone 此 repo
2. 到 repo Settings → Pages → Source 選 `main` branch
3. 網址即為 `https://<username>.github.io/badminton-queue/`

### Firebase 設定（必要）

需要自行建立 Firebase 專案並設定 Realtime Database 規則：

```json
{
  "rules": {
    "rooms": {
      "$roomId": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

> 將 `index.html` 中的 `firebaseConfig` 替換為你自己的 Firebase 專案設定。

---

## 技術規格

- 純單一 `index.html`，無 npm / Node.js 依賴
- Firebase Realtime Database（compat SDK v9，CDN 引入）
- QRCode.js（CDN）
- 深色 / 淺色主題切換（偏好存於 localStorage）
- 手機優先響應式設計
