# Insight 速記 — AI Agent 的心智模型

> 這份檔案收集「概念級 / 心智模型級」的洞察，與 `personal-info.md`（事實紀錄）分開。
> 每條編號，往後設計 workshop 時可直接引用。講者每講一個就往這裡加。

---

## INSIGHT-1：LLM 本質是 I/O 黑盒子，跟 chatbot 沒兩樣

> **來源**：講者陳述（2026-07-01）

### 核心命題
一個 LLM，不管外包裝成 chatbot、agent、orchestrator，**本質上就是一個根據 input 吐 output 的 I/O 黑盒子**。從這個角度看，最炫的 coding agent 跟最陽春的 web chatbot **沒有本質差別**——都是「給一段 input，拿一段 output」。

### 只有两根槓桿能讓 output 更好
1. **改善 input（context）** —— 也就是「context engineering」
2. **換更強的模型**

其餘所有花俏的東西（prompt 模板、RAG、MCP、skill 檔、orchestrator、delegation、tool calling⋯⋯）**全部都只是「改善 input」這根槓桿的不同實作方式**。

### 這條洞察拆穿了什麼
- **拆穿「AI 是魔法」**：沒有魔法，就是 I/O。學生一旦內化這點，就不再把 agent 當神拜，而開始像工程師一樣思考「我該怎麼構造 input」。
- **拆穿「vibe coding」的盲目**：只按 Enter、不塑造 input，等於把輸出完全交給模型當下的隨機性。
- **拆穿「換工具就會變強」的迷思**：換 agent 框架常常只是換一種「包裝 context 的方式」，不是換模型能力。

### 對 workshop 的啟示
- **第一堂課該建立的唯一底層觀念**，可能就是這條。它讓後面所有「context engineering / skill / MCP / delegation」都有統一的解釋框架——「這些都是 input 的構造方法」。
- 對應一個教學手法：**先讓學生把一次 LLM 呼叫看成「一段文字進、一段文字出」**（正是講者 text-thread 經驗的起點，見 `personal-info.md` §6.2），再示範「同樣的模型，input 不同 → output 天差地遠」。這個對照實驗會讓 INSIGHT-1 當場被學生「親身驗證」。

### 交叉引用
- `personal-info.md` §6.2-6.3：text-thread 經驗是 INSIGHT-1 的「親身活體實驗」——因為講者能直接編輯歷史（= 改 input），所以親眼看到 output 跟著變。
- 後續若講者補充「context engineering 的具體手法」（清單第 2 項 workflow、或任何 prompting/skill/MCP 技巧），**那些都是 INSIGHT-1 的應用案例**，不是獨立主題。

---

## INSIGHT-2：把 LLM 當成「可經驗式 debug 的系統」，不是「要答案的神諭」

> **來源**：講者陳述（2026-07-01），來自其日常 context-engineering 技巧庫（見 `personal-info.md` §5.7）

### 核心命題
INSIGHT-1 說 LLM 是 I/O 黑盒子。但黑盒子不是不能研究——任何工程師面對黑盒子，用的就是同一套經驗方法。**把 LLM 當成系統來 debug，而不是當神諭來問**，是「會用」與「不會用」的分水嶺。講者身為系統工程背景的 LLM 土著，自然把 GDB / 實驗那套直覺搬過來用。

### 講者用的四個 debug 手法（每一個都有工程對應）

| 講者手法 | 對應的工程 debug 技巧 | 在 LLM 上的意義 |
|---|---|---|
| **重新 roll 一次** | 重跑測試 / 取樣 | 探索 output 分佈。同一 input 多次取樣，看答案是穩健還是運氣好 |
| **改 input + 重新 roll** | 改參數重跑 | INSIGHT-1 的主迴圈：迭代塑造 context |
| **Fork chat / 雙 thread A/B** | Controlled experiment / diff 輸入 | 只動一個維度、比較 output → isolate 出哪個 input 因子才有效 |
| **偷看 thinking process** | 看 stack trace / 觀察中間狀態 | 部分打開黑盒子，看模型推理鏈是否走偏 |

### 講者追求的兩個目標（對應 INSIGHT-1 兩根槓桿）
1. **了解怎麼 input 最有效率** → context engineering 本身（槓桿一）
2. **了解不同模型效果如何** → 模型選擇（槓桿二）

### 這條洞察拆穿了什麼
- **拆穿「問一次就相信」**：一次 output 只是分佈裡的一個樣本，不是「模型的答案」。
- **拆穿「AI 給的答案 = 它的實力」**：同模型，input 不同、採樣不同，表現天差地遠。
- **拆穿「模型選錯就沒救」**：換模型之前，先把 input 這根槓桿用滿（對應 INSIGHT-1）。

### 對 workshop 的啟示
- 這四個手法**每一個都是現成的課堂實作題**：
  - 全班同一題一起 re-roll → 親眼看見變異
  - 改一句 prompt 比 output diff → 看見 input 的力量
  - Fork 兩條線做 A/B → 學會受控實驗
  - 看 thinking 找錯 → 學會讀推理鏈
- 更深一層：這套手法是**「把學生從 vibe coder 改造成 LLM 工程師」的最短路徑**。學生一旦開始 re-roll + A/B，就回不去了——他們會開始「看見」分佈，而分佈一旦被看見，就不可能再當神諭拜。

### 交叉引用
- INSIGHT-1 的實作層：INSIGHT-1 給理論（黑盒子 + 兩根槓桿），INSIGHT-2 給方法（怎麼研究這個黑盒子）。
- `personal-info.md` §5.7：講者的具體技巧庫。
- `personal-info.md` §6.2：text-thread 編輯歷史 = INSIGHT-2「改 input 重跑」手法的最透明形式。

---

## INSIGHT-3：「Agent」就是一個 loop —— 把名詞拆掉

> **來源**：講者陳述（2026-07-01），來自其 Zed agent 時代的觀察（見 `personal-info.md` §5.8）

### 核心命題
所謂 "AI agent" 不是新東西，**就是一個迴圈**：

1. 給 LLM 一個 system prompt，下面寫好工具定義（`read` / `write` / `edit` / `bash` 等 + 使用說明 + 呼叫格式）
2. LLM 吐 output
3. 若 output 符合某工具的呼叫格式 → 執行該工具，**把結果回灌進 context**
4. 重新送一次 input 給 LLM
5. 重複，直到 LLM 自己決定停止

整個「agentic」魔法，**就是這五行 while loop**。

### 這條洞察拆穿了什麼
- **拆穿「agent 是新型 AI」**：agent = LLM + 一個 while loop + 幾個工具。LLM 還是那個 INSIGHT-1 的 I/O 黑盒子，只是外面包了迴圈。
- **拆穿「agent 會自主思考」**：它沒有「想」，每次迴圈都還是「給 input、吐 output」，只是 input 裡多了「上一步工具的結果」。
- **拆穿「agent 框架很神祕」**：Claude Code、Cursor agent、Zed agent、opencode、Cline、gemini-cli⋯⋯**底層全都是這個 loop 的不同實作**，差別只在工具集、system prompt、context 管理策略。

### 對 workshop 的啟示
- 這條是 INSIGHT-1（黑盒子）+ INSIGHT-2（debug 黑盒子）之後的第三層祛魅：**把「agent」這個名詞徹底拆掉**。學生會瞬間明白「為什麼同一個模型，放在不同框架裡表現不同」——因為 framework 在改迴圈的 input（system prompt、工具描述、context 注入策略）。
- **教學手法**：課堂上直接展示一個 ~20 行的 agent loop 原型（`while` + LLM call + tool dispatch），讓學生看到「魔法的全部程式碼」。看過一次，終身祛魅。
- 講者的 `curl` 抓網頁、doc→markdown 注入等技巧（見 §5.8），本質都是「**主動在這個 loop 的某一步，注入新 input**」。

### 交叉引用
- INSIGHT-1 的延伸：把「一次 LLM 呼叫」放大成「多次 LLM 呼叫 + 工具回授」。
- INSIGHT-4 的前提：既然 agent 是 loop，loop 裡的「LLM」不同回合可以換不同模型。
- `personal-info.md` §5.8：講者所有 agent 時代技巧，都是對這個 loop 的操作。

---

## INSIGHT-4：把多個模型當成「可組合的組件」（model composition）

> **來源**：講者陳述（2026-07-01），實習期間為最大化每月 API 用量所發展出的策略（見 `personal-info.md` §5.8）

### 核心命題
INSIGHT-1 說改善 output 有兩根槓桿：input 與模型。但「模型」這根槓桿**不必只能選一個**。實務上可以把多個模型當成可組合的組件，**依各自的長處調度，用 text 把它們串起來**。

每個模型有不同維度的長處：
- **能力**（聰明度 / 規劃力）：Claude 3.7 / Claude 4 等
- **價格**：Gemini / DeepSeek 等便宜模型
- **context 長度**：Gemini 1M vs Claude 短
- **模態**：Gemini 多模態 vs 純文字模型

→ 把 text（markdown / 純文字）當成模型之間的「**通用匯流排**」，就能讓「貴但短」的模型負責規劃、「便宜但長」的模型負責實作、「有眼睛」的模型負責 OCR。

### 講者實作的三個 compose pattern

| Pattern | 做法 | 剖析 |
|---|---|---|
| **貴規劃 + 便宜實作** | 同一 context 內先用 Claude 3.7 規劃/架構，再切 Gemini 模仿實作 | 品質瓶頸在規劃階段時，用便宜模型收割強模型的 plan |
| **長 context 當壓縮機** | Gemini 讀 AI-native 文件庫 → 總結 → 餵 Claude 實作 | 用 Gemini 的 1M context 當「context down-sampler」，把長 input 壓成 Claude 能消化的短 input |
| **多模態當 OCR** | Gemini 讀圖 → 轉文字 → 餵純文字模型 | 用多模態模型當「模態轉換器」，把視覺資訊轉成任何模型都能讀的 text |

### 這條洞察拆穿了什麼
- **拆穿「選錯模型就卡住」**：瓶頸在哪一階段，就只在那階段用貴模型，其他階段用便宜的。
- **拆穿「我得有 A 模型才能做 X」**：常常只要找一個「擅長 X 的模型」當預處理器，就能讓手上的模型也做得到。
- **拆穿「API quota 不夠用」**：講者實習時最大化月用量的核心策略就是這條——**把貴模型省下來只用在最關鍵的規劃/決策步**。

### 對 workshop 的啟示
- **特別適合「學生沒預算」情境**：教他們用免費/便宜的模型當主力，只在關鍵處用貴模型。
- 三個 pattern 都可現場 demo：Gemini Flash 跑長文件總結 → 切給免費 Claude 跑實作，讓學生看到「月費 $0 也能做出近似 pro 體驗」。
- 跟 INSIGHT-3 結合：所謂 multi-model orchestration，**本質就是「在 agent loop 的不同回合，換不同的 LLM 來當那個 I/O 黑盒子」。loop 不變，只換 box。**

### 交叉引用
- INSIGHT-1 的「模型」槓桿的進階用法：從「選一個」變「組合多個」。
- INSIGHT-3 的延伸：agent loop 裡的「LLM」可以是不同回合不同模型。
- `personal-info.md` §5.8：講者的具體三招 + 其他技巧。

---

## INSIGHT-5：MCP 工具設計的兩種典範 —「提升智商」vs「外包苦工」

> **來源**：講者陳述（2026-07-01），來自其調查 Zed MCP 商店高下載量伺服器後的歸納（見 `personal-info.md` §5.9）

### 核心命題
MCP（Model Context Protocol）本質就是一個協議：把 local 或 remote 的 RPC 包成 tool、加上 tool 描述，掛在 agent 的 tool 清單下，agent 就會像 `read`/`write`/`edit`/`bash` 一樣呼叫它。MCP 常被形容為「模型的 USB」。

但 MCP server 在設計上有兩種截然不同的典範：

| 典範 | 工具數 | 每個工具做什麼 | 範例 | 軟體工程類比 |
|---|---|---|---|---|
| **A. 少量深實作** | 少（1~3 個）| 每個工具只做一件事，把複雜度在內部消耗掉，輸出高度精煉的 context | context7（抓最新 doc 餵給模型）、講者的 markitdown | 「少量公開介面、深實作」——複雜度內部吸收 |
| **B. 多量薄實作** | 多（十幾～幾十個）| 每個工具對應一種用法，把服務原樣暴露 | github mcp、postgres mcp | 「多介面、薄實作」——複雜度推給上層 |

對 LLM 而言：
- **A 典範 = 提升模型的能力 / 智商**：模型不用懂 doc 怎麼抓，工具直接給它「已經是最相關的 context」。
- **B 典範 = 讓 LLM 做苦工**：模型要自己決定呼叫哪個工具、怎麼組合，等於把編排負擔推給 LLM。

### 為什麼 B 典範常是壞選擇（講者觀點）
1. **污染上下文**：幾十個工具描述塞進 system prompt，吃掉大量 token、稀釋有效 context。
2. **壓低 tool-call 成功率**：工具一多，模型選錯工具、用錯參數的機率顯著上升——而很多模型本來就不擅長 tool-call。
3. **結果**：B 典範在弱模型上幾乎不可用。

### 實證支持（已查證，2026-07）
講者這個「直覺」**已被多方量化實證**，且程度比直覺更嚴重——**所有數據與原始來源見 `references.md` §4**。最關鍵的可引用數字：
- 控制實驗（GPT-4o）：tool-selection 準確率 **43%（4 工具）→ 2%（51 工具）**，同模型同任務只變工具數。
- Speakeasy benchmark：10 工具滿分 → 107 工具完全失敗。
- Anthropic 官方：Claude 在 30-50 工具後明顯衰退，為此建 Tool Search（Opus 4.0: 49%→74%）。
- 真實案例：4 servers / 167 工具 = 60K tokens 還沒工作就吃掉。
- 平台硬上限：Cursor 40 工具、Copilot 128、Zed profiles；Perplexity CTO 2026-03 公開棄用 MCP。

→ INSIGHT-5 從「個人觀點」**升級為「可量化、可引用」的教材**。設計教材時直接引用 `references.md` §4 的數字做課堂震撼材料。

### 緩解手法（連回 INSIGHT-4）
當必須用 B 典範時，講者的解法是：**先讓 Claude（強模型）使用並建立示範軌跡，再切弱模型接手**——弱模型會模仿強模型已走過的 tool-call 序列。這正是 INSIGHT-4「貴規劃 + 便宜實作」的應用。

### 這條洞察拆穿了什麼
- **拆穿「MCP 越多越強」**：裝一堆 MCP 不會讓 agent 變強，反而常讓它變笨（context 污染 + tool-call 失敗）。
- **拆穿「裝了就能用」**：MCP 的價值取決於設計典範。**一個設計良好的 A 典範 MCP > 十個 B 典範 MCP**。
- **拆穿「弱模型 + 多 MCP = 省錢」**：反向才對——多 MCP（B 典範）需要強模型才能駕馭。

### 對 workshop 的啟示
- 這條是「**教學生怎麼挑 MCP / 怎麼自己寫 MCP**」的判斷框架：**優先寫 A 典範（給模型精煉 context），謹慎用 B 典範（只在使用者真的需要互動操作時）**。
- 對應一個實作題：讓學生把同一個服務寫成兩種 MCP（「一個深工具」vs「十個薄工具」），在同一任務上比成功率。差異會非常直觀。
- 講者自己的 `zed-mcp-server-markitdown`（29,963 下載）就是 A 典範範例——單一工具、把「PDF/doc/slide → markdown」的複雜度在內部消耗，只給模型乾淨的 markdown。

### 交叉引用
- 呼應 INSIGHT-1：A 典範 = 主動改善 input（給模型最好消化的格式）。
- 呼應 INSIGHT-3：MCP 工具就是 agent loop 裡「可呼叫的工具」的擴充來源。
- 呼應 INSIGHT-4：B 典範的緩解（強模型示範 → 弱模型模仿）= 模型組合策略。
- `personal-info.md` §5.9：MCP 實戰歷程與 markitdown wrapper 故事。

---

## INSIGHT-6：環境分工 — web chatbot 與 local agent 各有所長，用 text 當匯流排

> **來源**：講者陳述（2026-07-01），見 `personal-info.md` §5.10

### 核心命題
不同 agent 環境有截然不同的比較利益：
- **Web chatbot**（Perplexity、Gemini deep research）：能在背景**批量搜尋數十到上百個網頁**——這是 local agent 做不到（或做得慢/差）的超能力。但它進不了你的 codebase、讀不到 local context。
- **Local agent**（Zed agent / opencode）：完全存取你的檔案/程式碼/歷史 context，能 read/write/edit/bash，但 web 搜尋能力遠不及專門的搜尋引擎後端。

→ 最優解不是「選邊站」，而是**讓各環境做自己最擅長的事，用 text/markdown 把結果在兩邊之間搬**。講者 routine：web chatbot 跑 deep research 批量搜尋 → 把 markdown 結果貼回 local agent 繼續加工。

### 跟 INSIGHT-4 的關係（同一底層原則，不同顆粒度）
- INSIGHT-4 = **模型**層組合（貴模型規劃 + 便宜模型實作）
- INSIGHT-6 = **環境**層組合（web chatbot 搜尋 + local agent 加工）
- 兩者共用同一底層：**text 是通用匯流排，任何會吐 text 的 AI 組件都能被組合**。

### 這條洞察拆穿了什麼
- **拆穿「web chatbot 是落後選擇」**：講者雖主力是 local agent，仍持續用 web chatbot——因為它的批量搜尋是 local 難以複製的能力。「用 web chatbot」不等於「vibe coding」，關鍵是把它當**研究後端**而非**答案來源**。
- **拆穿「我得讓 local agent 什麼都能做」**：local agent 不必內建強搜尋；把研究外包給專門環境再把結果餵回來，反而更有效率。
- **拆穿「chatbot 跟 agent 是競爭關係」**：它們是**分工伙伴**。

### 對 workshop 的啟示
- 對「學生只會用 ChatGPT 網頁版」的情境，這條是**反轉**：不是叫學生丟掉 ChatGPT，而是教他們**把 ChatGPT / Perplexity 當研究後端**，再把產出搬進 local 工具鏈加工。學生現有的習慣（用網頁 chatbot）變成資產，不必從零換軌。
- 實作題：用 Perplexity / Gemini deep research 跑一個研究題目 → markdown 結果存檔 → 在 local agent 裡注入當 context → 讓 local agent 基於這份研究繼續寫程式/分析。整條鏈路一氣呵成。

### 交叉引用
- INSIGHT-4 的環境層兄弟（共用「text 通用匯流排」原則）。
- INSIGHT-1 的應用：把 deep research 的 markdown 結果當「改善 input」的最強素材。
- `personal-info.md` §5.10：講者的環境分工 routine。

---

## INSIGHT-7：自建 context 語料庫 — 與其讓 AI 盲猜，主動把整個世界搬進它的 context

> **來源**：講者陳述（2026-07-01）+ `~/School` 目錄實證（見 `personal-info.md` §5.11）

### 核心命題
INSIGHT-1 說「改善 input」。最極致的改善 input，不是改 prompt，而是**預先打造一整個專屬的、版本控管的、markdown 化的知識庫，讓 agent 在裡面工作**。

講者的 routine（針對每門課）：
1. **拉下課程檔案**（slide / PDF / 作業 / 講義）
2. **全部轉 markdown**（AI-native 格式，INSIGHT-1 應用）
3. **整理成獨立 git repo**（每門課一個 note repo，含 `course-materials/`、`notes/`、`exam/` 等結構）
4. **在該 repo 內直接問 agent**——agent 自動以整門課內容為 context，不是盲猜
5. **把該目錄當作業/專題的 submodule**——作業一開工就繼承整門課背景

講者自況：**「手搓出類似 NotebookLM 或 RAG 的能力」**。但這版本比 NotebookLM 更強：版本控管、可組合（submodule）、可攜（純 markdown）、完全自控。

### 結構三件套（講者的 context 架構，`~/School` 已實證）
| 組件 | 角色 | 實例 |
|---|---|---|
| **note repo**（語料庫）| 該領域完整 markdown 知識庫 | `ntu-2025fall-advanced-compiler-note`（20 md + 9 pptx + 5 pdf）|
| **work repo**（作業/專題）| 實際產出，以 submodule 引用語料庫與上游 | `...-hw1-G36maid` 拉 Cornell `bril`；`cs-computer-graphics` 拉 4 個作業 repo |
| **AGENTS.md**（agent 操作手冊）| 告訴 agent 在此 repo 怎麼工作 | 講者 15+ 個 repo 都有 |

→ 這是「context 架構」：把**知識庫**與**工作專案**分離，用 agent 操作手冊當橋樑。同樣的 pattern 也出現在講者的 `ctf-arsenal`（`.agents/skills/`）與 opencode/omo workflow。

### 跟其他 insight 的關係
- **INSIGHT-1 的最極致應用**：改善 input 改到「整個 repo 都是 input」。
- **INSIGHT-5 的尺度放大**：A-典范 MCP 是「在工具層預先精煉 context」；INSIGHT-7 是「在 repo 層預先精煉 context」——同原則、不同尺度。
- **跟 INSIGHT-6 一外一內互補**：INSIGHT-6 把「研究」外包給 web chatbot；INSIGHT-7 把「課程知識」內化為自有語料庫。都是為 local agent 構造最強 input。

### 這條洞察拆穿了什麼
- **拆穿「問 AI 就是好的 AI 使用」**：「問」之前先決定 AI 在什麼 context 裡問。同問題、同模型，在語料庫 repo 裡問 vs 空白對話問，答案天差地別。
- **拆穿「我得懂 RAG / 向量資料庫才能做這件事」**：git + markdown + 任何會讀檔的 agent，就能做出比向量 RAG 更可控、更透明、更可組合的版本。RAG 的本質是「給模型相關 context」，檔案系統 + agent 就是最直接的實作。
- **拆穿「NotebookLM 是神奇新產品」**：它的核心就是「語料庫 + LLM」，講者用既有工具手搓出更強版。

### 對 workshop 的啟示（**至今最具轉移性的 workflow**）
- 這是至今**最適合直接教給學生**的 workflow：每個學生都修課、每個學生都能做、**不需要進階環境或付費 API**。
- 它同時教會學生 **git + markdown + context engineering + agent 操作手冊** 四件事，且立即改善課業（複習、作業、專題）。
- 它把「AI 輔助學習」從「請 ChatGPT 幫我摘要」升級成「**建一個讓 agent 住進去的知識庫**」——心智模型的躍遷。
- 實作題：學生挑一門現在修的課，照三件套（note repo + work repo + AGENTS.md）實作一遍，期末回饋。
- **結構性 bonus**：講者的 `~/School` 目錄（含 README 命名規範）本身就是現成教材範本。

### 交叉引用
- INSIGHT-1 的最極致應用；INSIGHT-5 的尺度放大；跟 INSIGHT-6 一外一內互補。
- `personal-info.md` §5.11：`~/School` 實際結構與三件套實證。

---

## INSIGHT-8：AGENTS.md = 業已標準化的「repo 級 system prompt 注入」

> **來源**：講者陳述（2026-07-01）+ 歷史考證（見 `references.md` §6）

### 核心命題
AGENTS.md 不是某家公司的專利，是**業界事實標準**：一份放在 repo 根的 markdown，本質上就是**針對該 repo/workspace 注入的 system prompt**。**README.md 給人看，AGENTS.md 給 agent 看。**

- **起源**：2025-08 Sourcegraph Amp 團隊發起 → OpenAI / Google (Jules) / Cursor / Factory 聯合推動 → **2025-12 捐 Linux Foundation（AAIF）**。
- **採用**：30+ agents 原生讀取（Codex、Cursor、Copilot、Jules、Gemini CLI、Aider、Windsurf、**Zed**、Devin⋯⋯）；60,000+ repos。Claude Code 原生讀 `CLAUDE.md` 但 fallback 讀 AGENTS.md。
- **統一了**：原本每家一套（`.cursorrules` / `CLAUDE.md` / `GEMINI.md` / `.github/copilot-instructions.md` / `.windsurfrules`），AGENTS.md 是 vendor-neutral baseline。完整歷史與來源見 `references.md` §6。

### 講者用法
自從 Zed 支援後，**幾乎每個 repo 都先建 AGENTS.md 再開工**——低成本、高回報的固定習慣（見 `personal-info.md` §5.11，`~/School` 內 15+ 處 AGENTS.md）。

### 這條洞察拆穿了什麼
- **拆穿「每個工具要學不同 rules 系統」**：底層都是同一件事——注入 system prompt。AGENTS.md 是統一介面。
- **拆穿「AGENTS.md 是某公司專利」**：它是 Linux Foundation 下的開放標準，不綁定任一廠商。
- **拆穿「這是形式主義 / 儀式」**：它是 INSIGHT-1 最直接的應用——主動寫下模型該知道的 context，而不是讓它猜。寫不寫，agent 表現天差地別。

### 對 workshop 的啟示
- **「第一次進任何 repo，先寫 AGENTS.md」是最小投入、最高回報的習慣**。
- 它把「prompt engineering」從「寫一句漂亮的一次性 prompt」變成「**為整個專案寫一份持久的說明**」——後者才是工程，前者是玄學。
- 實作題：學生為自己作業 repo 寫 AGENTS.md，比較有/無時 agent 表現差異。
- **教學 gotcha**（見 `references.md` §6.4）：nested discovery 各工具不一致（Codex 串接 root→cwd；Cursor / Claude Code 不做 nested）；Claude Code 靠 `@AGENTS.md` import 橋接。

### 交叉引用
- INSIGHT-1 的應用（system prompt = input 的一部分）。
- INSIGHT-7 三件套之一（agent 操作手冊角色）——本條把它獨立出來強調「標準 / 可攜」面向。
- 跟 INSIGHT-5 A-典范精神一致（預先精煉 context 給模型）。
