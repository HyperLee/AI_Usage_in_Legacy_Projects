# AI 導入專案前期設定

- 我預設AI工具是 `GitHub Copilot`

## 設定檔指引

對於一個新/舊專案 我會加入下面的操作.
除非能確保該專案都沒有人使用過AI相關工具

1. 參考 `project-init.prompt.md` 檔案
- 產生 `.gitignore`
- 產生 `.editorconfig`
- 修改 `.editorconfig` 以強制程式碼風格
- 加入 startDebugging 設定 (這部分是要在VS Code中使用的, 如果不使用這套IDE可以忽略)

2. `.github` 資料夾加入 `agents/instructions/prompts` 相關檔案
- agents
  - code-review.agent.md
  - CSharpExpert.agent.md
- instructions
  - csharp.instructions.md
- prompts
  - create-readme.prompt.md 

對於上述檔案, 可以根據個人喜好來做增減但是 csharp.instructions.md 建議一定要加入, 這樣AI在分析程式碼時會比較準確.
如果不知道有那些範本可以參考, 可以到 `https://github.com/github/awesome-copilot/tree/main` 找尋相關資源.

## 優化 `csharp.instructions.md` 檔案
`csharp.instructions.md` 這檔案必須要根據專案需求來做調整,主要是針對專案的程式碼風格,命名規則,架構設計等做說明.
這隻檔案可以說是Rule的概念, 把你想要的規範都寫進去, 這樣AI在分析程式碼時才會比較準確.
簡單作法可以參考我目前檔案內容, 放到專案中 接著開啟對話視窗選擇比較聰明的模型比如 `Claude Opus 4.5` 
接著對AI說 "請參考 `.github/agents/instructions/csharp.instructions.md` 檔案內容,來當作範本, 幫我依據目前專案寫法與規範來幫我更新這份檔案"
簡單說當你沒有想法或是不知道如何開始就使用我的檔案來當作範本, 接著讓AI根據目前專案內容檔案風格等等來幫你優化這份檔案內容.
當AI完成之後, 請務必自己再閱讀一次, 確保內容是你想要的規範, 如果有需要可以再手動調整.
這份檔案初期會有一段磨合期, 需要不斷的調整與優化, 才能達到你想要的效果.
instructions.md 檔案不需要人工呼叫使用, AI會自動參考.

## prompts與agents檔案說明
這邊是需要手動呼叫的, 所以可以依據個人想使用的功能來決定要加入那些檔案.
`create-readme.prompt.md`, 我個人有寫檔案需求, 所以我會使用這個檔案來制定一些規範給AI來幫我產生README.md檔案.
`code-review.agent.md`, 這個檔案是用來做程式碼審查的, 可以協助你找出程式碼中的問題與優化建議.
`CSharpExpert.agent.md`, 這個檔案是用來當作C#專家助手, 可以協助你解決C#相關的問題與需求.
其實網路上的資源很多, 可以從頭自己寫也可以參考網路範本使用.
我提供出來得檔案都是我已經使用過的版本.



