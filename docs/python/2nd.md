## Python 資料分析入門（Day 2）

**日期**：2025-10-25  
**來源**：自學課程《AI 資料科學家全方位學程》— pandas 資料表格操作入門  
**關聯主題**：#Python #pandas #資料分析 #DataFrame #CSV #Colab #資料科學入門  

---

### 📘 學習摘要

**課程主題：**  
學習如何使用 `pandas` 操作資料表格，理解 DataFrame 與 Series 的結構與用途，並能夠讀取、篩選與運算資料。

**🎯 學習目標：**  
1. 理解 pandas 的核心結構：**Series** 與 **DataFrame**。  
2. 學會從 CSV 檔案中讀取資料、檢視與簡單分析。  
3. 能進行欄位篩選、排序與運算操作。  

**🧠 核心概念：**
- pandas 是 Python 的資料分析核心工具，讓資料處理像操作 Excel 一樣直覺。
- 支援多種格式（CSV、Excel、JSON、SQL），與 `numpy`、`matplotlib`、`scikit-learn` 無縫整合。
- 類比思維：
  - JS 陣列 → pandas `Series`
  - JS 物件陣列 → pandas `DataFrame`

> 💡 pandas 的設計哲學是「用最少的程式碼完成最多的資料操作」。

---

### 💻 實作範例

**1️⃣ 導入與建立資料表**
```python
import pandas as pd

data = {
    "Name": ["Alice", "Bob", "Cindy", "David"],
    "Age": [25, 30, 22, 35],
    "Score": [88, 92, 79, 95]
}

df = pd.DataFrame(data)
print(df)
````

**2️⃣ 常用操作**

```python
# 查看前幾筆資料
print(df.head(2))

# 查看統計摘要
print(df.describe())

# 篩選條件：Score > 85
print(df[df["Score"] > 85])

# 排序
print(df.sort_values(by="Score", ascending=False))
```

**3️⃣ 讀取 CSV 實戰**
建立檔案 `students.csv`：
>如何建立csv檔請看[連結](#建立csv檔)

```csv
Name,Age,Score
Alice,25,88
Bob,30,92
Cindy,22,79
David,35,95
Ella,27,81
```

在 Colab 執行：

```python
df = pd.read_csv("students.csv")
print(df)
print(df[df["Age"] > 25])
```

---

### 🧩 練習任務（20分鐘）

**目標：**

1. 用 pandas 建立一個 DataFrame，包含：

   * 欄位：`Product`, `Price`, `Quantity`
   * 至少 5 筆資料
2. 新增欄位 `Total = Price * Quantity`
3. 篩選出 `Total > 1000` 的商品
4. 由高到低排序

**範例輸出：**

```
  Product  Price  Quantity  Total
2  Laptop  30000         1  30000
4  Tablet  12000         2  24000
```

**Google Colab 練習位置：**  
[Colab連結：2nd.pythonLearning](https://colab.research.google.com/drive/14Oy0bd_khyR1fv7R_-dRr4xQwC80Yy_u?hl=zh-tw#scrollTo=VjHtrS_uaKvM)

---

### 📈 延伸挑戰：從前端思維轉換成資料操作思維

| 類別  | JavaScript                                       | pandas                                        |
| --- | ------------------------------------------------ | --------------------------------------------- |
| 篩選  | `arr.filter(x => x.score > 85)`                  | `df[df["score"] > 85]`                        |
| 排序  | `arr.sort((a,b) => b.score - a.score)`           | `df.sort_values(by="score", ascending=False)` |
| 新欄位 | `arr.map(x => ({...x, total: x.price * x.qty}))` | `df["total"] = df["price"] * df["qty"]`       |

> 💡 小技巧：
> pandas 支援「鏈式操作」(chained operations)，可連續處理資料：
>
> ```python
> df[df["Score"] > 80].sort_values(by="Age")[["Name", "Score"]]
> ```

---

### 💡 其他說明與應用

* pandas 的「資料思維」與「前端思維」的差異：
  從操作 DOM → 轉為操作資料表格。
* `DataFrame` 結構直觀清晰，像 Excel + JS object 的結合。
* 使用 `.describe()` 能快速取得統計摘要，非常適合初步探索資料。
* 鏈式操作語法極為強大，可將篩選、排序、欄位挑選合併在一行。
* 之後可結合 `matplotlib` 繪製視覺化圖表，讓分析結果更直觀。

---

### 🔗 延伸學習

* [pandas 官方教學文件](https://pandas.pydata.org/docs/)
* Kaggle：Python + pandas 實戰練習
* 延伸閱讀：

  * 《Python for Data Analysis》by Wes McKinney
  * [Google Colab](https://colab.research.google.com) 線上執行環境

## 建立csv檔

### 🧰 方法一：直接在 Google Colab 建立檔案（最方便）

> 適合剛開始練習、不想開啟 VSCode 的情況。

#### ✅ 步驟

1. 打開 [Google Colab](https://colab.research.google.com)
2. 新增一個新的 Notebook
3. 在第一個 code cell 貼上這段程式碼執行：

```python
# 直接用 Python 建立 students.csv
import pandas as pd

data = {
    "Name": ["Alice", "Bob", "Cindy", "David", "Ella"],
    "Age": [25, 30, 22, 35, 27],
    "Score": [88, 92, 79, 95, 81]
}

df = pd.DataFrame(data)
df.to_csv("students.csv", index=False)  # 存成 CSV 檔
print("✅ 已建立 students.csv 檔案！")

# 驗證是否成功
!ls
```

執行完後你會看到：

```
students.csv
sample_data/
```

✅ 接著你就能用：

```python
pd.read_csv("students.csv")
```

來讀取這個檔案了。

---

### 💻 方法二：用 VSCode 本地端建立（專案實戰用）

> 適合你想用本機 Python 環境練習（例如 `python` 或 `jupyter notebook`）。

#### ✅ 步驟

1. 在你的資料夾（例如 `~/python_project/`）底下建立新檔案：

   ```
   students.csv
   ```

2. 貼上以下內容：

   ```csv
   Name,Age,Score
   Alice,25,88
   Bob,30,92
   Cindy,22,79
   David,35,95
   Ella,27,81
   ```

3. 存檔後在同一資料夾建立一個 `read_csv_test.py`：

   ```python
   import pandas as pd

   df = pd.read_csv("students.csv")
   print(df)
   ```

4. 在終端機執行：

   ```bash
   python read_csv_test.py
   ```

---

### ☁️ 方法三：用 Google Sheets 另存成 CSV

> 適合沒有開發環境、想快速產生資料檔案。

#### ✅ 步驟

1. 開啟 Google Sheets → 新增試算表
2. 在 A1~C6 輸入以下資料：

| Name  | Age | Score |
| ----- | --- | ----- |
| Alice | 25  | 88    |
| Bob   | 30  | 92    |
| Cindy | 22  | 79    |
| David | 35  | 95    |
| Ella  | 27  | 81    |

3. 點選：

   ```
   檔案 → 下載 → 逗號分隔值 (.csv)
   ```
4. 存成 `students.csv`，即可在 Python 讀取。

---

### 🎯 確認檔案正確性

你可以用任何文字編輯器（如 VSCode、Notepad、Sublime）打開看看。
正確格式應該長這樣👇：

```
Name,Age,Score
Alice,25,88
Bob,30,92
Cindy,22,79
David,35,95
Ella,27,81
```