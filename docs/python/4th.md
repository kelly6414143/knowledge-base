# 🗓️ 第4天：資料視覺化入門（Matplotlib + Seaborn）

## 🎯 學習目標

1. 了解為什麼視覺化是資料分析的重要步驟。
2. 學會使用 `matplotlib` 與 `seaborn` 畫出基本圖表。
3. 能夠從數據快速觀察趨勢與異常。

---

## 🧠 核心知識講解

### 🔸 為什麼要做資料視覺化？

* 一張圖能比幾百行數據更快揭示規律。
* 對外報告、內部簡報、探索資料時都必備。
* 在資料科學工作流程中屬於「Exploratory Data Analysis (EDA)」階段。

> 💬 類比前端世界：
>
> * Chart.js、ECharts、D3.js → Python 世界的 matplotlib + seaborn
> * 你以前用 JSX + Canvas 畫圖；現在用 **Python + pandas** 自動生成。

---

## 💻 實作範例

### 第1步：載入套件與準備資料

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 建立模擬資料
data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
    "Revenue": [12000, 15000, 13000, 17500, 16000, 19000],
    "Cost": [8000, 9500, 9000, 11000, 10500, 11500]
}
df = pd.DataFrame(data)
df
```

---

### 第2步：基本折線圖（Line Chart）

```python
plt.plot(df["Month"], df["Revenue"], label="Revenue", marker='o')
plt.plot(df["Month"], df["Cost"], label="Cost", marker='s')

plt.title("Monthly Revenue vs Cost")
plt.xlabel("Month")
plt.ylabel("Amount (NTD)")
plt.legend()
plt.grid(True)
plt.show()
```

> 📈 折線圖（Line Chart）：適合觀察趨勢（如每月變化）。

---

### 第3步：長條圖（Bar Chart）

```python
plt.bar(df["Month"], df["Revenue"], color="skyblue")
plt.title("Revenue by Month")
plt.xlabel("Month")
plt.ylabel("Revenue")
plt.show()
```

> 📊 長條圖（Bar Chart）：適合比較不同類別間的數值。

---

### 第4步：使用 seaborn 增強美觀

```python
sns.set(style="whitegrid")  # 設定風格
sns.barplot(x="Month", y="Revenue", data=df, palette="viridis")

plt.title("Revenue Trend (Seaborn)")
plt.show()
```

---

### 第5步：散佈圖（Scatter Plot）觀察關聯

```python
sns.scatterplot(x="Cost", y="Revenue", data=df)
plt.title("Cost vs Revenue Relationship")
plt.show()
```

> 💡 用於觀察「變數之間的關係」，類似分析「廣告花費 vs 收入」。

---

### 第6步：快速統計視覺化（用於EDA）

```python
# 範例資料：學生分數
students = pd.DataFrame({
    "Name": ["Alice","Bob","Cindy","David","Ella","Frank"],
    "Score": [88, 92, 79, 95, 84, 91]
})

# 分布圖（Histogram）
sns.histplot(students["Score"], bins=5, kde=True)
plt.title("Score Distribution")
plt.show()
```

> 📊 分布圖（Histogram）可幫助發現是否偏態或有異常值。

---

## 🧩 練習任務（20分鐘）

請建立一份銷售資料（或使用昨天的 `sales.csv`），包含：

```
Month, Product, Sales
Jan, A, 1200
Jan, B, 800
Feb, A, 1600
Feb, B, 900
Mar, A, 2000
Mar, B, 1100
```

請完成以下：

1. 繪製每月總銷售額（折線圖）
2. 繪製不同產品的銷售對比（長條圖）
3. 嘗試在圖表上加上標題、座標標籤、顏色主題


### 其他支線
- [聚合 (Aggregation) - Group By 分群聚合](../modules_methods/groupby.md)


---

## 📈 延伸挑戰（進階）

試著將多張圖表整合為「儀表板」：

```python
fig, axes = plt.subplots(1, 2, figsize=(10,4))
sns.barplot(x="Month", y="Sales", data=df, ax=axes[0])
sns.lineplot(x="Month", y="Sales", data=df, ax=axes[1])
plt.tight_layout()
plt.show()
```

> 🧩 這樣的圖表可直接放入報告或自動生成分析報表。
