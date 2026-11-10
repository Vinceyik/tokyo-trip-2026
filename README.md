# 東京・神奈川・富士山 七日六夜旅程筆記

2026 年 11 月 12 日至 18 日，東京・神奈川・富士山家族之旅的隨身行程網站。

- **網站**：<https://vinceyik.github.io/tokyo-trip-2026/>
- **Repo**：<https://github.com/Vinceyik/tokyo-trip-2026>

---

## 這個網站是什麼

一個單頁、零依賴、可離線的旅行筆記，主要給作者與父母在旅途中用手機查看。設計取向：

- 日式簡約（和紙色、墨色、茜色），大量留白
- **大字體**，預設 17.5px，可一鍵切換「特大字」
- 每個景點都有 Google Maps 連結
- 出發前必辦事項（Visit Japan Web）、回程退稅、交通票券、緊急聯絡全部內建，旅程中不需要再上網搜尋

---

## 檔案結構

```
index.html                  ← 唯一的內容來源（所有文字、樣式、JavaScript 都在這裡）
sw.js                       ← Service Worker，提供離線快取
manifest.webmanifest        ← 加到手機主畫面的設定
assets/
  icon.svg                  ← 網站圖示
  oden-night-2026-11-13.jpg ← 三姨提供的海老名夜市海報
  hakone-freepass-route.jpg ← 三姨提供的箱根周遊券截圖
HANDOVER.md                 ← 交接文件：背景、已定決定、已核實事實、待補資料（AI 先讀這份）
AGENTS.md                   ← 給 AI 的編輯規則
README.md                   ← 本文件
```

`index.html` 是**單一真實來源**。不要在 repo 裡建立第二個 HTML 副本，否則內容會不同步。

---

## 如何修改內容

1. 直接編輯 `index.html`。
2. 用瀏覽器開啟（雙擊即可，或 `python3 -m http.server`）。
3. commit 並 push 到 `main`，GitHub Pages 會自動更新（約 1 分鐘）。

### 找尋要改的段落

每個區塊上方都有中文註解，例如：

```html
<!-- =========================================================
     住宿（全程只換一次）
     ========================================================= -->
```

| 想改什麼 | 搜尋字串 |
|---|---|
| 航班時間、航班號 | `航班資料` |
| 住宿、地址、Airbnb 連結 | `住宿（全程只換一次）` |
| 每日行程 | `id="d12"` 至 `id="d18"` |
| Visit Japan Web 步驟 | `Visit Japan Web` |
| 回程退稅 | `回程退稅流程` |
| 交通票券 | `交通票券總表` |
| 邊啲要預訂 | `預訂懶人包` |
| 緊急電話 | `緊急聯絡` |
| 天氣與衣著 | `11 月天氣與衣著` |
| 出發前清單 | `出發前清單` |
| 實用日文 | `實用日文` |

### 每日行程的固定結構

每一天是一個 `<article class="day-card" id="d12">`，內含：

```html
<header class="day-head">…</header>          <!-- 日期、標題、副標 -->
<div class="aunt-banner">…</div>             <!-- 選用：三姨提示 -->
<ol class="schedule-list">
  <li class="schedule-item">
    <div class="schedule-meta">
      <span class="time-pill">15:05</span>   <!-- 時間 -->
      <span class="category-text">抵達</span> <!-- 分類 -->
    </div>
    <h4 class="schedule-title">…</h4>
    <p class="schedule-desc">…</p>
    <a class="inline-map-link" href="…">📍 …</a>
  </li>
</ol>
<aside class="day-note">…</aside>            <!-- 貼心備忘 -->
<aside class="meal-note">…</aside>           <!-- 餐飲建議 -->
```

新增一個行程項目，複製整個 `<li class="schedule-item">…</li>` 再改文字即可。

---

## 設計規範（改動時請遵守）

| 項目 | 值 |
|---|---|
| 背景 | `#F4F1EA` |
| 卡片 | `#FCFBF8` |
| 主文字 | `#22201E` / `#3D3935` |
| 強調色 | `#9E3B2E`（茜色，只用於重點） |
| 輔助色 | `#3B5944`（千歲綠） |
| 圓角 | 16px 卡片 / 12px 內層 |
| 正文 | `calc(17.5px * var(--scale))` |
| 標題 | 明朝體 `.serif` |

規則：

- **不要新增第三、四種強調色**。整體只有茜色與綠色。
- 所有字級用 `calc(Npx * var(--scale))`，否則「特大字」模式會失效。
- 觸控目標最小 44px 高。
- 卡片左右邊界必須一致（`.app` 的 16px padding）。
- 不要用 `position: fixed` 蓋住內容。

---

## 內容注意事項

網站上的價格、時間、營業資訊會變。修改時請：

- 標明「以官網為準」或「以現場為準」，不要寫死會過期的數字。
- 航班、酒店、Airbnb 連結如更新，同時更新 `README` 沒提到的部分即可，無需另開檔案。
- 三姨的資料（電話）由使用者自行在網頁上填寫，**不要 commit 私人電話到 repo**。

---

## 部署

GitHub Pages，branch `main`，root directory。Push 後自動部署。

```bash
git add -A
git commit -m "更新行程內容"
git push
```

---

## 給其他 AI 的指示

請先讀 `AGENTS.md`。
