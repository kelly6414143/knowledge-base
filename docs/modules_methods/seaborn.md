# 🌊 Seaborn 全面解析：用最少程式碼畫出最漂亮的統計圖

---

## 🎯 一、Seaborn 是什麼？

`Seaborn` 是基於 **matplotlib** 的高階視覺化套件，
它提供了 **更美觀的樣式**、**更高層次的統計圖表 API**，
讓你可以用幾行程式碼就完成原本需要數十行 `matplotlib` 才能畫出的圖。

> 💬 一句話理解：
> Seaborn = Matplotlib + Pandas + 統計美學。

---

## 🧠 二、Seaborn 的用途與優勢

| 特點                        | 說明                         |
| ------------------------- | -------------------------- |
| ✅ 美觀預設樣式                  | 不需手動設定顏色、格線、字型             |
| ✅ 與 pandas DataFrame 無縫整合 | 直接使用欄位名稱作為 x、y             |
| ✅ 內建統計功能                  | 自動畫出平均值、信賴區間、分布曲線          |
| ✅ 豐富的圖表種類                 | 支援 20+ 統計圖（散佈圖、箱型圖、熱力圖...） |
| ✅ 一行搞定複雜圖表                | 適合資料探索分析（EDA）              |

---

## 💻 三、安裝與基本設定

```python
!pip install seaborn
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
```

設定主題樣式（推薦一開始設定）：

```python
sns.set(style="whitegrid", palette="muted", font_scale=1.1)
```

---

## 📊 四、常見圖表與用途

---

### 1️⃣ **散佈圖（Scatter Plot）**

觀察兩變數間關係。

```python
df = sns.load_dataset("tips")  # 內建範例資料集
sns.scatterplot(x="total_bill", y="tip", data=df)
plt.title("Tip vs Total Bill")
plt.show()
```

> 💡 類似 matplotlib 的 `plt.scatter()`，但更簡潔。
> 可輕鬆加上顏色分類：

```python
sns.scatterplot(x="total_bill", y="tip", hue="sex", style="time", data=df)
```

---

### 2️⃣ **折線圖（Line Plot）**

觀察時間序列或趨勢變化。

```python
sns.lineplot(x="size", y="tip", data=df)
```

> Seaborn 自動加上**平均線與信賴區間 (confidence interval)**。

```python
sns.lineplot(x="size", y="tip", data=df, ci=95)
```

---

### 3️⃣ **長條圖（Bar Plot）**

比較分類資料的平均值。

```python
sns.barplot(x="day", y="total_bill", data=df)
```

> 自動顯示每類的平均值與誤差線。
> 顏色分類版：

```python
sns.barplot(x="day", y="total_bill", hue="sex", data=df)
```

---

### 4️⃣ **箱型圖（Box Plot）**

觀察資料的分布、極端值（outlier）。

```python
sns.boxplot(x="day", y="total_bill", data=df)
```

> 📦 可快速看到中位數、四分位距、異常值。
> 類似統計課常見的「箱形圖」。

---

### 5️⃣ **小提琴圖（Violin Plot）**

結合箱型圖 + 分布圖，顯示資料密度。

```python
sns.violinplot(x="day", y="total_bill", data=df)
```

> 🎻 比箱型圖更豐富，適合比較群體之間的分布形狀。

---

### 6️⃣ **熱力圖（Heatmap）**

觀察矩陣資料或變數關聯。

```python
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap")
plt.show()
```

> 💡 熱力圖是資料探索階段的必備工具，用於發現變數關聯性。

---

### 7️⃣ **分布圖（Histogram / KDE）**

看資料的分布狀態。

```python
sns.histplot(df["total_bill"], bins=10, kde=True, color="skyblue")
```

> `kde=True` 可畫出平滑的機率密度曲線。

---

### 8️⃣ **配對圖（Pair Plot）**

一次比較所有變數的兩兩關係。

```python
sns.pairplot(df, hue="sex")
```

> 📈 EDA 常用利器，能快速發現哪些變數之間呈線性關係。

---

### 9️⃣ **分類資料分布（Count Plot）**

顯示每類資料出現次數。

```python
sns.countplot(x="day", data=df)
```

> 類似 JS 中的 histogram，但針對分類欄位（非連續數值）。

---

## 🎨 五、風格與主題設定

Seaborn 提供多種主題樣式：

```python
sns.set_style("whitegrid")  # 其他選項：darkgrid, white, dark, ticks
```

改變顏色風格：

```python
sns.set_palette("pastel")  # 可選：deep, bright, colorblind, muted
```

改變圖表尺寸：

```python
sns.set_context("talk")  # 其他選項：paper, notebook, poster
```

---

## 🧩 六、搭配 pandas 使用（最常見組合）

```python
import pandas as pd

sales = pd.DataFrame({
    "Month": ["Jan","Feb","Mar","Apr"],
    "Revenue": [12000,15000,13000,17000],
    "Category": ["A","B","A","B"]
})

sns.barplot(x="Month", y="Revenue", hue="Category", data=sales)
plt.title("Monthly Sales by Category")
plt.show()
```

> 📊 pandas 提供資料結構，seaborn 提供視覺語法。
> 這組合幾乎是 EDA 的標準搭檔。

---

## 🧠 七、Seaborn 與 Matplotlib 的關係

| 功能   | Matplotlib | Seaborn       |
| ---- | ---------- | ------------- |
| 調整細節 | 手動設定       | 自動美化          |
| 程式碼量 | 較多         | 較少            |
| 統計功能 | 無          | 內建平均與誤差線      |
| 適用情境 | 客製報表、複雜控制  | 快速分析、EDA、報告輸出 |

> 💡 建議實務工作中：
>
> * EDA 初期 → 用 **Seaborn** 快速觀察資料分布。
> * 報告呈現 → 用 **Matplotlib** 微調樣式、字型、標籤。

---

## 🧩 八、綜合範例：視覺化完整分析流程

```python
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset("tips")

plt.figure(figsize=(12,8))

# 上半部：收入 vs 星期
plt.subplot(2,2,1)
sns.barplot(x="day", y="total_bill", data=df, hue="sex")

# 下半部：小費 vs 金額
plt.subplot(2,2,2)
sns.scatterplot(x="total_bill", y="tip", hue="time", size="size", data=df)

# 第三張：分布情況
plt.subplot(2,2,3)
sns.histplot(df["tip"], kde=True)

# 第四張：變數關聯
plt.subplot(2,2,4)
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="coolwarm")

plt.tight_layout()
plt.show()
```

這幾乎就是一個小型的「自動化資料分析報告」。

---

## 📈 九、延伸工具與進階學習建議

| 套件                       | 功能      | 特點               |
| ------------------------ | ------- | ---------------- |
| **Plotly**               | 互動式視覺化  | 適合 Web Dashboard |
| **Altair**               | 宣告式視覺語法 | 結構清晰、整合 Jupyter  |
| **Seaborn + Matplotlib** | 靜態統計圖   | EDA 與報告最常用組合     |

---

## ✅ 小結

| 重點                       | 說明                 |
| ------------------------ | ------------------ |
| Seaborn 建立在 matplotlib 上 | 更高層次 API、美觀、簡潔     |
| 適合探索性資料分析 (EDA)          | 一行畫出統計圖表           |
| 與 pandas 無縫整合            | 可直接使用 DataFrame 欄位 |
| 可與 matplotlib 結合微調樣式     | 完成專業級圖表輸出          |

