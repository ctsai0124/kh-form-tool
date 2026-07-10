# 簡章轉報名表工具

上傳學校甄選簡章 PDF，自動判讀關鍵欄位（校名、簡章編號、報考組別、報名/甄試時間地點等），
套印成「報名表 / 甄選證 / 切結書」三件式表單，可直接列印或另存 PDF。

**完全在瀏覽器端執行，不需要 API key、不需要伺服器、不會外流任何資料**
（PDF 內容不會上傳到任何地方，OCR 與判讀都在使用者自己的電腦裡跑）。

---

## 放到 GitHub Pages 上線（約 5 分鐘）

### 1. 建立一個新的 Repository
1. 登入 GitHub → 右上角 `+` → **New repository**
2. Repository name 隨意取，例如 `kh-form-tool`
3. 選擇 **Public**（GitHub Pages 免費方案需要 Public repo；如果學校有企業版 GitHub 才能用 Private）
4. 建立完成後，把這個資料夾裡的 `index.html` 上傳進去：
   - 網頁上點 **Add file → Upload files**，把 `index.html` 拖進去
   - 或用 git 指令：
     ```bash
     git clone https://github.com/你的帳號/kh-form-tool.git
     cd kh-form-tool
     cp index.html .
     git add index.html
     git commit -m "建立簡章轉報名表工具"
     git push
     ```

### 2. 開啟 GitHub Pages
1. 進入 repo 的 **Settings → Pages**
2. Source 選擇 **Deploy from a branch**
3. Branch 選 `main`，資料夾選 `/ (root)`，按 **Save**
4. 等 1～2 分鐘，頁面上會出現網址，格式類似：
   ```
   https://你的帳號.github.io/kh-form-tool/
   ```

### 3. 把網址給人事同仁
直接把上面的網址傳給同仁，用 Chrome 或 Edge 開啟即可使用，不需要安裝任何東西。

---

## 給人事同仁的使用注意事項

- **第一次使用**掃描版簡章時，瀏覽器需要下載 OCR 語言模型（幾 MB），需要網路連線，
  大約多花幾秒到十幾秒；之後瀏覽器會快取起來，同一台電腦下次會快很多。
- 這是**規則式判讀**（不是 AI），碰到排版特殊的簡章可能抓錯或抓不到，
  **務必核對左側欄位再列印**，這也是為什麼所有欄位都做成可編輯。
- 掃描版 PDF 目前只會 OCR **前 4 頁**（大部分學校的關鍵資訊都在前 1～2 頁），
  如果有簡章把報名時間地點放在很後面的頁數，欄位會抓不到，需要手動填寫。
- 建議用 Chrome / Edge / Firefox 最新版；手機瀏覽器也能開，但列印排版建議用電腦。

## 之後想維護／調整欄位判讀規則

判讀規則都寫在 `index.html` 裡的 `parseFieldsFromText()` 這個函式，
是一串 regex（樣式比對），如果之後發現某個學校的欄位一直抓不到，
可以把該欄位附近的簡章文字片段告訴我，我再幫你加規則進去。
