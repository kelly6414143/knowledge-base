# 注意

## 開發小技巧：如何正確「更名」？

### 在執行更名動作時，有兩個細節需要注意：

* 使用 git mv 指令：直接在作業系統改名，Git 有時會把它偵測為「刪除舊檔」+「新增新檔」。建議使用 git mv <舊檔名> <新檔名>，這樣 Git status 會直接顯示為 renamed，歷史紀錄（Git Log）也會延續。
* 大小寫問題 (Windows/Mac)：Git 預設可能不區分大小寫。如果你只是想把 User.js 改成 user.js，Git 可能偵測不到變動。這時需要強迫更名：
git mv User.js temp.js && git mv temp.js user.js [2, 3, 4, 5, 6] 



### 要分辨檔案是「更名」還是「先刪除再新增」，主要取決於 Git 是否偵測到這兩者之間的關聯：
## 1. 透過 Source Control 面板確認

   1. 點擊左側活動列的 Source Control 圖示（或按 Ctrl + Shift + G）。
   2. 查看 "Changes" 列表：
   * 更名（Rename）：你會看到檔案顯示為 R 符號，後面跟著路徑變化（例如 old_name -> new_name）。
      * 刪除再新增（Delete & Add）：你會看到兩個獨立的狀態——舊檔案標示為 D (Deleted)，而新檔案標示為 U (Untracked) 或 A (Added)。 [1, 2, 3] 
   
## 2. 檔案瀏覽器（Sidebar）的顏色與代碼
在左側的檔案樹中，檔案名稱旁邊的字母代表其狀態：

* R (紫色/藍色)：表示檔案被重新命名。
* D (紅色/灰色)：表示檔案已刪除。
* U 或 A (綠色)：表示這是一個全新的檔案。 [2, 3] 

## 3. 如何讓 Git 「抓到」它是更名？
Git 的更名偵測是基於內容相似度。如果內容變動太大，Git 可能會誤判為一刪一增。你可以嘗試：

* 暫存後查看：先將新檔案 git add。通常在暫存（Stage）之後，Git 會重新比對內容，原本顯示的 D 和 A 可能會合併變回一個 R。
* 使用終端機檢查：在 Cursor 內建終端機輸入 git status -s。
* 出現 R old -> new 代表 Git 已成功偵測為更名。
   * 出現 D old 和 ?? new 則代表 Git 目前視其為兩個獨立事件。 [2, 3, 4] 


