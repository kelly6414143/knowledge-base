# 選取相同y軸 多游標（Multi-Caret / Column Selection）

## 1️⃣ 垂直同一欄位（真正的 Y 軸選取）

例如：

```ts
t("view.online");
t("view.offline");
t("view.pending");
```

你想同時選取：

```
online
offline
pending
```

### 🖥 Windows

👉 **Alt + Shift + 滑鼠拖曳**

或

👉 **Alt + Shift + Insert**（切換 Column Mode）

### 🍎 macOS

👉 **Option + Shift + 滑鼠拖曳**

---

# 2️⃣ 選取「相同字串」的多處位置（更常用）

例如整個檔案都有：

```ts
"view.online";
```

### 🖥 Windows

👉 把游標放在字上
👉 **Alt + J**（選取下一個相同字）

👉 **Ctrl + Alt + Shift + J**（一次全選全部相同）

### 🍎 macOS

👉 **Ctrl + G**（選下一個）
👉 **Ctrl + ⌘ + G**（全選）

---

## 🔥 3️⃣ 最強用法（前端專案超常用）

如果你只是想「每一行相同位置插入東西」：

例如：

```ts
online;
offline;
pending;
```

想變成：

```ts
t("view.online");
t("view.offline");
t("view.pending");
```

👉 用 Column Selection
👉 在最前面打 `t('view.`
👉 在最後面補 `')`

效率直接起飛 🚀

---

# 建議你用哪個？

依你做 i18n 的情境：

- 批量改 key → 用 **Alt + J**
- 垂直對齊改結構 → 用 **Column Mode**
