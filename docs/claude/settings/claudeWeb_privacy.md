# Claude 網頁版逐步操作

> 操作步驟
>
> 1. `Settings → Privacy`：關掉 **Model Improvement**
> 2. 新對話右上角點 **鬼魂圖示**：開 **Incognito chat**
> 3. `Settings → Capabilities`：關掉 **Search and reference chats**
> 4. `Settings → Capabilities`：Pause 或 Reset **Memory**

## 一、你要控制的其實是 4 件事

Claude 網頁版和 App 目前和隱私最相關的控制，主要是：

1. 關閉 **Model Improvement / 模型改進資料使用**
2. 使用 **Incognito chat / 無痕聊天**
3. 關閉 **Search and reference chats / 搜尋過往對話**
4. 調整或關閉 **Memory / 記憶功能**

---

## 二、關閉資料用於模型改進

### 你要達成什麼

讓一般對話不要被用來幫助改進 Claude。官方說明中提到，你可以在隱私相關設定中調整這件事，且你保有控制權。

### 操作路徑

**Claude → Settings → Privacy / Privacy Settings → Model Improvement**

### 實際步驟

1. 打開 Claude 網頁版
2. 點左下角帳號區或設定入口
3. 進入 **Settings**
4. 找到 **Privacy** 或 **Privacy Settings**
5. 將 **Model Improvement** 關閉

### 你會看到什麼

會看到和隱私、資料使用相關的切換選項。官方支援文提到，你可以隨時調整 privacy 和 model improvement 設定。

### 注意

就算你開著 Model Improvement，**Incognito chats 仍不會被用來改進 Claude**。

---

## 三、開啟無痕聊天（最重要）

### 你要達成什麼

建立一個不進入聊天紀錄、也不進入記憶與過往聊天搜尋的對話。官方說明指出，無痕聊天不會儲存在 chat history，也不會被 Claude 用於搜尋過往聊天；同時也不會被用來改進 Claude。

### 操作路徑

**新對話畫面右上角 → 鬼魂圖示（ghost icon）**

### 實際步驟

1. 在 Claude 開一個新的非 project 對話
2. 看右上角是否有 **鬼魂圖示**
3. 點一下鬼魂圖示
4. 進入 **Incognito chat**

### 你會看到什麼

官方文件指出，在一般非 project 對話中，右上角會有 ghost icon；點下去就會開啟 incognito chats。

### 這個模式的效果

-- 不會存到 chat history。
-- Claude 不會把它納入 memory。
-- Claude 不會從這些對話中搜尋先前內容。
-- 不會被用於改進 Claude。

### 注意

如果你是 **Team / Enterprise** 帳號，官方說明指出 incognito chats 仍可能遵循組織的資料保留與匯出政策。

---

## 四、關閉「搜尋過往對話」

### 你要達成什麼

避免 Claude 在新對話中自動引用舊對話內容。

### 操作路徑

**Settings → Capabilities → Preferences → Search and reference chats**

### 實際步驟

1. 進入 **Settings**
2. 打開 **Capabilities**
3. 找到 **Preferences**
4. 將 **Search and reference chats** 關閉

### 你會看到什麼

官方文件明確寫到，可以到 `Settings > Capabilities`，在 Preferences 區塊把 **Search and reference chats** 關掉。

### 關閉後效果

Claude 不會再從你過去的對話中抓資料來延續上下文。

---

## 五、關閉或重設記憶功能

### 你要達成什麼

避免 Claude 根據你的聊天建立長期偏好或工作記憶。

### 操作路徑

**Settings → Capabilities → Memory**

### 實際步驟

1. 進入 **Settings**
2. 點 **Capabilities**
3. 找到 **Memory**
4. 你可以：
   - 關閉或暫停記憶
   - 使用 **Pause memory**
   - 使用 **Reset memory**

### 三個差別

-- **Memory 開啟**：Claude 可根據聊天建立記憶。
-- **Pause memory**：保留既有記憶，但不再使用或新增新記憶。
-- **Reset memory**：永久刪除所有記憶，包含 project memories。

### 補充

官方也指出，你可以在 `Settings > Capabilities` 裡看到並編輯 memory summary。

---

## 六、最實用的隱私組合

## 情境 A：你要貼公司機密

建議這樣做：

1. 開 **Incognito chat**
2. 關閉 **Model Improvement**
3. 不要把完整憑證、密碼、金鑰貼進去

官方支援文也直接提醒，對於財務資訊、醫療資料、密碼、機密商業文件，仍應謹慎處理。

## 情境 B：你不想 Claude 記得你過去的工作內容

建議這樣做：

1. 關閉 **Search and reference chats**
2. 關閉或 Pause **Memory**
3. 敏感對話改用 **Incognito chat**

## 情境 C：你只是偶爾有一段敏感內容

最省事做法：

1. 不必全域改設定
2. 直接新開 **Incognito chat** 即可。
