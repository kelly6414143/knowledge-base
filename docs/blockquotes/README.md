# 引用區塊（blockquotes）

- [引用區塊（blockquotes）](#引用區塊blockquotes)
  - [模擬訊息框](#模擬訊息框)
    - [使用 引用區塊 (blockquotes) 搭配 emoji 或圖示模擬訊息框](#使用-引用區塊-blockquotes-搭配-emoji-或圖示模擬訊息框)
    - [支援 HTML 的 Markdown（例如 MkDocs、VitePress、Docsify）](#支援-html-的-markdown例如-mkdocsvitepressdocsify)
  - [同一個引用區塊中斷行](#同一個引用區塊中斷行)
    - [使用兩個空白 + Enter](#使用兩個空白--enter)
    - [用 `<br>` 明確插入換行](#用-br-明確插入換行)
    - [用空白行「段落式分隔」](#用空白行段落式分隔)
  - [進階技巧](#進階技巧)
    - [1. 在 MkDocs / VitePress / Docsify 自訂樣式](#1-在-mkdocs--vitepress--docsify-自訂樣式)
    - [2. 使用 Admonition 插件或短碼（shortcodes）](#2-使用-admonition-插件或短碼shortcodes)
    - [3. 可存取性（Accessibility）建議](#3-可存取性accessibility建議)
    - [4. 折疊內容（Collapsible block）和進階互動](#4-折疊內容collapsible-block和進階互動)
    - [5. 嵌套引用與列表混用](#5-嵌套引用與列表混用)
    - [6. GitHub 與靜態網站兼容性清單](#6-github-與靜態網站兼容性清單)
    - [7. 常見問題（Gotchas）與解法](#7-常見問題gotchas與解法)
    - [8. 實用範例集合(可折疊)](#8-實用範例集合可折疊)

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

---

## 進階技巧

以下為實務上常用的進階技巧與注意事項，包含在不同靜態網站生成器與 GitHub 上的相容性、可存取性建議，以及實用的範例片段。

### 1. 在 MkDocs / VitePress / Docsify 自訂樣式

如果文件站點支援 HTML 或自訂 CSS，可以使用帶 class 的容器，然後在站點樣式表中定義顏色與 icon。例如：

```markdown
<div class="kb-admonition kb-admonition-info">
<p><strong>ℹ️ 提示：</strong> 這是自訂樣式的訊息框。</p>
</div>
```

對應的 CSS（放在站點的 stylesheet）示例：

```css
.kb-admonition {
  border-left: 4px solid #2196f3;
  padding: 0.75em 1em;
  background: #f3f9ff;
  color: #222;
}
.kb-admonition-info {
  border-color: #2196f3;
}
.kb-admonition-warning {
  border-color: #ff9800;
  background: #fff3e0;
}
```

註：不要在 GitHub README 中依賴這些自訂 CSS；GitHub 不會載入站點的 CSS。但在工程化站點（MkDocs、VitePress）中，這能提供一致的視覺風格。

### 2. 使用 Admonition 插件或短碼（shortcodes）

許多文件工具（例如 MkDocs 的 mkdocs-material、Hugo、VitePress）提供 admonition 或 note/alert 內建或插件機制。優先使用這些功能可以讓內容更語意化、可被 TOC/搜尋辨識，並自動套用樣式。

範例（mkdocs-material）：

```markdown
!!! note "ℹ️ 資訊"
這是使用 admonition 的內容，會由主題自動格式化。
```

### 3. 可存取性（Accessibility）建議

- 為重要訊息提供語意化標題（例如用粗體前綴或使用 `<strong>`），以利螢幕閱讀器閱讀。
- 避免僅使用顏色來表示訊息類型；同時加入 icon 或文字標籤（Info/Warning/Error）。
- 若使用可折疊區塊，選擇 `details`/`summary` 標籤，並確保 keyboard 可操作：

```markdown
<details>
<summary>更多說明（按 Enter 或空白鍵以展開）</summary>

這是詳細內容。

</details>
```

### 4. 折疊內容（Collapsible block）和進階互動

使用原生 HTML 的 `details` / `summary` 可以在大多數現代瀏覽器與靜態站點上正常工作。但在 GitHub 的某些渲染情況下，樣式可能不同。若要在站點中加入動畫或記住展開狀態，需在站點 JavaScript 中處理。

### 5. 嵌套引用與列表混用

當在引用區塊內使用列表或其他區塊（code、表格）時，確保每行都加上 `>`，或使用縮進來維持結構。範例如下：

````markdown
> - 項目一
> - 項目二
>
> 1. 有序一
> 2. 有序二

> ```bash
> echo "程式碼在引用內"
> ```
````

注意：某些 Markdown 引擎對混合縮排的容錯性不同，必要時使用 HTML 容器以保證佈局。

### 6. GitHub 與靜態網站兼容性清單

- GitHub: 支援基本 blockquote、`details`、內嵌 HTML（有限）。不支援站點自訂 CSS。
- MkDocs / VitePress / Hugo: 支援自訂 CSS、admonition 插件、shortcodes。建議利用主題提供的警示/卡片元件。

### 7. 常見問題（Gotchas）與解法

- 換行無效：記得在行尾加兩個空白或使用 `<br>`。
- 列表消失或縮排錯亂：檢查 `>` 是否存在於每一行的開頭，或改用 HTML 容器。
- 圖示在純文字環境顯示為方塊：避免完全依賴 emoji 做為唯一的語意標記，提供文字備註。

### 8. 實用範例集合(可折疊)

- 站點友好的 admonition（mkdocs-material）：

```markdown
!!! tip "✅ 小技巧"
使用 `>` 或 `admonition` 皆可，但在工程文件站點上使用 `admonition` 可取得更一致的視覺呈現。
```

- 可折疊的 Q&A：

```markdown
<details>
<summary>問：如何在 blockquote 中換行？</summary>

答：最穩定的方式是加兩個空格後換行，或使用 `<br>`。

</details>
```
