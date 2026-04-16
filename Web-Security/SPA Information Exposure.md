# SPA Information Exposure &nbsp;&nbsp;LV.1

### 🔬觀察 (Observation)
進入 OWASP Juice Shop 後，發現這是一個資安練習平台，照理說應該有一個「進度清單」或「計分板」來告訴使用者解題進度，但在網頁選單中完全找不到這個按鈕，就只是一個 Juice Shop Page？

<br>

### 🧐假設 (Hypothesis)
也許真正網頁藏在某個地方？ 例如藏在 Sources 而不是在 UI 上呈現？

<br>

### ⌨️實作 (Hands-on)
1. 進入瀏覽器開發者工具，切換到 Sources 分頁，Windows (F12)、MacOS (Option + Command + I)
2. 打開主程式檔案 main.js
3. 既然要找計分版，我們可以嘗試搜尋 score-board 或 path
4. 我們找到了一行 Code：```{ path: "score-board", component: bs }```
5. 手動將網址修改為：http://localhost:3000/#/score-board

<br>

### 📝結論 (Conclusion)
透過 http://localhost:3000/#/score-board 我們成功進入計分版頁面
這代表可以繞過 UI 限制，直接存取原本不打算對外公開的後台資訊或管理功能

<br>

### 🧰維護 (Mitigation)
不應該僅在前端 UI 隱藏連結，對於敏感路徑，後端必須實施權限驗證（Authorization），確保只有特定權限的使用者才能看到特定頁面的資料
