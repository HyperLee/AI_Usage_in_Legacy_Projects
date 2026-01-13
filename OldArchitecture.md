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
