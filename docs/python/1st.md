## Python 資料分析入門（Day 1）

**日期**：2025-10-24  
**來源**：自學課程《AI 資料科學家全方位學程》— Python 資料分析基礎  
**關聯主題**：#Python #資料分析 #AI入門 #前端轉職AI #Colab #pandas #numpy  

---

### 📘 學習摘要

**課程定位**：  
針對已有前端（JavaScript + React）背景的工程師，設計的「資料科學家速成路線」。  
重點在於從語法轉換出發，快速進入能用 Python 做資料分析與 AI 專案的階段。

**🎯 學習目標：**  
1. 理解 Python 與 JavaScript 的差異與思維轉換。  
2. 掌握 Python 基本語法與資料結構（list、dict、tuple）。  
3. 能使用 Jupyter Notebook 或 Google Colab 撰寫程式並執行輸出。

**🧠 核心概念：**
- **Python 為資料導向語言**，生態系完整且廣泛應用於 AI 領域。  
- 常用套件：
  - `pandas`：資料處理神器（如 Excel + JS object）
  - `numpy`：數學與矩陣運算
  - `matplotlib` / `seaborn`：資料視覺化
  - `scikit-learn`、`tensorflow`、`pytorch`：機器學習與深度學習框架

> 💡 心法對比  
> 前端偏向事件驅動與即時互動；  
> 資料科學偏向批次資料運算與邏輯分析。

**💻 實作重點範例：**
- 建立變數與資料結構（list、dict、tuple）  
- 使用 `for` 與 `if` 進行條件判斷  
- 使用 list comprehension（Python 版 map/filter）

**範例程式：**
```python
fruits = ["apple", "banana", "mango"]
for fruit in fruits:
    if fruit == "banana":
        print("🍌 是香蕉！")
    else:
        print(f"🥝 這是 {fruit}")
````

**Google Colab 練習位置：**  
[Colab連結：1st.pythonLearning](https://colab.research.google.com/drive/16MIWFxtt1L9parhNKACKb8GhE5rvUwjA#scrollTo=pjLtFaZGKMLF)

**JS&PY差異**  

> 建立變數  
> 
> **JS** 
> ```=javascript 
> const a = 20 
> ```
> **PY** 
> ```=python 
> a = 20 
> ```

> 打印內容  
> 
> **JS** 
> ```=javascript 
> console.log('123') 
> console.log(a) 
> ```
> **PY** 
> ```=python 
> print("123") 
> print(f"{a}") 
> ```

> List、Tuple、Dict 基本操作  
> 
> **JS** 
> ```=javascript 
> const fruits = ["apple", "banana", "mango"] 
> const person = {name: "Kelly", job: "Frontend Engineer"}  
> const grades = [90,85.88]
> ```
> **PY** 
> ```=python 
> fruits = ["apple", "banana", "mango"] 
> person = {"name": "Kelly", "job": "Frontend Engineer"} 
> grades = (90, 85, 88) 
> print(fruits[0])      # apple
> print(person["job"])  # Frontend Engineer
> print(sum(grades)/len(grades))
> ```

> for loop + if 條件判斷  
> 
> **JS** 
> ```=javascript 
> for fruit in fruits {
>   if(fruit === "banana"){
>     console.log("🍌 是香蕉！")
>   }else{
>     console.log(f"🥝 這是 {fruit}")
>   }
> }
> ```
> **PY** 
> ```=python 
> for fruit in fruits:
>    if fruit == "banana":
>        print("🍌 是香蕉！")
>    else:
>        print(f"🥝 這是 {fruit}")
> ```

> 練習 list comprehension（Python 的「map/filter」）  
> 
> **JS** 
> ```=javascript 
> const upper_fruits = fruits.map(f=> {
>    if(f != "banana"){
>       return f.uppertocase()
>    }else{
>       return f 
>    }
>   }
> )
> ```
> **PY** 
> ```=python 
> upper_fruits = [f.upper() for f in fruits if f != "banana"]
> print(upper_fruits)
> ```

---

### 📈 延伸挑戰：進階前端思維轉換

| JavaScript                               | Python                                       |
| ---------------------------------------- | -------------------------------------------- |
| `const arr = [1,2,3].map(x => x*2)`      | `arr = [x*2 for x in [1,2,3]]`               |
| `obj = {a:1, b:2}`<br>`Object.keys(obj)` | `obj = {"a":1, "b":2}`<br>`list(obj.keys())` |
| `for(let i=0; i<5; i++)`                 | `for i in range(5):`                         |

---

### 💡 其他說明與應用

* 作為前端工程師，最大的轉換在於「思維重心」：
  從「即時互動」轉為「資料邏輯與批次運算」。
* 對比 JavaScript，我更能感受到 Python 的語意化與資料結構的簡潔性。
* 接下來可嘗試將舊有的 JS 陣列操作或 API 資料處理邏輯改寫成 Python，
  練習思維轉換並熟悉語法。

---

### 🔗 延伸學習

* [Google Colab 線上練習環境](https://colab.research.google.com)
* 延伸閱讀：

  * 《Python for Data Analysis》by Wes McKinney
  * pandas 官方文件：[https://pandas.pydata.org/docs/](https://pandas.pydata.org/docs/)
  * Kaggle「Python 基礎」課程：[https://www.kaggle.com/learn/python](https://www.kaggle.com/learn/python)