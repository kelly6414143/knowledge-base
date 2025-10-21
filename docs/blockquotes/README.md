# 引用區塊（blockquotes）

- [引用區塊（blockquotes）](#引用區塊blockquotes)
  - [模擬訊息框](#模擬訊息框)
    - [使用 引用區塊 (blockquotes) 搭配 emoji 或圖示模擬訊息框](#使用-引用區塊-blockquotes-搭配-emoji-或圖示模擬訊息框)
    - [支援 HTML 的 Markdown（例如 MkDocs、VitePress、Docsify）](#支援-html-的-markdown例如-mkdocsvitepressdocsify)
  - [同一個引用區塊中斷行](#同一個引用區塊中斷行)
    - [使用兩個空白 + Enter](#使用兩個空白--enter)
    - [用 `<br>` 明確插入換行](#用-br-明確插入換行)
    - [用空白行「段落式分隔」](#用空白行段落式分隔)

## 模擬訊息框

### 使用 引用區塊 (blockquotes) 搭配 emoji 或圖示模擬訊息框

> ✅ 適合：GitHub README、普通 Markdown 檔

```markdown
> ℹ️ **資訊提示：**  
> 這是一般資訊提示的內容，可在 GitHub 上正確顯示。

> ⚠️ **警告：**  
> 使用前請確認設定是否正確。

> ✅ **成功：**  
> 設定已完成！
```

🔹 顯示效果：

> ℹ️ **資訊提示：**  
> 這是一般資訊提示的內容，可在 GitHub 上正確顯示。

> ⚠️ **警告：**  
> 使用前請確認設定是否正確。

> ✅ **成功：**  
> 設定已完成！

---

### 支援 HTML 的 Markdown（例如 MkDocs、VitePress、Docsify）

> ✅ 適合：工程化文件網站、內部知識庫（如 MkDocs）

```markodwn
<div style="border-left: 4px solid #2196F3; background: #E3F2FD; padding: 0.75em 1em;">
<strong>ℹ️ 資訊：</strong>
這是使用 HTML 製作的訊息框。
</div>
```

🔹 顯示效果：

<div style="border-left: 4px solid #2196F3; background: #E3F2FD; padding: 0.75em 1em;color:#222">
<strong>ℹ️ 資訊：</strong>  
這是使用 HTML 製作的訊息框。
</div>

---

## 同一個引用區塊中斷行

### 使用兩個空白 + Enter

> ℹ️ 標準 Markdown 換行法

```markdown
> 這是第一行。  
> 這是第二行。
```

> 📘 重點：
>
> - 第一行結尾要加「兩個空白」
> - 再按 Enter 進入下一行時仍需加上 >
> - 保持每行前面都有 >

🔹 顯示效果：

> 這是第一行。  
> 這是第二行。

---

### 用 `<br>` 明確插入換行

> ℹ️ HTML 標籤

```markdown
> 這是第一行。<br>
> 這是第二行。
```

🔹 顯示效果：

> 這是第一行。<br>
> 這是第二行。

> 💡 備註：  
> 這個方法最穩定，適用於所有 Markdown 引擎（GitHub、MkDocs、Obsidian、Notion 等）。

---

### 用空白行「段落式分隔」

```markdown
> 這是第一段。
>
> 這是第二段。
```

> 📘 用途：  
> 如果想在同一個引用框內分開兩段文字（類似 paragraph），可用這種方式。
