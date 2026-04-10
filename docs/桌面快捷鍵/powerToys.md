# PowerToys

> PowerToys 是 Microsoft 提供的一組 Windows 工具，支援 Windows 10 與 Windows 11，其中包含 Always On Top，可把某個視窗固定在其他視窗上方。

可以，下面用 **Windows 電腦版** 角度，直接教你安裝與使用 PowerToys。

## PowerToys 是什麼

PowerToys 是 Microsoft 提供的一組 Windows 工具，支援 Windows 10 與 Windows 11，其中就包含你要的 **Always On Top**，可把某個視窗固定在其他視窗上方。([Microsoft Learn][1])

## 安裝方式

### 方式 1：用 Microsoft Store 安裝

這是最簡單的方式。

做法：

1. 開啟 **Microsoft Store**
2. 搜尋 **PowerToys**
3. 找到 **Microsoft PowerToys**
4. 按 **安裝**

Microsoft 官方文件也把 Microsoft Store 列為正式安裝方式之一。([Microsoft Learn][1])

---

### 方式 2：用 winget 安裝

如果你習慣用命令列，可以開啟 **PowerShell** 或 **命令提示字元**，輸入：

```powershell
winget install --id Microsoft.PowerToys --source winget
```

這是 Microsoft 官方提供的安裝指令。([Microsoft Learn][1])

---

### 方式 3：從 GitHub 下載安裝檔

官方也支援從 GitHub 發行頁下載安裝程式，常見檔名會是：

- `PowerToysSetup-...-x64.exe`
- `PowerToysSetup-...-arm64.exe`

一般多數 Windows 桌機/筆電大多選 **x64**。([Microsoft Learn][1])

---

## 安裝後怎麼開啟

安裝完成後：

1. 按鍵盤 **Win**
2. 搜尋 **PowerToys**
3. 開啟它

通常會看到左側一整排工具清單。

## 安裝後如何使用

1. 開啟 PowerToys
2. 左側找到 **Always On Top** 並啟用
3. 對著想固定的視窗按 **Win + Ctrl + T**
4. 再按一次取消

## 常見情況

### 1. 快捷鍵按了沒反應

先檢查：

- PowerToys 有沒有開啟
- Always On Top 模組有沒有啟用
- 快捷鍵有沒有被你改掉

### 2. 某些程式不能置頂

官方文件提到，**若目標視窗是用系統管理員權限開啟的程式**，PowerToys 可能也需要用系統管理員模式執行，才能對那個視窗生效。([Microsoft Learn][4])

例如像：

- 工作管理員
- 某些以管理員執行的工具
