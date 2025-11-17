# Group By 分群聚合

---

## ✅ 範例資料 - 將相同月份的金額加總後畫折線圖

假設你有以下 DataFrame：

```python
import pandas as pd

data = {
    "Month": ["Jan", "Jan", "Feb", "Feb", "Mar", "Mar"],
    "Product": ["A", "B", "A", "B", "A", "B"],
    "Sales": [1200, 800, 1600, 900, 2000, 1100]
}

df = pd.DataFrame(data)
print(df)
```

輸出：

```
  Month Product  Sales
0   Jan       A   1200
1   Jan       B    800
2   Feb       A   1600
3   Feb       B    900
4   Mar       A   2000
5   Mar       B   1100
```

---

## 🧩 第1步：用 `groupby()` 加總同月份的 Sales

```python
monthly_sum = df.groupby("Month", as_index=False)["Sales"].sum()
print(monthly_sum)
```

輸出結果：

```
  Month  Sales
0   Feb   2500
1   Jan   2000
2   Mar   3100
```

> 💡 `groupby("Month")`：依月份分群
> `["Sales"].sum()`：對每組的 Sales 欄位加總
> `as_index=False`：保留欄位名稱而不是設成索引

---

## 🧩 第2步：依月份排序（可選）

若月份是文字（Jan, Feb, Mar...），想按照順序排序：

```python
order = ["Jan", "Feb", "Mar", "Apr", "May", "Jun"]
monthly_sum["Month"] = pd.Categorical(monthly_sum["Month"], categories=order, ordered=True)
monthly_sum = monthly_sum.sort_values("Month")
```

---

## 💻 第3步：繪製折線圖（matplotlib）

```python
import matplotlib.pyplot as plt

plt.plot(monthly_sum["Month"], monthly_sum["Sales"], marker='o', color='teal')
plt.title("Monthly Total Sales")
plt.xlabel("Month")
plt.ylabel("Total Sales (NTD)")
plt.grid(True)
plt.show()
```

輸出圖表：
📈 一條顯示每月總銷售額變化的折線。

---

## 💻 第4步：用 seaborn 畫更美的版本

```python
import seaborn as sns
sns.set(style="whitegrid", palette="muted")

sns.lineplot(x="Month", y="Sales", data=monthly_sum, marker="o")
plt.title("Monthly Total Sales (Seaborn)")
plt.show()
```

> `seaborn` 會自動加上平滑的線條與統一風格。

---

## 🧩 延伸應用：若想同時顯示產品別趨勢

如果你想要顯示「各產品在每月的趨勢」：

```python
sns.lineplot(x="Month", y="Sales", hue="Product", data=df, marker="o")
```

效果：

* 一條線代表一個產品
* `hue="Product"` 幫你自動分色分組

---

## ✅ 小結

| 操作     | 語法                                   | 說明            |
| ------ | ------------------------------------ | ------------- |
| 加總同月份  | `df.groupby("Month")["Sales"].sum()` | 聚合資料          |
| 保留欄位格式 | `as_index=False`                     | 不將 Month 變成索引 |
| 排序月份   | `pd.Categorical(..., ordered=True)`  | 保持月份順序        |
| 折線圖    | `plt.plot()` / `sns.lineplot()`      | 顯示趨勢變化        |
