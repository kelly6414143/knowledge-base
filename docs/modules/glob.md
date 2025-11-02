
# 📦 glob 模組完整說明

## 前提概要
在進行資料分析時，我們經常會遇到「**多檔案批次讀取**」的情況，例如：

* 每個月都有一份銷售報表 (`sales_jan.csv`, `sales_feb.csv`, `sales_mar.csv`)
* 每個部門都有一份資料 (`dept_A.csv`, `dept_B.csv`)
* 每個城市的資料分開存放 (`taipei_data.csv`, `kaohsiung_data.csv`)

## 🎯 一句話概念：

> **glob** 讓你用「萬用字元 (wildcard)」去搜尋符合條件的檔案路徑。

---

## 🧠 基本語法

```python
import glob

files = glob.glob(pattern, recursive=False)
```

### 參數說明：

| 參數          | 說明                         |
| ----------- | -------------------------- |
| `pattern`   | 檔案路徑搜尋樣式，例如 `"data/*.csv"` |
| `recursive` | 是否遞迴搜尋子資料夾（預設 False）       |

---

## 🔍 常見萬用字元（wildcards）

| 字元      | 功能                                 | 範例                                               |
| ------- | ---------------------------------- | ------------------------------------------------ |
| `*`     | 匹配任意字元（不限長度）                       | `*.csv` → 匹配所有 `.csv` 檔                          |
| `?`     | 匹配任意單一字元                           | `data_?.csv` → 匹配 `data_a.csv`, `data_1.csv`     |
| `[abc]` | 匹配括號內任一字元                          | `file_[12].csv` → 匹配 `file_1.csv` 和 `file_2.csv` |
| `**`    | （需搭配 `recursive=True`）匹配所有子資料夾中的檔案 | `data/**/*.csv`                                  |

---

## 💻 範例 1：找出所有 CSV 檔案

假設你有這些檔案：

```
sales_jan.csv
sales_feb.csv
sales_mar.csv
report.txt
```

```python
import glob

files = glob.glob("sales_*.csv")
print(files)
```

輸出：

```
['sales_jan.csv', 'sales_feb.csv', 'sales_mar.csv']
```

---

## 💻 範例 2：批次讀取所有 CSV 合併成一份 DataFrame

```python
import pandas as pd
import glob

files = glob.glob("sales_*.csv")

# 用 list comprehension 一次讀入所有檔案
df_all = pd.concat([pd.read_csv(f) for f in files], ignore_index=True)

print(df_all.head())
```

> 💡 `ignore_index=True` 會重新編號 index（避免重複索引）

這樣只要資料夾中新增一個 `sales_apr.csv`，程式就會自動讀入，**不用再手動改檔名！**

---

## 💻 範例 3：遞迴搜尋（含子資料夾）

假設你的資料夾結構如下：

```
data/
  jan/sales_jan.csv
  feb/sales_feb.csv
  mar/sales_mar.csv
```

```python
files = glob.glob("data/**/*.csv", recursive=True)
print(files)
```

輸出：

```
['data/jan/sales_jan.csv', 'data/feb/sales_feb.csv', 'data/mar/sales_mar.csv']
```

---

## 💻 範例 4：結合 os.path 操作完整路徑

有時候我們只想取「檔名」或「資料夾名」，可以搭配 `os.path`：

```python
import os, glob

for file in glob.glob("data/*.csv"):
    filename = os.path.basename(file)   # 取得檔名
    folder = os.path.dirname(file)      # 取得資料夾
    print(f"{filename} 位於 {folder}")
```

---

## ⚡ 延伸應用（非常實用）

| 情境            | 寫法                                      |
| ------------- | --------------------------------------- |
| 找所有 JSON 檔    | `glob.glob("*.json")`                   |
| 找特定資料夾下的圖片    | `glob.glob("images/*.png")`             |
| 找所有子資料夾中的 CSV | `glob.glob("**/*.csv", recursive=True)` |
| 找名稱中包含日期的檔案   | `glob.glob("*2025*.csv")`               |

---

## 🧩 小練習

假設資料夾有：

```
data_2025_01.csv  
data_2025_02.csv  
data_2025_03.csv  
notes.txt
```

請你：

1. 使用 `glob` 找出所有 `.csv` 檔案。
2. 用 pandas 讀入所有檔案並合併。
3. 計算所有月份的平均銷售額（假設每個檔都有 `Amount` 欄位）。

---

## 📈 延伸挑戰（進階應用）

如果你想在讀入時，自動加上「月份欄位」：

```python
import pandas as pd
import glob

files = glob.glob("sales_*.csv")

df_list = []
for f in files:
    month = f.split("_")[1].replace(".csv", "")  # 例如 jan / feb
    df = pd.read_csv(f)
    df["Month"] = month
    df_list.append(df)

df_all = pd.concat(df_list, ignore_index=True)
print(df_all.head())
```

這樣就能追蹤每筆資料來自哪個月份，非常適合分析「月度趨勢」📊！

---

是否要我幫你接續到 **第4天課程（資料視覺化入門）**，帶你用這些清理好的資料畫圖？
