# Python venv

```
root/
├─ .venv/
│  └─ Scripts/
│     ├─ activate.bat
│     └─ python.exe

```

## 現在用的是哪一個 Python

```
where python
```

## 建立 venv

```
python -m venv .venv
```

會生成 `root/.venv`

## 啟用 venv

PowerShell:

```
.venv\Scripts\Activate.ps1
```

Cmd:

```
.venv\Scripts\activate.bat
```

## 停用 venv

Cmd:

```
deactivate
```
