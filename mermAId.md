# vscode-mermAId

## 說明

Exploration into Copilot Chat-powered Diagram Generation

> 輕量的 VS Code 擴充，用以示範如何透過 Copilot Chat 建立與調整 Mermaid 圖表。

---

## 主要功能 ✅

- 使用 Copilot Chat 指令快速建立 Mermaid 圖表（UML、循序圖等）。
- 即時修改目前顯示的 Mermaid 圖表。
- 示範整合 Copilot Chat 與 VS Code 圖表產生流程，適合教學與驗證概念。

## 快速開始 🚀

1. 在 VS Code 裡安裝套件：
   - 前往 Marketplace：[vscode-mermAId - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.copilot-mermaid-diagram)
2. 開啟 Copilot Chat 並啟用對話。
3. 在對話中使用下列指令：
   - `@mermAId /uml` — 建立類別圖 (UML)
   - `@mermAId /sequence` — 建立循序圖
   - `@mermAId /iterate` — 修改目前顯示的 Mermaid 圖表

> 提示：指令會在 Copilot Chat 介面觸發，並將產生的 Mermaid 程式碼嵌入或更新至目前編輯器檔案中。

## 範例

```text
@mermAId /uml
# -> 會回傳一段 Mermaid 類別圖程式碼，並在編輯器中顯示圖形
```

## 原始碼與回報問題 🔧

- GitHub Repository: [microsoft/vscode-mermAId](https://github.com/microsoft/vscode-mermAId)
- 若有問題或要回報 Bugs，請在上面的 repo 提出 Issue。

---

## 注意事項 ⚠️

- 這個專案屬於探索性質，可能需要特定版本的 Copilot Chat 或 VS Code 才能正常運作。
- 請參考原始專案的說明文件以取得最新相依與使用方式。

---

如果你要我再把此 README 翻成英文版本或加入更多使用範例，請告訴我想要的內容。
