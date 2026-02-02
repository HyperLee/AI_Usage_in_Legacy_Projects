# AI 導入專案前期設定

> **預設 AI 工具**: GitHub Copilot

本指南將協助你在新專案或既有專案中導入 AI 開發工具，透過標準化設定檔與 AI 指令檔案，提升開發效率與程式碼品質。

---

## 目錄

- [設定檔指引](#設定檔指引)
- [優化 csharp.instructions.md 檔案](#優化-csharpinstructionsmd-檔案)
- [Prompts 與 Agents 檔案說明](#prompts-與-agents-檔案說明)
- [Skills 技能檔案說明](#skills-技能檔案說明)
- [日常 AI 開發流程](#日常-ai-開發流程)
- [Copilot SDK - 客製化整合方案](#copilot-sdk---客製化整合方案)
- [參考資源](#參考資源)

---

## 設定檔指引

### 步驟 1: 基礎設定檔建立

參考 [project-init.prompt.md](project-init.prompt.md) 檔案，建立以下基礎設定：

| 設定檔 | 用途 | 優先級 |
|--------|------|--------|
| `.gitignore` | 排除不需要版控的檔案 | 必須 |
| `.editorconfig` | 統一程式碼風格 | 必須 |
| `.vscode/launch.json` | VS Code 偵錯設定 | 建議 |

> **提示**: 如果不使用 VS Code IDE，可以忽略 `startDebugging` 相關設定

---

### 步驟 2: AI 指令檔案結構

在專案根目錄建立 `.github` 資料夾，並依照以下結構組織檔案：

```
.github/
├── agents/
│   ├── code-review.agent.md
│   └── CSharpExpert.agent.md
├── instructions/
│   └── csharp.instructions.md
└── prompts/
    └── create-readme.prompt.md
```

#### 檔案用途說明

| 類型 | 檔案名稱 | 用途 | 是否必須 |
|------|----------|------|----------|
| **Instructions** | `csharp.instructions.md` | AI 分析程式碼的核心規則與規範 | ✅ 必須 |
| **Agents** | `code-review.agent.md` | 程式碼審查專用 Agent | 選用 |
| **Agents** | `CSharpExpert.agent.md` | C# 專家助手 Agent | 選用 |
| **Prompts** | `create-readme.prompt.md` | 文件產生提示範本 | 選用 |

> **重要**: `csharp.instructions.md` 強烈建議加入，這是 AI 準確分析程式碼的關鍵檔案。

---

### 取得範本資源

如果不確定如何撰寫這些檔案，可以參考以下資源：

- [GitHub Awesome Copilot](https://github.com/github/awesome-copilot/tree/main) - 官方範本庫
- 使用本專案提供的範本作為起點

---

## 優化 csharp.instructions.md 檔案

### 核心概念

`csharp.instructions.md` 是 AI 分析程式碼的**核心規則檔案**，需要根據專案特性進行客製化調整。

**檔案用途**:
- 定義專案的程式碼風格
- 規範命名規則
- 說明架構設計原則
- 設定語法限制（例如：C# 版本相容性）

### 優化步驟

#### 1. 使用 AI 協助優化

```plaintext
步驟流程：
1. 將範本檔案放入專案
2. 開啟對話視窗，選擇進階模型（Claude Opus 4.5 / GPT-5.2 Codex）
3. 輸入提示詞：
   "請參考 .github/instructions/csharp.instructions.md 檔案架構內容作為範本，
    根據目前專案的寫法與規範，幫我更新這份檔案. 先深度研究與思考再開始修改。"
4. AI 會根據專案程式碼風格產生優化建議
```

#### 2. 人工審查與調整

> **重要提醒**: AI 產生的內容僅供參考，必須由開發者親自審查確認！

- ✅ 檢查規範是否符合專案需求
- ✅ 確認語法限制是否正確
- ✅ 驗證命名規則是否一致
- ✅ 必要時手動調整細節

#### 3. 持續優化

這份檔案會經歷**磨合期**，需要在實際使用中不斷調整：

- 發現 AI 產生的程式碼不符合期望時，更新規則
- 專案架構變更時，同步更新指令檔
- 定期檢視並精煉規則內容

> **使用方式**: `instructions.md` 檔案會被 AI 自動參考，無需手動呼叫

---

### 特殊情境：舊版 .NET Framework 專案

針對 .NET Framework 4.0 等舊版本專案，建議在 `xxx.prompt.md` 中明確定義技術限制：

- 可參考 [OldArchitecture.md](OldArchitecture.md) 檔案中的相關內容進行調整。

> **提示**: 如果再 `csharp.instructions.md` 中定義過但是產生的程式碼還是會超出使用語言版本， 可以嘗試在 prompt 中再次強調這個限制條件.

#### 撰寫建議

- **語言選擇**: 建議使用英文撰寫，AI 對英文內容的理解更精準
- **其他檔案**: Prompts 和 Agents 可使用中文，依個人偏好

---

## Prompts 與 Agents 檔案說明

### 使用方式差異

| 檔案類型 | 使用方式 | 時機 |
| -------- | -------- | ---- |
| **Instructions** | AI 自動參考 | 編寫程式碼時自動套用規則 |
| **Prompts** | 手動呼叫 | 需要特定任務時主動使用 |
| **Agents** | 手動呼叫/切換模式 | 需要專業協助時主動使用 |

### 檔案功能介紹

#### create-readme.prompt.md

**用途**: 文件產生提示範本

- 定義 README 文件的撰寫規範
- 協助 AI 產生結構化的專案說明文件
- 確保文件品質與一致性

**適用情境**: 需要為專案建立或更新說明文件時

---

#### code-review.agent.md

**用途**: 程式碼審查專用 Agent

- 自動檢查程式碼品質
- 找出潛在問題與漏洞
- 提供優化建議

**適用情境**: 

- 提交 Pull Request 前的自我審查
- 重構程式碼時的品質把關
- 學習最佳實踐

---

#### CSharpExpert.agent.md

**用途**: C# 專家助手

- 解決 C# 相關技術問題
- 提供架構設計建議
- 協助疑難排解

**適用情境**:

- 遇到複雜的 C# 問題
- 需要架構設計建議
- 學習進階 C# 技巧

---

### 取得更多範本

網路上有豐富的 Prompts 和 Agents 資源：

- **從頭開始**: 根據需求自行撰寫
- **參考範本**: 使用本專案提供的範本
- **社群資源**: 瀏覽 [GitHub Awesome Copilot](https://github.com/github/awesome-copilot/tree/main) 尋找更多範本

> **提示**: 本專案提供的檔案都是實際測試過的版本，可直接使用或作為基礎進行修改

---

## Skills 技能檔案說明

### 核心概念

**Skills** 是 2025 年 12 月推出的全新 AI 技術協定，與 Instructions、Prompts、Agents 並列為 AI 自訂功能的四大類型。

**檔案用途**:

- 定義可重複使用的 AI 技能模組
- 透過關鍵字快速呼叫特定功能
- 自動被 AI 參考，無需手動呼叫
- 提供領域專業知識與操作流程

### 使用方式

| 檔案類型 | 檔案位置 | 呼叫方式 | 適用情境 |
| -------- | -------- | -------- | -------- |
| **Skills** | `.github/skills/` | 關鍵字觸發 | 需要特定專業技能時 |
| **Instructions** | `.github/instructions/` | 自動參考 | 編寫程式碼時 |
| **Prompts** | `.github/prompts/` | 手動呼叫 | 執行特定任務時 |
| **Agents** | `.github/agents/` | 手動切換 | 需要專家協助時 |

### 範例:Code-Review Skill

本專案提供 `Code-Review` 技能範本作為參考:

**檔案結構**:
```
.github/
└── skills/
    └── Code-Review/
        └── SKILL.md
```

**使用範例**:
```plaintext
請用 Code-Review skill 審查 #sym:FindLHS
```

**說明**:

- `請用 Code-Review skill 審查` - 關鍵字， 自動觸發該 Skill
- `#sym:FindLHS` - 要審查的程式碼檔案標籤

### 建立 Skills 檔案

#### 方法 1: 從 Agent 轉換

如果已有 Custom Agent 檔案，可直接轉換為 Skill:

1. 複製 Agent 檔案內容
2. 在 `.github/skills/` 建立新資料夾
3. 建立 `SKILL.md` 檔案
4. 調整格式以符合 Skill 規範

#### 方法 2: 從零開始

參考官方文件規範撰寫:
1. 定義 SKILL 名稱與觸發關鍵字
2. 描述 SKILL 的功能與用途
3. 說明使用方式與參數
4. 提供使用範例

#### 方法 3: 使用 skill-creator

使用 skill-creator 這個 skills 來建立屬於自己的 skills，
使用自然語言透過AI輔助來幫助生成skills檔案

#### 方法 4: GitHub 找有興趣的 Repository

在 GitHub 上找出覺得不錯或是有趣的 Repository，將其下載下來之後，將裡面的 程式碼 檔案轉換成 Skills 檔案
對著 AI 說: "把這個目錄中的專案變成我的全域性 Skills 檔案"

### 注意事項

> **重要提醒**: Skills 是經由關鍵字自動觸發的， VS Code 預設沒有開啟支援， 需要在設定中啟用:chat.useAgentSkills. 詳細可以參考官方說明

**疑難排解**:

- ✅ **呼叫成功**: AI 自動識別關鍵字並執行對應功能
- ❌ **呼叫失敗**: 可能原因:
  - Skill 檔案說明不夠明確
  - 關鍵字與 Skill 名稱不匹配
  - 檔案路徑或格式錯誤

**解決方案**:
1. 檢查 `SKILL.md` 檔案內容是否清楚
2. 確認關鍵字定義正確
3. 必要時可直接呼叫檔案指定使用(但這不是原始設計目的)

### 參考資源

詳細的 Skills 使用說明與規範，請參考:

- [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [About Agent Skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
- [Skills 學習平台](https://skillsmp.com/)

> **提示**: Skills 是新技術，建議先從範本開始，逐步熟悉後再自行建立

---

## 日常 AI 開發流程

### 完整開發週期

```mermaid
graph LR
    A[收到 PM/SA 給予的系統分析報告書] --> B[需求確認與細化]
    B --> C[撰寫開發規格書]
    C --> D[AI 優化規格書]
    D --> E[人工審查規格]
    E --> F[AI 開發實作]
    F --> G[程式碼審查]
    G --> H[測試與驗證]
```

### 步驟詳解

#### 階段 1: 需求分析

**輸入**: PM/SA 給予的系統分析報告書

**任務**:

1. 仔細閱讀需求書內容
2. 識別模糊或不清楚的需求
3. 列出潛在問題與遺漏點
4. 與 PM/SA 確認細節，確保認知一致
5. 任何不清楚的地方都要詢問確認需求一致避免事後返工

> **重要**: 需求確認階段投入的時間，能避免後續大量的返工

---

#### 階段 2: 規格書撰寫

**第一版（手動撰寫）**:

建立規格書大綱，包含以下內容：

- 功能需求清單
- 技術架構設計
- 資料庫結構規劃
- API 介面定義
- 前端頁面規劃
- 測試計畫

**AI 優化（使用進階模型）**:

```plaintext
提示詞範例：
"file:xxx.prompt.md 這是我的需求大綱，幫我完善規格書內容。
只需要調整內容，先不用實作開發。"
```

**建議模型**:

- 規格書撰寫: Claude Opus 4.5 / GPT-5.2 Codex
- AI 擅長撰寫結構化文件，充分利用其優勢

---

#### 階段 3: 規格審查

> **關鍵提醒**: AI 不是你，無法讀懂你的想法！

**審查重點**:

- ✅ 技術方案是否可行
- ✅ 功能描述是否完整
- ✅ 邊界條件是否考慮
- ✅ 錯誤處理是否完善
- ✅ 效能要求是否滿足

**上下文（Context）的重要性**:

```plaintext
❌ 不良範例：
"幫我做一個會員系統"

✅ 良好範例：
"幫我做一個會員系統，需求如下：
- 使用 ASP.NET Core 10.0， c# 14
- 支援 Email/Google 登入
- 需要 Email 驗證
- 包含角色權限管理
- 資料庫使用 SQL Server
- 需要實作忘記密碼功能
- 遵循專案既有的架構模式（請參考 #file:UserModule.cs）"
```

**原則**: 提供的上下文越完整，AI 產生的內容越符合需求

---

#### 階段 4: 程式碼實作

**模型選擇策略**:

| 工作類型 | 建議模型 | 原因 |
| -------- | -------- | ---- |
| 規格書撰寫 | Claude Opus 4.5 / GPT-5.2 Codex | 需要更好的邏輯推理與文件組織能力 |
| 程式碼開發 | Claude Sonnet 4.5 | 平衡效能與成本 |
| 簡單需求 | Raptor mini / Claude Haiku 4.5 | 節省 AI 額度 |

**成本控制建議**:

- 高級請求額度充足 → 全程使用進階模型
- 額度有限 → 規格階段用進階模型，開發階段用標準模型

---

#### 階段 5: 程式碼審查

> **核心原則**: AI 產出的程式碼是 AI 的，不是你的！

**必要審查步驟**:

1. **邏輯審查**
   - 檢查商業邏輯是否正確
   - 驗證邊界條件處理
   - 確認錯誤處理機制

2. **程式碼品質**
   - 是否符合專案規範
   - 命名是否清晰易懂
   - 是否有重複程式碼

3. **安全性檢查**
   - SQL Injection 防護
   - XSS 防護
   - 敏感資料處理

4. **效能評估**
   - 資料庫查詢效率
   - 演算法複雜度
   - 記憶體使用

**使用 code-review Agent**:
```plaintext
"@code-review 請審查以下程式碼，重點檢查安全性與效能問題"
```

---

#### 階段 6: 測試與驗證

**測試檢查清單**:

- [ ] 單元測試通過
- [ ] 整合測試通過
- [ ] 手動測試主要流程
- [ ] 邊界條件測試
- [ ] 錯誤情境測試
- [ ] 效能測試（如適用）

**提交前確認**:

- [ ] 程式碼已審查
- [ ] 測試已完成
- [ ] 文件已更新
- [ ] Commit 訊息清楚

---

### 開發心法

**1. AI 是助手，不是替代品**

- AI 提供建議與草稿
- 開發者負責審查與決策
- 保持批判性思考

**2. 充分的上下文是關鍵**

- 清楚描述需求
- 提供相關程式碼參考
- 說明專案限制

**3. 不要期待一步到位**

- 大型任務需要拆分
- 逐步優化與調整
- 保持耐心與迭代思維

**4. 持續學習與優化**

- 記錄有效的提示詞
- 優化 instructions 檔案
- 分享團隊最佳實踐

---

## Copilot SDK - 客製化整合方案

> **最新功能** (2026 年 1 月 推出)

GitHub 正式推出 [Copilot SDK](https://github.com/github/copilot-sdk)，讓開發者能夠將 GitHub Copilot 的智慧代理嵌入自家應用、IDE、服務或自動化流程中。

Copilot SDK 架構圖 參考 #file:246147.jpg

### 什麼是 Copilot SDK

Copilot SDK 是一套多平台開發套件，用於將 GitHub Copilot Agent 整合到第三方應用與服務。產品可直接呼叫 Copilot 的能力（例如程式碼補完、聊天式輔助、專案現代化代理等），無需從零建置 AI 代理。

### 主要用途

#### IDE 或編輯器內嵌助理

- 將 Copilot 的即時程式碼建議與聊天功能整合至自家開發工具或擴充套件中

#### 企業應用中的自動化任務

- 應用於程式碼審查、升級建議、測試生成、CI/CD 自動化或專案現代化流程
- 範例：Visual Studio 的現代化代理示例

#### 建立客製化代理與工作流程

- 依公司內部規範、私有程式庫或專案範本調整回應行為
- 提供一致且可控的開發體驗

#### 跨平台整合

- 支援多種語言與平台
- 可部署於 Web、桌面或伺服器端服務

### 決策要點與建議

#### 是否需要內嵌 AI 助手

- 若目標是提升開發效率或自動化重複性任務，Copilot SDK 屬於直接可行的整合路徑

#### 效率需求

- 評估團隊是否需要將 AI 能力整合到現有工具鏈中
- 考慮自動化流程的投資報酬率

#### 資料與隱私

- 需評估私有程式碼、合規與授權需求
- 確認 SDK 與企業政策相容

---

## 參考資源

### 官方與社群資源

1. **[VSCode 設定](https://github.com/doggy8088/github-copilot-configs)**  
   保哥的 GitHub Copilot 設定參考

2. **[Awesome Copilot](https://github.com/github/awesome-copilot/tree/main)**  
   GitHub 官方 Copilot 資源庫

3. **[Skills 學習平台](https://skillsmp.com/)**  
   AI 輔助開發技巧與最佳實踐

4. **[如何安裝 VSCode 與編譯](https://www.youtube.com/watch?v=fF9p4TPRJDk)**  
   環境設定教學影片

5. **[Spec Kit](https://github.com/github/spec-kit)**  
   SDD 的規範與範本

6. **[Use Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)**  
   官方 Agent Skills 使用說明

7. **[About Agent Skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)**
   官方 Agent Skills 介紹

8. **[Clawdbot](https://www.inside.com.tw/article/40571-clawdbot-github-mac-mini-ai-agent-logan-kilpatrick)**
   Clawdbot 在 GitHub 自我定位為「你在自己設備上運行的個人 AI 助理」，它還會在你已經在用的管道回覆你，包含 WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、Microsoft Teams、WebChat，並延伸支援更多通道。
   - [介紹說明](https://2023meowmiles.com/moltbot-%e5%ae%8c%e6%95%b4%e6%8c%87%e5%8d%97%ef%bc%9a6-%e8%90%ac-github-stars-%e8%83%8c%e5%be%8c%e7%9a%84%e8%87%aa%e8%a8%97%e7%ae%a1-ai-%e5%8a%a9%e6%89%8b%ef%bc%8c%e9%96%8b%e7%99%bc%e8%80%85%e5%bf%85/)

### 進階學習資源

想深入了解如何更有效使用 AI 開發工具？

- 參考 Trello「資源共享區」
- 收錄多個 GitHub Copilot 使用指南
- 包含 AI 輔助開發最佳實踐

---

## 總結

透過標準化的設定與流程，AI 工具能夠有效提升開發效率。但請記住：

> **AI 是強大的助手，但最終的品質把關仍需要開發者的專業判斷。**

**成功關鍵**:
- ✅ 完善的 instructions 檔案
- ✅ 清晰的需求與規格
- ✅ 充分的程式碼審查
- ✅ 持續的優化與學習

祝你的 AI 開發之旅順利！
  