# 🎨 matplotlib 全面解析

## 🎯 一、matplotlib 是什麼？

`matplotlib` 是 **Python 的核心資料視覺化套件**。
幾乎所有進階圖表工具（如 `seaborn`、`pandas.plot()`、`plotly`）的底層都依賴它。

> 💬 一句話理解：
> `matplotlib` 就像 Python 的「Canvas」或「Chart.js」，
> 你可以用它**從零繪出各種類型的圖表**。

---

## 🧠 二、用途與應用場景

| 類型        | 用途         | 常見圖表                  |
| --------- | ---------- | --------------------- |
| **趨勢分析**  | 看數值隨時間變化   | 折線圖 (Line Chart)      |
| **比較分析**  | 比不同群組的大小   | 長條圖 (Bar Chart), 水平條圖 |
| **分布分析**  | 看數據分布與集中程度 | 直方圖 (Histogram), KDE  |
| **關聯分析**  | 看兩變數的關係    | 散佈圖 (Scatter Plot)    |
| **構成分析**  | 比例、佔比      | 圓餅圖 (Pie Chart)       |
| **多維視覺化** | 多變數組合      | Subplots, 多軸圖         |

---

## 🧩 三、matplotlib 架構理解（核心概念）

> 🧱 結構邏輯類比：
> HTML → `<canvas>`
> React → `render()`
> matplotlib → `Figure` + `Axes`

```plaintext
Figure：整個圖表的畫布（Canvas）
Axes：畫布上的一張圖（subplot）
Axis：每個圖上的 X/Y 軸
```

### 範例結構：

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()  # 建立畫布與軸
ax.plot([1, 2, 3, 4], [10, 20, 15, 25])  # 畫線
ax.set_title("Example Plot")
ax.set_xlabel("X Axis")
ax.set_ylabel("Y Axis")
plt.show()
```

---

## 💻 四、常用圖表類型與語法

### 1️⃣ 折線圖 Line Chart

顯示趨勢變化。

```python
plt.plot([1,2,3,4], [10,20,15,25], color='blue', linestyle='--', marker='o')
plt.title("Monthly Growth")
plt.xlabel("Month")
plt.ylabel("Revenue")
plt.show()
```

🔹 參數說明：

* `color`: 顏色 (ex: `'blue'`, `'#FF5733'`)
* `linestyle`: 線型 (`'-'`, `'--'`, `':'`)
* `marker`: 標記形狀 (`'o'`, `'s'`, `'^'`)

---

### 2️⃣ 長條圖 Bar Chart

比較類別之間的數值。

```python
labels = ['A', 'B', 'C']
values = [30, 55, 70]
plt.bar(labels, values, color='skyblue')
plt.title("Product Sales")
plt.show()
```

> 📊 類似前端的 `<BarChart>` 組件，適合分類資料比較。

---

### 3️⃣ 直方圖 Histogram

顯示數值分布情況。

```python
import numpy as np
data = np.random.normal(100, 15, 200)
plt.hist(data, bins=10, color='orange', edgecolor='black')
plt.title("Score Distribution")
plt.xlabel("Score")
plt.ylabel("Frequency")
plt.show()
```

> 🎯 常用於分析成績分布、年齡層、價格範圍等。

---

### 4️⃣ 散佈圖 Scatter Plot

分析變數間關聯。

```python
x = [1,2,3,4,5]
y = [10,12,20,25,40]
plt.scatter(x, y, color='green', s=100)
plt.title("Cost vs Revenue")
plt.xlabel("Cost")
plt.ylabel("Revenue")
plt.show()
```

> 💡 若點呈現明顯斜率 → 代表變數之間有關聯。

---

### 5️⃣ 圓餅圖 Pie Chart

看比例或結構。

```python
sizes = [40, 35, 25]
labels = ["Product A", "Product B", "Product C"]
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=140)
plt.title("Market Share")
plt.show()
```

> 📈 適合顯示佔比資訊（例如市場份額）。

---

### 6️⃣ 多圖組合 (Subplots)

在同一畫面展示多張圖。

```python
fig, axs = plt.subplots(1, 2, figsize=(10,4))

axs[0].bar(["A","B","C"], [10,15,7])
axs[0].set_title("Bar Chart")

axs[1].plot([1,2,3], [3,2,5])
axs[1].set_title("Line Chart")

plt.tight_layout()
plt.show()
```

---

## 🧠 五、圖表美化技巧

| 功能 | 函式                            | 範例                          |
| -- | ----------------------------- | --------------------------- |
| 標題 | `plt.title()`                 | `plt.title("Sales Report")` |
| 標籤 | `plt.xlabel() / plt.ylabel()` | `plt.xlabel("Month")`       |
| 圖例 | `plt.legend()`                | `plt.legend(["A","B"])`     |
| 網格 | `plt.grid(True)`              | `plt.grid(alpha=0.3)`       |
| 顏色 | `color` 參數                    | `color="tomato"`            |
| 大小 | `figsize`                     | `plt.figure(figsize=(6,4))` |

---

## 🧩 六、與 pandas 整合使用

pandas DataFrame 直接內建 `.plot()` 方法，其實底層就是 `matplotlib`！

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "Month": ["Jan","Feb","Mar","Apr"],
    "Revenue": [12000,15000,13000,17000]
})

df.plot(x="Month", y="Revenue", kind="line", marker='o')
plt.title("Revenue Trend")
plt.show()
```

> 📊 pandas + matplotlib 是最常見組合，用一行即可畫圖。

---

## 🧩 七、進階：雙軸圖與樣式設定

### 雙軸圖（左右兩邊各一個軸）

```python
fig, ax1 = plt.subplots()

ax2 = ax1.twinx()
ax1.plot(df["Month"], df["Revenue"], color='blue', label='Revenue')
ax2.plot(df["Month"], df["Cost"], color='red', label='Cost')

ax1.set_xlabel("Month")
ax1.set_ylabel("Revenue", color='blue')
ax2.set_ylabel("Cost", color='red')
plt.title("Revenue vs Cost")
plt.show()
```

---

## 🧩 八、整體思維：從資料到圖像的流程

```plaintext
1️⃣ 取得資料 (pandas / numpy)
2️⃣ 清理與整理 (DataFrame)
3️⃣ 選擇適合圖表類型
4️⃣ 用 matplotlib 畫圖
5️⃣ 美化與調整
6️⃣ 儲存 / 展示結果
```

---

## 💾 九、輸出圖表

```python
plt.savefig("report_chart.png", dpi=300, bbox_inches="tight")
```

> 可直接匯出高解析度圖表用於報告或簡報。

---

## 📈 十、延伸學習：Seaborn 與 Plotly 的比較

| 套件             | 特點           | 適合情境             |
| -------------- | ------------ | ---------------- |
| **matplotlib** | 基礎、靈活、客製性高   | 精細控制圖表細節         |
| **seaborn**    | 美觀、快速、整合統計功能 | 資料探索與報表          |
| **plotly**     | 互動式、網頁友好     | Dashboard、Web可視化 |

---

## ✅ 小結

| 重點                          | 說明                  |
| --------------------------- | ------------------- |
| matplotlib 是 Python 的「繪圖引擎」 | 所有進階圖表套件都建立在它上面     |
| 適用於靜態圖表與報告輸出                | 尤其是探索分析（EDA）階段      |
| 搭配 pandas 可快速產出圖形           | `df.plot()` 即為最方便入口 |
