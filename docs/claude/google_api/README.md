# GOOGLE API

可以，取得 **Google Sheets API** 通常不是去「下載一個 API」，而是做這 4 件事：

1. 建立或選擇一個 **Google Cloud 專案**
2. 在專案中 **啟用 Google Sheets API**
3. 建立 **憑證**
4. 把憑證給你的程式使用 ([Google支援][1])

---

## 先選：你要用哪種方式存取 Sheet

### 情境 A：讀你自己的 Google Sheet

最常用的是 **OAuth 2.0 Client ID**。
適合：

- 你自己登入後讀取自己的 Sheet
- 本機工具 / CLI / 桌面程式
- 測試階段先快速打通流程

Google 的 Sheets Quickstart 也是先教這條路：先設定 OAuth consent screen，再建立 Desktop app 的 OAuth client。([Google for Developers][2])

### 情境 B：讓腳本或後端自動讀取 Sheet

常用 **Service Account**。
適合：

- 自動化腳本
- 後端服務
- 不想每次手動登入授權

Service account 需要在 Google Cloud 建立，並下載金鑰給程式使用。([Google for Developers][3])

## 我建議你現在先用哪個

依你目前是在做：

- 本地專案
- Claude Code 輔助
- 想先把 Google Sheet 內容拉進來

我建議你**先用 OAuth 2.0 Desktop app**，比較容易成功。
等流程跑順後，再考慮改成 Service Account。

## 取得 Google Sheets API 的實際步驟

### 方式一：OAuth 2.0（推薦你先用）

#### 第 1 步：建立 Google Cloud 專案

到 Google Cloud Console，建立一個新專案，或選既有專案。這是 API 與憑證的容器。([Google支援][1])

#### 第 2 步：啟用 Google Sheets API

進入：
**APIs & Services → Library**
搜尋 **Google Sheets API**
按 **Enable**。([Google支援][1])

#### 第 3 步：設定 OAuth consent screen

進入：
**Google Auth platform**
先完成 App name、Audience、Data Access 等基本設定。Quickstart 明確要求先做這一步。([Google for Developers][2])

#### 第 4 步：建立 OAuth Client ID

進入：
**Google Auth platform → Clients**
按 **Create Client**
選 **Desktop app**
建立後下載 JSON 憑證檔。Google 的 Node.js Quickstart 建議把它存成 `credentials.json`。([Google for Developers][4])

#### 第 5 步：在程式中使用這個憑證

你的 Node.js 或 Python 程式會用這個 `credentials.json` 啟動授權流程；第一次執行時會開啟登入授權，授權完成後就能讀取你的 Google Sheet。這是官方 quickstart 的標準流程。([Google for Developers][4])

### 方式二：Service Account（之後可升級）

#### 第 1 步：建立 Google Cloud 專案

同上。([Google支援][1])

#### 第 2 步：啟用 Google Sheets API

同上。([Google支援][1])

#### 第 3 步：建立 Service Account

進入：
**IAM & Admin → Service Accounts**
建立一個 service account。([Google for Developers][3])

#### 第 4 步：建立金鑰

為這個 service account 建立金鑰，通常下載 **JSON**。Google 文件有說這類憑證是 public/private key pair。([Google for Developers][3])

#### 第 5 步：把目標 Google Sheet 分享給這個 service account

把 service account 的 email 加到 Google Sheet 的分享名單，至少給 Viewer。
否則就算 API 與金鑰都正確，還是讀不到資料。這是實務上最常漏掉的一步；這點雖然不是上面搜尋結果的主段落重點，但屬於 Google Workspace/API 的標準存取模型。

## OAuth 和 Service Account 怎麼選

### 先用 OAuth，如果你：

- 是自己在本機開發
- 只是先做 POC
- 目前由你本人操作 Google Sheet

### 用 Service Account，如果你：

- 想做自動排程
- 想在伺服器上跑
- 想避免每次登入授權

## 你目前最適合的最小路線

我建議你現在直接走這條：

1. 建一個 Google Cloud 專案
2. 啟用 Google Sheets API
3. 設定 OAuth consent screen
4. 建立 **Desktop app** 類型的 OAuth Client
5. 下載 `credentials.json`
6. 再讓 Claude Code 幫你寫一支 Node.js 小腳本去讀指定 Sheet

這是最省事的起手式。([Google for Developers][2])

## 你之後在 Claude Code 裡可以怎麼下指令

等你拿到 `credentials.json` 後，可以對 Claude Code 說：

```text
請幫我用 Node.js 建立一支讀取 Google Sheets 的腳本。

需求：
1. 使用 OAuth 2.0 Desktop app 憑證
2. 憑證檔名為 credentials.json
3. 讀取指定 spreadsheetId 與工作表範圍
4. 先把資料印出成 JSON
5. 後續我要再把它轉成禪道草稿輸入格式
```

## 注意

### 1. API Key 不是你的首選

Google 文件有 API key 的建立方式，但對 Google Sheets 這種需要存取使用者資料的情境，通常不夠用；你多半需要 OAuth 或 service account。([Google for Developers][5])

### 2. 憑證要保密

不管是 OAuth client secret 還是 service account JSON，都不要上傳到 GitHub。Google 也建議對 API key / 憑證做限制與安全管理。([Google支援][6])

## 遇到的問題

### 權限問題: 錯誤 403：access_denied

這個錯誤**多半不是程式碼本身壞掉**，而是 **OAuth 設定端**有一項沒對到。
你這個 `403: access_denied` 在你目前情境下，最常見是這 3 種原因：

1. **OAuth consent screen 還在 Testing，但你的 Google 帳號沒有被加到 Test users**
2. **User type / Audience 設成 Internal，結果你使用的帳號不在該組織內**
3. **Client 類型建錯了，腳本用的是 localhost 流程，但憑證不是對應的 Desktop app / 正確 client**

#### 先直接給你最可能的答案

如果你是自己本機測試，**最先檢查「Test users」**。

Google 官方說明很明確：
如果 OAuth consent screen 的 **User type 是 External**，而且目前還是 **Testing**，就必須在 **Audience → Test users** 裡把要登入授權的 email 加進去，否則會被拒絕。

#### 你現在先照這個順序檢查

##### 1. 檢查 OAuth consent screen 的 Audience / Test users

到 Google Cloud Console：

**Google Auth platform → Audience**

看這幾項：

- **User type** 是不是 `External`
- **Publishing status** 是不是 `Testing`
- **Test users** 裡面有沒有你現在拿來登入授權的 Google 帳號

如果是 `External + Testing`，你必須把自己的 Gmail 加到 **Test users**。

你要怎麼修

把你現在實際登入的 Google 帳號加進去，例如：

- `xxx@gmail.com`

加完後等幾分鐘，再重新跑授權流程。

##### 2. 檢查是不是選成 Internal

如果你的 OAuth app 設成 **Internal**，那只有該 Google Workspace 組織內的帳號可以使用；若你現在拿的是一般個人 Gmail，或不是同組織帳號，就會被擋。Google Help 對 `403 org_internal` 有明確說明。

你要怎麼修

如果你只是自己測試，通常設成：

- **External**
- 再把自己加進 **Test users**

##### 3. 檢查 OAuth Client 類型是不是建對

你錯誤訊息裡有：

- `redirect_uri=http://localhost`
- `flowName=GeneralOAuthFlow`

這表示你的腳本正在走本機回呼的 OAuth 流程。
對這種本機 CLI / 桌面流程，應使用適合的 OAuth client 類型；Google 對桌面/原生應用有專門的 OAuth 流程說明。

#### 你要怎麼判斷

看你下載的 `credentials.json` 裡面，常見會有兩種結構：

##### 若是 Desktop app

通常會看到類似：

```json
{
  "installed": {
    ...
  }
}
```

#### 若是 Web application

通常會看到類似：

```json
{
  "web": {
    ...
  }
}
```

如果你的 Claude Code 腳本是照 **桌面 CLI / 本機授權** 的寫法，但你建立的是 **Web application** client，常會出現授權流程對不起來的問題。
反過來也一樣。

你要怎麼修

如果你現在是：

- 在本機 PowerShell 跑腳本
- 讓瀏覽器跳授權
- 再回到本機 localhost

那我建議你重新建立一個 **Desktop app** 的 OAuth Client，然後把新的 `credentials.json` 換掉試一次。
Google 的 Sheets Quickstart 也是先從建立對應的 OAuth client 開始。

[1]: https://support.google.com/googleapi/answer/6158841?hl=en&utm_source=chatgpt.com "Enable and disable APIs - API Console Help"
[2]: https://developers.google.com/workspace/sheets/api/quickstart/go?utm_source=chatgpt.com "Go quickstart | Google Sheets"
[3]: https://developers.google.com/workspace/guides/create-credentials?utm_source=chatgpt.com "Create access credentials | Google Workspace"
[4]: https://developers.google.com/workspace/sheets/api/quickstart/nodejs?utm_source=chatgpt.com "Node.js quickstart | Google Sheets"
[5]: https://developers.google.com/workspace/sheets/api/quickstart/js?utm_source=chatgpt.com "JavaScript quickstart | Google Sheets"
[6]: https://support.google.com/googleapi/answer/6310037?hl=en&utm_source=chatgpt.com "Best practices for securely using API keys"
[7]: https://support.google.com/cloud/answer/13461325?hl=en&utm_source=chatgpt.com "Submitting your app for verification"
