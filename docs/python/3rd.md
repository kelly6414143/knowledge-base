# 🗓️ 第3天：用 pandas 進行資料清理（Data Cleaning）

## 🎯 學習目標

1. 了解為什麼資料清理是資料分析的關鍵步驟。
2. 學會處理缺失值（NaN）、重複值、資料格式不一致等問題。
3. 能夠用 pandas 清理與轉換資料，使其可用於分析或機器學習。

---

## 🧠 核心知識講解

### 🔸 為什麼資料清理這麼重要？

在真實世界中，資料常常是「髒」的：

* 缺少資料（空白、NaN、NULL）
* 格式不一致（字串 / 數字混雜）
* 重複紀錄、異常值（outlier）
* 不同來源需要合併（merge / join）

> 💬 類比前端經驗：
>
> * 清理資料就像處理「後端回傳不一致的 JSON」。
> * 你不會直接丟進畫面，而是先格式化、驗證、轉換。
> * pandas 就是幫你做「資料格式清理」的強力工具。

---

## 💻 實作範例

### 第1步：建立模擬資料集

```python
import pandas as pd
import numpy as np

data = {
    "Name": ["Alice", "Bob", "Cindy", "David", None, "Bob"],
    "Age": [25, 30, None, 35, 28, 30],
    "Score": [88, 92, np.nan, 95, 81, 92]
}

df = pd.DataFrame(data)
print("原始資料：")
print(df)
```

---

### 第2步：處理缺失值 (Missing Values)

```python
# 檢查是否有缺失值
print(df.isnull().sum())

# 1️⃣ 移除含有缺失值的列
cleaned_df = df.dropna()
print(cleaned_df)

# 2️⃣ 用平均值或固定值補缺
df.fillna({"Score":df["Score"].mean()}, inplace=True)
df.fillna({"Age":0}, inplace=True)
df.fillna({"Name":"Unknown"}, inplace=True)
print(df)
```

---

### 第3步：移除重複值

```python
print("去除重複前：", len(df))
df = df.drop_duplicates()
print("去除重複後：", len(df))
```

---

### 第4步：格式轉換與欄位處理

```python
# 將欄位名稱統一小寫
df.columns = df.columns.str.lower()

# 轉換欄位型別
df["age"] = df["age"].astype(int)

# 新增一欄位 (資料轉換)
df["level"] = df["score"].apply(lambda x: "A" if x >= 90 else "B")
print(df)
```

---

### 第5步：合併與拆分資料（merge / concat）

```python
# 建立第二個 DataFrame
extra = pd.DataFrame({
    "name": ["Alice", "Bob", "Ella"],
    "city": ["Taipei", "Kaohsiung", "Taichung"]
})

merged = pd.merge(df, extra, on="name", how="left")
print(merged)
```

`how` 參數類似 SQL JOIN：

* `inner`：交集（兩邊都有的資料）
* `left`：保留左表全部資料
* `outer`：全部合併（缺的補 NaN）

---

## 🧩 練習任務（20分鐘）

建立一個 `sales.csv`（模擬銷售資料）：

```csv
Customer,Amount,Date
Alice,1200,2025-01-01
Bob,,2025-01-02
Cindy,900,2025-01-03
Alice,1200,2025-01-01
,700,2025-01-04
David,1500,
```

請完成以下操作：

1. 用 pandas 讀取 CSV。
2. 將空白值補上（缺少 Customer → `"Unknown"`，缺少 Amount → 平均值）。
3. 移除重複列。
4. 新增欄位 `Tax = Amount * 0.05`。
5. 輸出成乾淨版 `clean_sales.csv`。

**Google Colab 練習位置：**  
[Colab連結：1st.pythonLearning](https://colab.research.google.com/drive/16MIWFxtt1L9parhNKACKb8GhE5rvUwjA#scrollTo=pjLtFaZGKMLF)

---

## 📈 延伸挑戰（進階）

嘗試將多個 CSV 檔案合併，例如：

* `sales_jan.csv`
* `sales_feb.csv`

使用：

```python
import glob

files = glob.glob("sales_*.csv")
df_all = pd.concat([pd.read_csv(f) for f in files])
```

> 💡 小技巧：
> 若要快速檢查資料品質，可使用：
>
> ```python
> df.info()
> df.describe()
> df.nunique()
> ```

> 了解更多 [glob 模組](../modules/glob.md)