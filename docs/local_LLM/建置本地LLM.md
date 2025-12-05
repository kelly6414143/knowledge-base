# 建置本地 LLM(Winodws+nodeJS)

<details>
<summary>提示詞</summary>
後續再增加
</details>

## 架構

```=arduino
Ollama（本地推論）
     ↑  ↓  localhost:11434
Node.js RAG Server
     ├─ ingest：文件 & Axure HTML → 切chunk → Embedding
     ├─ vectorDB：Chroma（Node版本）存向量
     ├─ ask：搜尋片段 + Prompt + LLM 回答
React 前端（可選）

```

## 偵測電腦是否能跑[7B / 8B]模型

提供資訊如下

```=yaml
CPU：Intel i7-12700H
GPU：NVIDIA RTX 3050 4GB
RAM：16GB
作業系統：Windows 11
```

## 下載 Ollama

> Ollama 是 LLM 模型管理工具  
> 就是一個讓你輕鬆下載、啟動、管理 AI 模型的工具。

到官網：https://ollama.com/download

> 注意
>
> - 安裝後 Ollama 會自動啟動
> - 系統托盤（右下角）會看到 Ollama 小圖示
> - 不需要你登入任何帳號、不需要 API key

安裝後在 PowerShell 輸入：

```
ollama --version
```

## 本地 LLM 建置

### 下載並運行模型（首次測試）

1. 開啟 PowerShell (系統管理員身分)
2. 輸入指令下載模型 (以 Qwen2.5 7B 為例)

   ```
   ollama run qwen2.5:7b
   ```

   你會看到畫面像這樣：

   ```
   pulling qwen2.5:7b...
   ...
   >>
   ```

3. 測試模型是否正常

   下載完成後，在 `>>` 後面輸入： `你好`

   如果你看到 AI 回覆，代表：本地 LLM 建置成功 🎉

### 測試 Ollama 的本地 API

> Ollama 內建一個 HTTP API：  
> `http://localhost:11434`

1. 在 PowerShell 輸入以下指令

```=powershell
Invoke-WebRequest `
-Uri "http://localhost:11434/api/generate" `
-Method POST `
-ContentType "application/json" `
-Body '{"model":"qwen2.5:7b","prompt":"API 測試"}'
```

執行後你會看到像這樣的 JSON 輸出，代表：LLM API 已經成功運作！🎉

```=arduino
{"model":"qwen2.5:7b","created_at":...,"response":"...."}
```

> PS: 可使用 **postman** 去驗證

### 使用 Node.js 呼叫本地 LLM

1. 新增一個資料夾  
   `local-llm-test`
2. 初始化 Node 專案  
   `npm init-y`
3. 安裝 axios  
   `npm install axios`
4. 建立第一支 Node.js LLM 呼叫程式
   - 建立檔案 `test-llm.js`，內容可以看代碼
   - 執行 `node test-llm.js`

### 本地 LLM API Server

1. 檔案 `package.json` 添加，`"type": "module"`
2. 安裝 `Express + CORS`
   ```=bash
   npm install express cors axios
   ```
3. 建立 `server.js`，內容可以看代碼
   - 啟動本地 API Server：`node server.js`

### 後續的/chat 相關 API，都可以在 postman 測試，以及增加前端畫面

## 在 Ollama 裝 embedding 模型

```
ollama pull nomic-embed-text
```

> 從 Ollama 官方庫下載 nomic-embed-text  
> 這是一顆專門用來做向量嵌入（embeddings）的模型  
> 下載完成後，/api/embeddings 就可以用它來算向量

確認是否存在

```
ollama list
```

---

### 其他

#### 整體架構（Windows + Node.js）

```
Ollama（本地推論）
     ↑  ↓  localhost:11434
Node.js RAG Server
     ├─ ingest：文件 & Axure HTML → 切chunk → Embedding
     ├─ vectorDB：Chroma（Node版本）存向量
     ├─ ask：搜尋片段 + Prompt + LLM 回答
React 前端（可選）

```

#### 專案結構（Node.js 版）

```
company-rag-node/
├─ data/
│  ├─ docs/               # 公司文件 txt/md/pdf（先支持 txt/md）
│  └─ prototypes/         # Axure HTML 原型（*.html）
├─ src/
│  ├─ ingest.ts           # 建索引
│  ├─ query.ts            # 查詢 & Prompt
│  ├─ htmlParser.ts       # 解析 Axure HTML
│  ├─ server.ts           # Express API /ask
│  ├─ vector.ts           # Chroma Client（Node 版）
│  └─ config.ts
├─ package.json
└─ tsconfig.json

```
