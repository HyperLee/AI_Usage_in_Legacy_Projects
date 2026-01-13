# AI 導入專案前期設定

- 我預設 AI 工具是 `GitHub Copilot`

## 設定檔指引

對於一個新 / 舊專案 我會加入下面的操作.

1. 參考 `project-init.prompt.md` 檔案

- 產生 `.gitignore`
- 產生 `.editorconfig`
- 修改 `.editorconfig` 以強制程式碼風格
- 加入 startDebugging 設定 (這部分是要在 VS Code 中使用的, 如果不使用這套 IDE 可以忽略)

2. `.github` 資料夾加入 `agents/instructions/prompts` 相關檔案

- agents
  - code-review.agent.md
  - CSharpExpert.agent.md
- instructions
  - csharp.instructions.md
- prompts
  - create-readme.prompt.md

對於上述檔案, 可以根據個人喜好來做增減但是 csharp.instructions.md 建議一定要加入, 這樣 AI 在分析程式碼時會比較準確.
如果不知道有那些範本可以參考, 可以到 `https://github.com/github/awesome-copilot/tree/main` 找尋相關資源.

## 優化 `csharp.instructions.md` 檔案

`csharp.instructions.md` 這檔案必須要根據專案需求來做調整, 主要是針對專案的程式碼風格, 命名規則, 架構設計等做說明.
這隻檔案可以說是 Rule 的概念, 把你想要的規範都寫進去, 這樣 AI 在分析程式碼時才會比較準確.
簡單作法可以參考我目前檔案內容, 放到專案中 接著開啟對話視窗選擇比較聰明的模型比如 `Claude Opus 4.5`
接著對 AI 說 " 請參考 `.github/agents/instructions/csharp.instructions.md` 檔案內容, 來當作範本, 幫我依據目前專案寫法與規範來幫我更新這份檔案 "
簡單說當你沒有想法或是不知道如何開始就使用我的檔案來當作範本, 接著讓 AI 根據目前專案內容檔案風格等等來幫你優化這份檔案內容.
當 AI 完成之後, 請務必自己再閱讀一次, 確保內容是你想要的規範, 如果有需要可以再手動調整.
這份檔案初期會有一段磨合期, 需要不斷的調整與優化, 才能達到你想要的效果.
instructions.md 檔案不需要人工呼叫使用, AI 會自動參考.

上述的檔案我是基於 .Net Core 10, c# 14 來當作範本, 對於這份檔案我也是調整很長時間才找出目前比較滿意的版本.
我有個專案是 .netFramework 版本然後版本還特別低, 我會特別加入如下 AI 產出來的 Code 比較滿意.
不然常常會遇到非 .NET Framework 4.0 的語法被使用, 導致無法相容的問題.

---

## 技術環境需求

- **開發框架**: ASP.NET WebForm (.NET Framework 4.0)
- **C# 語言版本**: C# 4.0
- **前端技術**: HTML5、JavaScript、jQuery
- **資料庫**: Microsoft SQL Server
- **連線字串**: 使用既有 `conn` 連線配置
- **相容性要求**: 須完全相容現有 C# 4.0 專案架構，不可破壞現有功能

## 重要開發準則

### 1. 程式碼風格與命名規範

- **函式命名**: 遵循 PascalCase 命名慣例 (如: `BindCountyDropDownList`)
- **變數命名**: 使用 camelCase (如: `countyID`)
- **控制項命名**: 使用有意義的前綴 (如: `ddl` 代表 DropDownList、`tb` 代表 TextBox)
- **避免衝突**: 檢查現有方法名稱，確保不產生命名衝突
- **註解規範**: 為所有新增方法提供詳細的 XML 文件註解

### 2. C# 4.0 語法相容性 (嚴格遵守)

```csharp
// ❌ 禁用語法
var result = GetData();                              // 禁用 var 關鍵字
string message = $"Hello {name}";                    // 禁用字串插值
string value = obj?.ToString();                      // 禁用 null-conditional operators
await SomeMethodAsync();                             // 禁用 async/await
List<string> items = new() { "A", "B" };            // 禁用目標型別 new 運算式

// ✅ 正確語法
DataTable result = GetData();                        // 明確型別宣告
string message = string.Format("Hello {0}", name);   // 使用 string.Format
string value = (obj != null) ? obj.ToString() : string.Empty;  // 明確 null 檢查
List<string> items = new List<string>() { "A", "B" };  // 完整型別宣告
```

### 3. 程式碼修改原則

- **保持功能一致**: 修改後的程式行為必須與原有程式完全一致
- **向下相容**: 不可破壞現有功能或影響其他相依模組
- **最小化影響**: 僅修改指定區塊程式碼，不改動其他邏輯
- **保留註解**: 保留原有的重要註解，協助理解程式脈絡
- **錯誤處理**: 保持與現有程式碼相同的 try-catch-finally 結構

### 4. 資料庫存取規範

- 使用 `SqlConnection` 搭配 `ConfigurationManager` 讀取連線字串
- 使用 `SqlDataAdapter` 進行資料查詢
- 使用參數化查詢 (`AddWithValue`) 防止 SQL Injection
- 確保連線物件在 `finally` 區塊中正確關閉
- 設定適當的 `CommandTimeout` (現有設定為 180 秒)

---

如果想看我舊版本的可以再提出, 由於有些檔案比較敏感就不放到網路上了避免爭議
`csharp.instructions.md` 檔案建議寫英文, AI 讀取英文比較厲害, 其餘檔案就隨意了.

## prompts 與 agents 檔案說明

這邊是需要手動呼叫的, 所以可以依據個人想使用的功能來決定要加入那些檔案.
`create-readme.prompt.md`, 我個人有寫檔案需求, 所以我會使用這個檔案來制定一些規範給 AI 來幫我產生 README.md 檔案.
`code-review.agent.md`, 這個檔案是用來做程式碼審查的, 可以協助你找出程式碼中的問題與優化建議.
`CSharpExpert.agent.md`, 這個檔案是用來當作 C# 專家助手, 可以協助你解決 C# 相關的問題與需求.
其實網路上的資源很多, 可以從頭自己寫也可以參考網路範本使用.
我提供出來得檔案都是我已經使用過的版本.

## 日常如何使用 AI 開發

日常開發步驟大概如下,
SA 會提供 `專案需求書` 裡面會說明客戶大概想要的樣子與功能.
但是基本上這檔案需求書通常都很粗略, 需要我們開發人員再進一步細化需求.
有些點糊糊不清的地方, 以及可能漏洞就需要再與 SA 確認避免事後認知不同.
當規格書確認完畢之後, 就可以開始寫開發規格書.
第一版我都是手動寫, 寫完看過沒問題之後再請 AI 協助優化.
我會對 AI 說 `file:xxx.prompt.md 這是我的大綱, 幫我完善規格書內容. 只需要調整內容先不用實作開發.`
接著 AI 會根據需求書內容來幫我產生一份比較完整的開發規格書.
AI 很會寫規格文件, 所以這部分可以多多利用 AI 的優勢來幫助你完成.
當 AI 產完之後一定要在自己看過一次內容, 確保沒有問題之後再進行開發.

`提醒大家AI不是你, 所以她不會知道你在想什麼以及要什麼, 所以一開始寫的大綱最好是把你知道的以及想要的都寫清楚`
這就是所謂的上下文 context, 讓 AI 能夠根據這些資訊來幫你產生你想要的內容.
上下文足夠多, AI 才能幫你產生比較符合你需求的內容.
不要幻想一句話就能搞定整個專案, 這是不可能的事情.

當規格書確認沒問題就可以交給 AI 來開發.
如果大家 AI 工具的高級請求每個月都用不完的話可以都使用比較聰明的模型來開發.
但是如果額度都不夠的話可以考慮寫規格書的時候使用比較聰明的模型, 開發的時候使用比較便宜的模型來開發. 來節省一些成本.
我個人是使用 `Claude Opus 4.5` 來寫規格書, 開發的時候使用 `Claude Sonnet 4.5` 來開發.
如果是需求都很簡單的話那我就會使用 `Raptor mini`

AI 產完程式碼之後務必要自己再看過一次, AI 產完是 AI 的程式碼, 不是你的程式碼.
請務必自己再看過一次, 確保沒有問題之後再進行提交與驗證.

以上是針對新舊專案的一些設定與使用的個人使用習慣說明,
如果想針對 AI 如何使用這就是另一個議題了.
可以先參考 Trello 上面的`資源共享區` 我有放了數個關於 GitHub Copilot 與 AI 使用的資源連結.
