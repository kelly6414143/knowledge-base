# PaddleOCR

`PaddleOCR` 是一個基於 PaddlePaddle 的 OCR（光學字符識別）工具，支持多種語言的文本識別。它提供了簡單易用的 API 和豐富的預訓練模型，方便用戶快速集成 OCR 功能。

```
圖片 (png / jpg)
   ↓
PaddleOCR
   ↓
文字 + 座標 + 順序
   ↓
清洗 / 結構化
   ↓
RAG / 搜尋 / 文件生成

```

## 作用

1️⃣ 文字偵測（Text Detection）

> 圖片中「哪些地方是文字？」

- 像在照片中畫出一個一個框框

- 告訴你「這一塊是文字區」

📦 常見模型：DBNet

2️⃣ 文字辨識（Text Recognition）

> 框起來的文字「實際內容是什麼？」

- 把框內圖片 → 轉成文字

- 支援 中 / 英 / 日 / 韓 / 數字 / 符號

📦 常見模型：CRNN、SVTR

3️⃣ 版面與結構（可選但很重要）

> 哪個是標題？哪個是表格？順序是什麼？

- 對文件、表格、UI 截圖特別有用

- 可搭配 layout / table 模型

## 安裝

> 升級 pip（避免安裝時出怪問題）
>
> ```
> python -m pip install --upgrade pip
> ```

安裝到系統環境：

```
pip install paddlepaddle
pip install paddleocr
```

安裝到 venv：

```
路徑\.venv\Scripts\python.exe -m pip install --upgrade pip
路徑\.venv\Scripts\python.exe -m pip install paddlepaddle paddleocr
```

[範例]:  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install --upgrade pip  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install paddlepaddle paddleocr

## 驗證 是否可用

```
路徑\.venv\Scripts\python.exe -c "from paddleocr import PaddleOCR; print('PaddleOCR OK')"
```

[範例]:  
D:\local-llm\ocr\.venv\Scripts\python.exe -c "from paddleocr import PaddleOCR; print('PaddleOCR OK')"

## 用 venv 的 python 執行

```
D:\local-llm\ocr\.venv\Scripts\python.exe D:\local-llm\ocr\ocr_paddle.py D:\local-llm\flow.png
```

## PPStructureV3

`PPStructureV3` 是一個基於 PaddleOCR 的文檔結構識別模型，旨在提高文檔分析和理解的準確性。它可以識別文檔中的各種結構元素，如標題、段落、表格等，並提供相應的位置信息。

> 升級 pip（避免安裝時出怪問題）
>
> ```
> python -m pip install --upgrade pip
> ```

## 安裝

安裝到系統環境：

```
pip install paddlepaddle
pip install paddleocr
pip install opencv-python
```

安裝到 venv：

```
路徑\.venv\Scripts\python.exe -m pip install --upgrade pip
路徑\.venv\Scripts\python.exe -m pip install paddleocr opencv-python
路徑\.venv\Scripts\python.exe -m pip install "paddlex[ocr]==[paddlex的version]"
```

> 如何取得 paddlex 的 version  
> D:\local-llm\ocr\.venv\Scripts\python.exe -c "import paddlex; print(paddlex.\_\_version\_\_)"

[範例]:  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install --upgrade pip  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install paddleocr opencv-python

## 驗證 是否可用

```
路徑\.venv\Scripts\python.exe -c "from paddleocr import PPStructureV3; print('PPStructureV3 OK')"
```

[範例]:  
D:\local-llm\ocr\.venv\Scripts\python.exe -c "from paddleocr import PPStructureV3; print('PPStructureV3 OK')"

## 用 venv 的 python 執行

```
D:\local-llm\ocr\.venv\Scripts\python.exe D:\local-llm\ocr\ppstructure_export_v3.py --image "D:\local-llm\prototypes\derived\screenshots\player\存款／優惠稽核.section_01.存
款稽核點.png" --out "D:\local-llm\out\test.blocks.json"
```
