# Claude Code 隱私設定步驟

> 操作步驟
>
> 1. 進專案
> 2. 建 `.claude/settings.local.json`
> 3. 用 `permissions.deny` 擋 `.env`、secrets、憑證檔
> 4. 用 `/config` 檢查設定是否生效

## 一、先理解：Claude Code 的「隱私設定」是怎麼做的

Claude Code 不是只有一個叫做「隱私模式」的按鈕；它主要是透過 **設定檔** 來控制行為，例如限制可以讀哪些檔案、哪些工具可用、設定是套用在全域還是專案。官方也提供 `/config` 指令開啟設定介面。

你最常會用到的是這 3 種設定範圍，且優先順序由高到低為：

1. `.claude/settings.local.json`
2. `.claude/settings.json`
3. `~/.claude/settings.json`

### 這三種檔案差別

- `~/.claude/settings.json`：你的電腦全域設定，所有專案都會吃到。
- `.claude/settings.json`：專案共用設定，適合團隊一起遵守。
- `.claude/settings.local.json`：只在你本機生效，適合放個人隱私限制，而且通常不應提交到 Git。

---

## 二、最推薦的新手做法

如果你的目標是「不要讓 Claude Code 碰到敏感資料」，最實用的方式是：

### 做法 A：用本機私有設定檔擋掉敏感檔案

在你的專案根目錄建立：

```bash
.claude/settings.local.json
```

填入：

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./config/credentials.json)",
      "Read(./*.pem)",
      "Read(./*.key)"
    ]
  }
}
```

官方文件明確說明可以在 `settings.json` / `settings.local.json` 使用 `permissions.deny` 來阻擋特定工具或路徑；`Read(...)` 這種規則就是用來限制讀取。

### 這樣做的效果

Claude Code 在這個專案裡即使正常工作，也會被限制不能讀你列出的敏感檔案。

---

## 三、逐步操作版

## 步驟 1：進入你的專案資料夾

### 目的

先確保你是在正確的專案下設定隱私限制。

### 操作

在終端機輸入：

```bash
cd 你的專案路徑
```

例如：

```bash
cd D:\projects\my-react-app
```

### 預期會看到什麼

終端機目前路徑變成你的專案資料夾。

### 常見失敗原因

- 路徑打錯
- 資料夾不存在
- Windows 路徑有空白但未正確處理

---

## 步驟 2：建立 `.claude` 資料夾

### 目的

Claude Code 會從這裡讀專案層級設定。

### 操作

macOS / Linux：

```bash
mkdir -p .claude
```

Windows PowerShell：

```powershell
mkdir .claude
```

### 預期會看到什麼

專案底下多一個 `.claude` 資料夾。

### 常見失敗原因

- 已經有同名資料夾，其實可以忽略
- 不在專案根目錄

---

## 步驟 3：建立本機隱私設定檔

### 目的

讓這份設定只在你本機生效，避免不小心提交到版本控制。`.claude/settings.local.json` 的優先權也高於專案與全域設定。

### 操作

建立檔案：

```bash
.claude/settings.local.json
```

內容範例：

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./config/credentials.json)",
      "Read(./*.pem)",
      "Read(./*.key)"
    ]
  }
}
```

### 預期會看到什麼

檔案建立成功，之後 Claude Code 進入這個專案會吃到這份規則。官方文件說明 Claude Code 會依設定層級合併設定，且 local 優先。

### 常見失敗原因

- JSON 格式錯誤，例如少逗號或括號
- 檔名打成 `setting.local.json`
- 放錯位置，不是在專案根目錄的 `.claude` 裡

---

## 步驟 4：把這個檔案排除在 Git 之外

### 目的

避免你的本機隱私規則被提交出去。

### 操作

在 `.gitignore` 加入：

```gitignore
.claude/settings.local.json
```

### 預期會看到什麼

Git 不再追蹤這個檔案。

### 常見失敗原因

- `.gitignore` 放錯位置
- 檔案之前已被 Git 追蹤，需額外取消追蹤

---

## 步驟 5：用 `/config` 檢查設定是否生效

### 目的

官方文件提到你可以在 Claude Code 互動介面用 `/config` 開啟設定介面，查看目前狀態與修改配置。

### 操作

啟動 Claude Code 後輸入：

```text
/config
```

### 預期會看到什麼

會開啟 Claude Code 的設定介面，可檢查目前套用的設定來源與內容。

### 常見失敗原因

- 還沒進入 Claude Code REPL
- Claude Code 版本較舊
- 安裝異常

---

## 四、進階隱私建議

## 1. 不要開太寬的自動權限

官方在 VS Code 整合頁面提醒：若啟用自動編輯權限，Claude Code 可能修改像 `settings.json`、`tasks.json` 這類會被編輯器執行的設定檔；處理不受信任工作區時，應偏向手動批准並仔細檢查變更。

### 建議

- 對陌生專案先用「只分析、不修改」
- 先要求 Claude 提計畫，再決定是否批准修改
- 重要檔案先用 Git commit 或 stash 保護

## 2. 限制 MCP / 外部工具

Claude Code 可透過 MCP 連很多外部工具與資料源；若你不需要，應避免配置不必要的 MCP server。

## 3. 可用 hooks 擋高風險行為

官方 hooks 文件說明可以在 `PreToolUse` 時攔截並拒絕工具呼叫，例如阻擋危險命令或敏感檔案操作。

---

## 五、適合前端工程師的隱私範本

你是前端工程師的話，通常建議先擋這些：

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./.npmrc)",
      "Read(./pnpm-workspace.yaml)",
      "Read(./secrets/**)",
      "Read(./*.pem)",
      "Read(./*.key)",
      "Read(./ios/**/GoogleService-Info.plist)",
      "Read(./android/**/google-services.json)"
    ]
  }
}
```

這不是官方範例原文，而是依官方 `permissions.deny` 機制延伸出的實務建議；目的是保護 API key、憑證、Firebase 設定等常見敏感檔。支撐的設定能力來自官方 settings 文件。
