# Q&A

## 影響語意搜尋是否準確為以下:

1. Embedding 實際內容
2. Query 的 embedding
3. TopK
4. Chunks 是否包含能被模型理解的語意
5. 召回後 AI 怎麼整理

## 語意搜尋的流程

```
(文件 text) → Embedding → [Vector] → 儲存到 Vector DB
      ↑                                       |
      |                                       ↓
   Query → Embedding → [Query Vector] → 相似度比對 → Top-K 結果
```
