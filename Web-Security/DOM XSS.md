# DOM XSS &nbsp;&nbsp;LV.1

### 🔬 觀察 (Observation)
在網頁右上角的 Search 框輸入 test，發現輸入的內容會直接呈現在網頁上，進一步嘗試輸入 HTML 標籤 \<h1>test\</h1>，網頁竟然直接渲染了該標籤（字體變大），代表程式沒有過濾使用者輸入的內容

<br>

### 🧐 假設 (Hypothesis)
既然頁面會執行我輸入的 HTML，那麼我假設如果輸入帶有 JavaScript 執行的代碼（Payload），瀏覽器也同樣會執行，進而達成 DOM-based XSS 攻擊

<br>

### ⌨️ 實作 (Hands-on)
1. 初步測試：在 Search 框輸入 test，確認內容原樣呈現
2. 標籤測試：輸入 \<h3>test\</h3>，確認網頁會解析 HTML 語法使字體變大
3. 注入攻擊：輸入惡意 Payload：``` <img src="x" onerror="alert('XSS')"> ```
   - 原理：故意給一個不存在的圖片路徑 \"(src="x")\"，觸發 \"onerror\" 事件來執行 JavaScript
5. 結果驗證：成功彈出顯示 "XSS" 的通知視窗

<br>

### 📝 結論 (Conclusion)
驗證結果顯示此頁面存在 DOM XSS 漏洞
當數據從 URL 參數（Source）被讀取，並在未經過濾的情況下寫入頁面（Sink）時，漏洞便發生了
 - 攻擊 URL 範例：
```http://localhost:3000/#/search?q=%3Cimg%20src%3D%22x%22%20onerror%3D%22alert('XSS')%22%3E```

<br>

### 🧰 維護 (Mitigation)
1. 輸入過濾：對所有使用者輸入的特殊字元（如 \`< \` 、 \` > \`）進行 HTML 編碼轉義。
2. 安全 API：在寫入 DOM 時，優先使用 \`.textContent\` 而不是 \`.innerHTML\`，避免瀏覽器將字串當作代碼執行
