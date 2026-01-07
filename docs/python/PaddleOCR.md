# PaddleOCR

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
```

安裝到 venv：

```
路徑\.venv\Scripts\python.exe -m pip install --upgrade pip
路徑\.venv\Scripts\python.exe -m pip install paddlepaddle paddleocr
```

[範例]:  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install --upgrade pip  
D:\local-llm\ocr\.venv\Scripts\python.exe -m pip install paddlepaddle paddleocr

## 用 venv 的 python 執行

```
D:\local-llm\ocr\.venv\Scripts\python.exe D:\local-llm\ocr\ocr_paddle.py D:\local-llm\flow.png

```
