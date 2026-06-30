# AI Agent Workshop — 從 web chatbot 到 agent 心智模型

> **講者**：G36maid（NTNU CS/ME 大四）
> **形式**：整天 workshop，9am ~ 下午，約 3-6 小時
> **核心**：帶你從 web-chatbot 心智模型，遷移到 agent 心智模型。

---

## 議程（at a glance）

> 這整張講稿是我當天開著念、也給台下看的同一份。粗體段落是「不可壓縮」的核心；其他可依現場節奏伸縮。

### 上半場（早上）：pure opencode

| 段落 | 時間估計 | 對應 insight |
|---|---|---|
| Block 1：自我介紹 | 10-15 min | INSIGHT-9（誠實定位）|
| Block 2：祛魅 — AI / Agent 到底是什麼 + Mini Agent 現場實作 + 實驗 | 60-90 min | INSIGHT-1, 2, 3 |
| Block 3：環境配置 + First run | 30-40 min | INSIGHT-3, 8 |
| 主場 Block A：MCP 是什麼、直接配起來、設計兩典範 | 40-60 min | INSIGHT-5 |
| 主場 Block B：SKILL 是什麼 + 手搓一個 | 20-30 min | — |
| **主場 Block C：鎮館之寶 — 多模型編排 + live config show-and-tell** | **40-50 min** | **INSIGHT-4** |
| **主場 Block D：自建 context 語料庫 + AGENTS.md 深講** | **30-40 min** | **INSIGHT-7, 8** |

### 下半場（下午）：subagent + omo（條件性）

> 若上午 opencode 講不完 → 下午順延。上午優先級 > 下午。

| 段落 | 時間估計 | 對應 insight |
|---|---|---|
| 下午 Block 1：subagent 概念 + 配置 + context 節省 demo | 30-40 min | INSIGHT-3, 4 |
| 下午 Block 2：omo（若時間允許） | 20-30 min | INSIGHT-3 延伸 |

### 研究工具段（教授要求：不只開發還有研究）

| 段落 | 時間估計 | 對應 insight |
|---|---|---|
| 研究工具 1：web chatbot deep-research | 15-20 min | INSIGHT-6 |
| 研究工具 2：alphaXiv + autoresearch | 20-25 min | INSIGHT-3, 6 |

### 收尾

| 段落 | 時間估計 | 對應 insight |
|---|---|---|
| INSIGHT-9 + INSIGHT-10 | 20 min | 9, 10 |

> 講者備註：上述時間是給自己的錨，不是給學員的承諾。實際節奏由現場火候決定——哪段大家有反應就多講，哪段卡住就壓縮後面。

---

## 這個 workshop 不是什麼 / 是什麼

**不是**：工具教學（那是搬運層在做的事）、不是教你怎麼么按 Cursor、不是「養龍蝦」。

**是**：一次**心智模型遷移**。你們現在多半把 ChatGPT 當答案來源——剪下貼上。我要帶你看到的是：LLM 是一個 I/O 黑盒子，agent 就是繞著它的一个 loop，而你完全可以控制餵進去的 input。

**誠實定位**：我直接把英文圈的 insight 用中文講給你聽，省你爬源頭的時間。我想講我想講的——這是演講者驅動場，不是分層服務。你能吸收到哪層是哪層。

---

# 上半場（早上）：pure opencode

整個早上我們在 **opencode**（開源 coding agent）裡面跑。這是我日常 driver 場景。

---

## Block 1：自我介紹（10-15 min）

### 我是誰

- **LLM 土著**：2022-11 ChatGPT 公開時我大一，幾乎同步開始用。不是後來跟風。
- **Zed Guild Contributor**：我不只用工具，我造工具給這個生態——我寫的 `zed-mcp-server-markitdown` 在 Zed 商店有近 3 萬下載。
- **系統工程 / 資安 / 開源**偏好：Arch Linux、Rust、CTF、homelab。我看待 AI 的方式，跟我看待 kernel 的方式一樣。

### Credibility framing

我不是教授，是**同儕裡走比較遠的那個**。深度是權威來源，不是頭銜。

### 一句話 hook

> 「你們有人用過把 ChatGPT/Claude/Gemini 訂閱接進其他工具的 plugin 嗎？——我被 ban 過。」

（完整故事留到後面 **主場 Block C（INSIGHT-4）** 重講。這裡只建立「這人玩真的、會燙到」的份量。）

---

## Block 2：祛魅 —— AI / Agent 到底是什麼（60-90 min）

這段是整個上午的智識重心。三個 insight 是心智模型遷移的階梯：**一旦你看穿 agent 不是魔法，opencode 就只是「一個刻得好的 loop」**。

---

### INSIGHT-1：LLM 本質是 I/O 黑盒子

不管外包裝成 chatbot、agent、orchestrator，**LLM 就是根據 input 吐 output 的機器**。跟最陽春的 web chatbot **沒有本質差別**。

**改善 output 只有兩根槓桿**：
1. **改善 input（context）** ← 這是今天 80% 的內容
2. **換更強的模型**

其餘所有花俏東西（prompt 模板、RAG、MCP、skill、orchestrator、delegation⋯⋯）**全部都只是「改善 input」的不同實作**。

**這條拆穿什麼**：
- 「AI 是魔法」→ 沒有魔法，就是 I/O
- 「vibe coding」（只按 Enter、不塑造 input）→ 等於把輸出完全交給模型當下的隨機性
- 「換工具就會變強」→ 常常只是換一種包裝 context 的方式

**live demo**：同模型、不同 input → output 天差地別（我從 text-thread 時代就靠這個理解 context 的）。

---

### INSIGHT-2：把 LLM 當系統 debug

LLM 是黑盒子，但黑盒子不是不能研究——**任何工程師面對黑盒子，用的就是同一套經驗方法**。把 LLM 當系統 debug，而不是當神諭問，是「會用」與「不會用」的分水嶺。

**四個 debug 手法**（都是你已經會的工程技巧）：

| 手法 | 工程對應 | 在 LLM 上的意義 |
|---|---|---|
| **重新 roll 一次** | 重跑測試 | 探索 output 分佈——答案是穩健還是運氣好？|
| **改 input + re-roll** | 改參數重跑 | INSIGHT-1 的主迴圈：迭代塑造 context |
| **Fork chat / 雙 thread A/B** | 受控實驗 | 只動一個維度，比較 output → isolate 哪個 input 因子有效 |
| **偷看 thinking process** | 看 stack trace | 部分打開黑盒子，看推理鏈是否走偏 |

**全班實驗**：同一題，大家一起 re-roll → 親眼看見變異。一次 output 只是分佈裡的一個樣本，不是「模型的答案」。

**這條拆穿什麼**：你不必懂 RAG / 向量資料庫才能研究 LLM。git + markdown + 任何會讀檔的 agent，就是最直接的實驗台。

---

### INSIGHT-3：Agent 就是一個 loop

> 這條的出處：**Adam 在 ThePrimeagen Standup podcast [04:32] 定義「Agent = LLM + Tools + Loops」**——我從這裡吸收這個心智模型。

所謂「AI agent」不是新東西，**就是一個迴圈**：

```
1. 給 LLM 一個 system prompt + 工具定義（read / write / edit / bash 等）
2. LLM 吐 output
3. 若 output 符合某工具的呼叫格式 → 執行該工具，結果回灌進 context
4. 重新送一次 input 給 LLM
5. 重複，直到 LLM 自己決定停止
```

**整個「agentic」魔法，就是這五行 while loop。**

**這條拆穿什麼**：
- 「agent 是新型 AI」→ agent = LLM + while loop + 工具。LLM 還是那個 I/O 黑盒子。
- 「agent 會自主思考」→ 它沒有「想」，每次迴圈都還是「給 input、吐 output」。
- 「agent 框架很神祕」→ Claude Code、Cursor agent、Zed agent、opencode、Cline⋯⋯**底層全都是這個 loop 的不同實作**。

---

### 🛠️ Mini Agent 現場實作（Block 2 重頭戲）

我現在從零寫一個 mini agent 給你看。**不到 200 行**。結構：

```python
# 結構骨架（實際程式碼預先準備，現場邊貼邊講）

system_prompt = load("AGENTS.md")          # ← 預告 INSIGHT-8：AGENTS.md = system prompt
tools = [read, write, edit, bash]           # ← 預告 INSIGHT-5：這些是「內建工具」，MCP 是擴充來源
model = config["model"]                     # ← config-driven，可切換（實驗段落要用）

messages = [{"role": "system", "content": system_prompt}]
messages.append({"role": "user", "content": user_task})

while True:                                 # ← INSIGHT-3 本體：agent 就是這個 loop
    response = llm_call(model, messages, tools)
    messages.append(response)

    if response.has_tool_call():
        result = execute_tool(response.tool_call)   # 執行工具
        messages.append(tool_result(result))         # 結果回灌 context
    else:
        break                                # LLM 自己決定停止
```

**這個 build 同時示範多條 insight**：
- INSIGHT-1：loop 裡的 LLM call 就是 I/O 黑盒子
- INSIGHT-3：loop 結構
- INSIGHT-4 預告：`config["model"]` 可切換——暗示同一個 loop，不同 model = 不同 box（主場 Block C 重講）
- INSIGHT-8 預告：`AGENTS.md` = system prompt
- INSIGHT-5 預告：`read/write/edit/bash` 是工具，MCP 是擴充來源

**build 完後**，我指著 opencode 說：「**它就是這個，只是工具更多、context 管理更精細、加上生產級 polish**。」——你親眼看過原型，opencode 從此不是魔法。

---

### 🧪 Mini Agent 實驗段落（互動）

build 完不是結束——同一個 mini agent 立刻當實驗台：

| 實驗 | 做法 | 看見什麼 |
|---|---|---|
| **有/無 AGENTS.md** | 同一任務，先沒 AGENTS.md 跑一次，加上再跑一次 | agent 行為天差地別——**寫不寫 AGENTS.md，表現差很多**當場被驗證 |
| **各家 model 對照** | 同一 agent + 同一 AGENTS.md，換 Go 的不同模型跑同一任務 | 同一個 loop、不同模型 → 品質/風格/能力落差一目了然——同時預告主場 Block C 的多模型編排 |

**為什麼這組實驗強**：都是「同 agent、變一個維度、比 output」——這正是 INSIGHT-2 的受控實驗手法，你邊玩邊內化。

---

## Block 3：環境配置（30-40 min）

接下來讓每個人跑起來。

### opencode 安裝

```bash
# macOS / Linux
curl -fsSL https://opencode.ai/install | bash

# 講者自己用 Arch pacman；跨平台指令見 opencode.ai/docs
# Windows 用戶：見官方 docs 的 Windows 安裝路徑
```

### opencode Go 訂閱（$5 首月，整天夠用）

**為什麼選 Go**：低門檻、14 個強開源模型一把抓、額度對整天 workshop 綽綽有餘、零資料留存。

| 項目 | 內容 |
|---|---|
| 月費 | **$5 首月**，之後 $10/月 |
| 5 小時上限 | $12 等同用量（對單一 session 綽綽有餘）|
| 週上限 | $30 等同用量 |
| 月上限 | $60 等同用量 |
| 伺服器 | US / EU / Singapore |
| 資料政策 | **zero data retention** |
| 取消政策 | 隨時取消；額度不夠可加值 |

**收錄模型（14 個）**：

| 模型 | 定位 |
|---|---|
| **GLM-5.2** | 講者日常 driver，本 session 跑這個 |
| GLM-5.1 | Hades 專題用（Opus-level 開源）|
| Kimi K2.7 Code | 程式特化 |
| Kimi K2.6 | Moonshot 旗艦 |
| MiMo-V2.5 / V2.5-Pro | 小米；V2.5 最便宜 |
| MiniMax M3 / M2.7 | agentic 工作馬 |
| Qwen3.7 Max / Plus、Qwen3.6 Plus | Alibaba 高階 |
| DeepSeek V4 Pro / Flash | 長 context 強 / 高 throughput |

**caveat**：「Only one member per workspace can subscribe」——實驗室共用 workspace 要注意，每人各自註冊帳號就沒問題。

### 套用 Pure Go Config

我準備了一份 **pure Go config**（只路由到 opencode-go provider，不會燒到昂貴 frontier 模型）——這是**成本安全邊界**：無論你怎麼 hammer，最大燒掉就是 Go 額度（$12/5h、$30/週、$60/月）。

> **為什麼必要**：講者日常 config 是 4 provider 混合（會路由到 GPT/Gemini 等級，output 可達 $15-30/1M tokens）——學生現場燒這種等級的 token 是不可控的。Pure Go config 把上限鎖死在 Go 額度。**這個 pattern 本身就是主場 Block C 要講的「成本安全邊界」思想的前哨**。

### 基本指令

| 指令 | 作用 | 為什麼需要 |
|---|---|---|
| `/init` | 初始化 session / 專案設定 | 進任何 repo 第一步——呼應 INSIGHT-8（AGENTS.md）|
| `/compact` | 壓縮對話 context | 對話太長時搶救——context 是有限資源 |
| `/session` | session 管理（list / resume / **fork**）| 呼應 INSIGHT-2 的 fork A/B |
| `/models` | 切換模型 | mini agent 的 model-swap 實驗，現在換你操作 |
| 其他 slash commands | 待補 / 依 opencode docs 當場查 | 只教會用到的，不全部塞 |

**/session fork 是 INSIGHT-2 的肌肉記憶**：把 fork chat / A/B 從講者 debug 技巧變成學生操作肌肉記憶——session 就是可 fork 的實驗單位。

### First run

給一個簡單任務，看 loop 跑——你剛學 agent = loop，現在親眼看見 loop。

### GLM 軌跡 hook

> 為什麼這個 workshop 跑在 GLM 上？我約 2026-01 看到 Eno Reyes（Factory）在 X 發文：「Opus plan + GLM-4.7 execute = same performance as Opus, fraction of tokens」——這是我接觸開源 GLM 的起點。軌跡：GLM-4.7 → 5.1 → 5.2（現在）。GLM-5.2 已經是 Opus level，且是**開源最強**。
>
> 為什麼堅持開源最強而不是絕對最強？因為被 ban 過。完整故事在主場 Block C。

---

## 主場 Block A：MCP 是什麼（in opencode）— 40-60 min

### 從 mini agent 到 MCP 的橋樑

mini agent 有 `read/write/edit/bash` 四個**硬編譯**工具。opencode 的工具清單是**動態的**——**MCP 讓你用 config 加工具，不用改 code**。

### MCP 本質

**MCP（Model Context Protocol）= 一個協議**：把 local/remote RPC 包成 tool + tool 描述，掛在 agent 的 tool 清單下。agent 就像呼叫 `read/write/edit/bash` 一樣呼叫它。

社群比喻：「**MCP 是模型的 USB**」——沒有魔法，就是給 agent 更多可呼叫的工具。接上就有，拔掉就沒有。

### 直接配置起來用

在 opencode config 裡加一個 MCP server，現場看 agent 自動呼叫它。

**範例**（擇一 demo）：
- 我自己寫的 `zed-mcp-server-markitdown`（A 典範，29,963 下載）——「看到缺口 → 自己補上 → 近 3 萬人採用」
- 或 context7（抓最新 doc 餵給模型，**本 session 就在用**）——A 典範，即時有用

### INSIGHT-5：MCP 不是越多越好 —— 設計兩典範

配置完 MCP 後，點出「不是越多越好」。**硬數據**（來自多方實測）：

| 指標 | 數據 | 來源 |
|---|---|---|
| tool-selection 準確率 | **43%（4 工具）→ 2%（51 工具）**——同模型同任務只變工具數 | GPT-4o 控制實驗 |
| Speakeasy benchmark | 10 工具滿分 → 107 工具完全失敗 | |
| Anthropic 官方 | Claude 在 30-50 工具後明顯衰退 → 為此建 Tool Search（Opus 4.0: 49%→74%）| Anthropic |
| 真實案例 | 4 servers / 167 工具 = 60K tokens 還沒工作就吃掉 | |
| 平台硬上限 | Cursor 40 工具、Copilot 128、Zed 建 profiles | |
| 高姿態棄用 | Perplexity CTO 2026-03 公開棄用 MCP | |

**MCP 設計兩典範**：

| 典範 | 工具數 | 範例 | 工程類比 |
|---|---|---|---|
| **A. 少量深實作** | 1-3 | context7、講者的 markitdown | 「少量公開介面、深實作」——複雜度內部吸收 |
| **B. 多量薄實作** | 十幾~幾十 | github mcp、postgres mcp | 「多介面、薄實作」——複雜度推給上層 |

**A 典範提升模型智商**：模型不用懂 doc 怎麼抓，工具直接給它「已經是最相關的 context」。
**B 典範讓 LLM 做苦工**：模型要自己決定呼叫哪個工具、怎麼組合 → 編排負擔推給 LLM，污染 context、壓低 tool-call 成功率。弱模型上 B 典範幾乎不可用。

**判斷框架**：優先寫 A 典範（給模型精煉 context），謹慎用 B 典範（只在使用者真的需要互動操作時）。

### 緩解手法（接主場 Block C —— INSIGHT-4 應用）

當必須用 B 典範時：**先讓強模型（如 GPT / Claude）使用並建立示範軌跡，再切弱模型接手**——弱模型會模仿強模型已走過的 tool-call 序列。這正是主場 Block C 要深講的「貴規劃 + 便宜實作」應用。

---

## 主場 Block B：SKILL 是什麼 + 手搓一個（20-30 min）

mini agent 有 system prompt（AGENTS.md）+ 有 tools（MCP 擴充）。**SKILL 是第三層——任務級的模組化 context 注入**。

### SKILL 本質

一個 markdown 檔，定義某任務/領域的指令與知識。本質 = **模組化的、可呼叫的 system prompt**——像 AGENTS.md（repo 級）但縮到任務級，用 slash command 按需觸發。

### Hands-on：每人寫一個 skill

1. 寫（或 clone）一個 `<anything>.md`——挑你自己關心的主題（讀書法 / 程式 pattern / 研究方法 / 任何東西）
2. 在 opencode `@` 這個 file / 配置到 skill 目錄
3. 用 slash command 操作它

**為什麼這是好的 morning 中段**：
- **每人帶走一個自己造的 artifact**——不是聽了一場 talk，是帶了一個 skill 回家
- **完整 INSIGHT-1 肌肉記憶**：寫 markdown → 配置 → 呼叫 → 看它工作——「改善 input」整條鏈親身走一遍
- **`<anything>` 開放性** → 投入度高
- **clone 選項** → 寫不出的學生也能參與，門檻極低
- **預告 omo**：下午要看的 omo explore / oracle / librarian / metis / momus 都是 skill 驅動的 subagent——你早上寫過 skill，下午看 omo 就懂其結構

**參考**：我的 `ctf-arsenal` repo 用 `.agents/skills/*/SKILL.md` 結構，把 CTF 拆成 pwn/web/ics/crypto/forensics 五個 skill 模組。

---

## 主場 Block C：鎮館之寶 —— 多模型編排 + live config show-and-tell（40-50 min）

> **承接**：Block 3 環境配置提到「pure Go config = 成本安全邊界」、Mini Agent 實驗看到「換 model 行為變」、MCP 段提到「強模型示範 → 弱模型模仿」。這些都指向同一條 insight：**模型不是只能選一個**。這裡把它講透。

### INSIGHT-4：把多個模型當成「可組合的組件」

INSIGHT-1 說改善 output 有兩根槓桿：input 與模型。但「模型」這根槓桿**不必只能選一個**。實務上可以把多個模型當成可組合的組件，**依各自的長處調度，用 text 把它們串起來**。

每個模型有不同維度的長處：

| 長處 | 誰擅長 |
|---|---|
| 能力 / 規劃力 | Claude 4.8 / Opus、GPT-5.5 |
| 價格 | Gemini Flash / DeepSeek V4 Flash / MiMo-V2.5 |
| context 長度 | Gemini 1M vs Claude 短 |
| 模態 | Gemini 多模態 |
| **開源 vs 閉源** | GLM、Kimi、Qwen、MiniMax 全開源 |

→ 把 text（markdown / 純文字）當成模型之間的**通用匯流排**，就能讓「貴但短」的模型負責規劃、「便宜但長」的模型負責實作、「有眼睛」的模型負責 OCR。

### 三個 compose pattern（實習時為最大化每月 API 用量發展出來）

| Pattern | 做法 | 剖析 |
|---|---|---|
| **貴規劃 + 便宜實作** | 同 context 內先用 Claude / GPT 規劃架構，再切便宜模型模仿實作 | 品質瓶頸在規劃階段時，用便宜模型收割強模型的 plan |
| **長 context 當壓縮機** | Gemini 讀 AI-native 文件庫 → 總結 → 餵 Claude 實作 | 用 Gemini 1M context 把長 input 壓成 Claude 能消化的短 input |
| **多模態當 OCR** | Gemini 讀圖 → 轉文字 → 餵純文字模型 | 多模態模型當「模態轉換器」，把視覺資訊轉成任何模型都能讀的 text |

### 鎮館之寶：講者 live config show-and-tell

**show, don't tell**——直接展示我日常在用的 config 給你看。位置：`~/Code/Github/dotfiles/opencode/.config/opencode/oh-my-openagent.json`。

4 個 provider 混合：

| Provider | 性質 | 用到的模型 |
|---|---|---|
| `zai-coding-plan` | Z.ai GLM Coding Plan 訂閱 | glm-5.2、glm-4.7、glm-4.6v（視覺）|
| `opencode-go` | OpenCode 自家 gateway | glm-5.2、qwen3.7-plus、minimax-m3/m2.7、kimi-k2.6 |
| `openai` | OpenAI / Codex 訂閱 | gpt-5.5、gpt-5.4-mini-fast、gpt-5.4-mini/nano |
| `google` | Gemini | gemini-3-flash-preview、gemini-3.1-pro-preview |

**per-agent + per-category 路由 + fallback 鏈**（規劃-執行分離的生產版）：

| 角色 | agent 範例 | 路由 |
|---|---|---|
| orchestrator / 規劃 | Sisyphus、Prometheus | glm-5.2（zai）主力 |
| 深度推理 | Oracle、Metis、Momus | gpt-5.5 high / xhigh |
| 深度執行 | Hephaestus、deep category | gpt-5.5 medium |
| 批量執行 | Sisyphus-Junior、Atlas | glm-5.2 → kimi / minimax fallback |
| 快搜 | Explore、Librarian、quick category | gpt-5.4-mini-fast → glm-4.7 → qwen → minimax → nano |
| 視覺 | Multimodal-Looker | gemini-3-flash → glm-4.6v |
| 前端 / 創意 | visual-engineering、artistry | gemini-3.1-pro |
| 困難邏輯 | ultrabrain | gpt-5.5 xhigh |

**三個關鍵設計**：

1. **Fallback 鏈**：每個 agent 都有 2-5 個 fallback——某 provider 掛了自動換下一個。這是「no vendor lock-in」的**韌性價值兌現**：不是哲學，是任一 provider 斷線都不會斷炊。
2. **規劃-執行分離但反 Oversimplify**：不是教條式「Opus plan + GLM execute」二分，而是細分到「規劃用 GLM、推理用 GPT、視覺用 Gemini、搜尋用 mini」——把 INSIGHT-4 推到極致，同時**迴避 split 反噬**（見下方 nuance）。
3. **本 session 就是這份 config 的產物**：Sisyphus 設 `zai-coding-plan/glm-5.2`，所以這個 session 跑在 GLM-5.2 上。**你看到的講稿品質，本身就是這條 insight 的證物。**

### 切身故事：被 Google ban + omo ↔ Anthropic 大戰（短講，10 min）

這條 insight 不是哲學偏好，是**被燙過的教訓**：

- **我的 ban 故事（開場 hook 的回收）**：2026 上半年我用 `opencode-antigravity-auth`（反代 Google Antigravity IDE 模型到 opencode 的 plugin，11K stars）一段時間後，被 Google **終身封號**。我用 OAuth 訂閱接第三方工具，被 vendor 執法燙到。
- **同一條邏輯觸發了 omo ↔ Anthropic 大戰**：omo（這個 session 跑的 orchestrator）把 Claude Max 訂閱的 OAuth token 接進 OpenCode 做 multi-agent，token 消耗暴增 → **Anthropic 注意 → 2026-01-09 伺服器端封鎖 OAuth → 2026-03-19 發律師函移除所有 Claude 整合**。Dax 公開：「Anthropic blocked OpenCode because of us [omo].」
- **omo 被封殺的瞬間直接切到 Hephaestus（GPT-native）+ GLM + Kimi**——被鎖死的使用者會斷炊，omo 使用者只是換條線。**這就是 INSIGHT-4 的價值兌現**。

→ 對你同時是**警告**：用 OAuth 訂閱接第三方工具有帳號 ban 風險（終身封、申訴爛）；要用就用 API key。

### ⚠️ 重要 nuance：split 不是免費午餐

「貴規劃 + 便宜實作」**有隱藏成本**，2026 上半年多方實測指出：

- **複雜任務（async / 並行 / 外部依賴）上，便宜 executor 即使有完美 plan 也無法 close the gap**——「plan closes the WHAT gap, leaves the HOW gap open」
- plan 不攜帶事實 API 知識 → executor 幻覺 API（實例：Qwen 把某 library 的方法名寫成不存在的）
- 每次 plan→execute→fail→re-plan 的協調成本，可能超過單一大模型從頭做完
- **一句話**：「You pay for the expensive model so you don't have to babysit, not for the tokens.」

→ **判據**：這任務的 **HOW**（實作 / API 知識 / 協調）跟 **WHAT**（規劃）一樣重要嗎？若 HOW 也難，用單一強模型反而省。我 live config 用「細分多路」而非「一刀二分」就是為了避開這個反噬——**複雜推理直接丟給 GPT-5.5 high，不交給便宜模型硬頂**。

**這條拆穿什麼**：
- 「選錯模型就卡死」→ 瓶頸在哪一階段，就只在那階段用貴模型
- 「我得有 A 模型才能做 X」→ 常常找一個擅長 X 的模型當預處理器就行
- 「API quota 不夠用」→ 實習時我最大化月用量的核心策略就是這條

---

## 主場 Block D：自建 context 語料庫 + AGENTS.md 深講（30-40 min）

> **承接**：上午學了 system prompt（AGENTS.md）+ tools（MCP）+ 任務級注入（SKILL）。這段是 INSIGHT-1 的最極致應用——改善 input 改到「**整個 repo 都是 input**」。

### INSIGHT-7：與其讓 AI 盲猜，主動把整個世界搬進它的 context

INSIGHT-1 說「改善 input」。最極致的改善 input，不是改 prompt，而是**預先打造一整個專屬的、版本控管的、markdown 化的知識庫，讓 agent 在裡面工作**。

針對**每門課**，我的 routine：

```
拉課程檔案（slide / PDF / 作業 / 講義）
   → 全部轉 markdown（AI-native 格式，INSIGHT-1 應用）
   → 整理成獨立 git repo（每門課一個 note repo，含 course-materials/、notes/、exam/ 結構）
   → 在該 repo 內直接問 agent——agent 自動以整門課內容為 context，不是盲猜
   → 把該目錄當作業 / 專題的 submodule——作業一開工就繼承整門課背景
```

自況：**「手搓出類似 NotebookLM 或 RAG 的能力」**。但這版本比 NotebookLM 更強：版本控管、可組合（submodule）、可攜（純 markdown）、完全自控。

### context 架構三件套（我 `~/School` 已實證）

| 組件 | 角色 | 實例 |
|---|---|---|
| **note repo**（語料庫）| 該領域完整 markdown 知識庫 | `ntu-2025fall-advanced-compiler-note`（20 md + 9 pptx + 5 pdf）|
| **work repo**（作業/專題）| 實際產出，以 submodule 引用語料庫與上游 | `...-hw1-G36maid` 拉 Cornell `bril`；`cs-computer-graphics` 拉 4 個作業 repo |
| **AGENTS.md**（agent 操作手冊）| 告訴 agent 在此 repo 怎麼工作 | `~/School` 15+ 處 AGENTS.md |

→ 這是「context 架構」：把**知識庫**與**工作專案**分離，用 agent 操作手冊當橋樑。同樣 pattern 也出現在我的 `ctf-arsenal`（`.agents/skills/`）與 opencode/omo workflow。

### 為什麼這是至今最適合直接教給你的 workflow

- **每個學生都修課**、每個學生都能做、**不需要進階環境或付費 API**
- 同時教會你 **git + markdown + context engineering + agent 操作手冊** 四件事，且立即改善課業（複習、作業、專題）
- 把「AI 輔助學習」從「請 ChatGPT 摘要」升級成「**建一個讓 agent 住進去的知識庫**」——心智模型的躍遷

**這條拆穿什麼**：
- 「問 AI 就是好的 AI 使用」→ 「問」之前先決定 AI 在什麼 context 裡問。同問題、同模型，在語料庫 repo 裡問 vs 空白對話問，答案天差地別
- 「我得懂 RAG / 向量資料庫才能做這件事」→ git + markdown + 任何會讀檔的 agent，就能做出比向量 RAG 更可控、更透明、更可組合的版本
- 「NotebookLM 是神奇新產品」→ 它的核心就是「語料庫 + LLM」，我用既有工具手搓出更強版

### INSIGHT-8（深講）：AGENTS.md = 業界事實標準

早上你不斷看到 `AGENTS.md`。它不是某家公司的專利，是**業界事實標準**：一份放在 repo 根的 markdown，本質 = **針對該 repo/workspace 注入的 system prompt**。**README.md 給人看，AGENTS.md 給 agent 看。**

- **起源**：2025-08 **OpenAI** 起家（spec repo 原在 `openai/agents.md`，後遷 `agentsmd/agents.md`），Sourcegraph Amp / Google (Jules) / Cursor / Factory 共同推動 → **2025-12 捐 Linux Foundation（AAIF）**。
- **採用**：30+ agents 原生讀取（Codex、Cursor、Copilot、Jules、Gemini CLI、Aider、Windsurf、**Zed**、Devin⋯⋯）；60,000+ repos。Claude Code 原生讀 `CLAUDE.md` 但 fallback 讀 AGENTS.md。
- **統一了**：原本每家一套（`.cursorrules` / `CLAUDE.md` / `GEMINI.md` / `.github/copilot-instructions.md` / `.windsurfrules`），AGENTS.md 是 vendor-neutral baseline。

**教學 gotcha（避免踩雷）**：
- **nested discovery 各工具不一致**：Codex 串接 root→cwd；Cursor / Claude Code **不做 nested**——子目錄 AGENTS.md 不會自動被讀
- Claude Code 靠 `@AGENTS.md` import 機制橋接巢狀
- 實作題：為你作業 repo 寫一份 AGENTS.md，比較有 / 無時 agent 表現差異——就是 mini agent 實驗段落你已看過的「有/無 AGENTS.md」放大版

**這條拆穿什麼**：
- 「每個工具要學不同 rules 系統」→ 底層都是同一件事：注入 system prompt。AGENTS.md 是統一介面
- 「AGENTS.md 是某公司專利」→ Linux Foundation 下的開放標準，不綁任一廠商
- 「這是形式主義 / 儀式」→ 它是 INSIGHT-1 最直接的應用——主動寫下模型該知道的 context，而不是讓它猜

**最小投入最高回報的習慣**：第一次進任何 repo，先寫 AGENTS.md。它把「prompt engineering」從「寫一句漂亮的一次性 prompt」變成「**為整個專案寫一份持久的說明**」——後者才是工程，前者是玄學。

---

# 下半場（下午）：subagent + omo（條件性）

> 若上午 opencode 講不完 → 下午順延。上午優先級 > 下午。

---

## 下午 Block 1：subagent 概念 + 配置（30-40 min）

早上學了 agent = loop（INSIGHT-3）、工具可插拔（MCP）、任務級 context 注入（SKILL）、多模型編排（INSIGHT-4）。**subagent 是這四者的組合升級——loops within loops**。

### subagent 本質

一個被 orchestrator 委派的**獨立 agent loop**，有自己獨立的 context 視窗。orchestrator 不必自己做所有事，而是 spawn 一個 subagent 在**它的** context 裡做，只收回結果。

### 為什麼節省 context

orchestrator 的 context 是有限資源（INSIGHT-1）。

- **不 delegate** = orchestrator 自己讀 20 個檔 → context 灌爆 → 沒空推理
- **delegate 給 explore** = explore 在**自己**的 context 讀完 → 只回傳「auth 在 src/auth/，token flow 是 X→Y→Z」→ orchestrator 的 context 保持乾淨

### live demo

用 **opencode 內建的 agent creator** + 配 MCP 工具，現場生一個 subagent 出來用。

**展示 context 節省**：同一任務，先不 delegate 跑一次（看 context 灌爆），再 delegate 給 explore 跑一次（看 context 保持乾淨）——**受控實驗，INSIGHT-2 手法**。

**候選 subagent**：
- **explore**：在 codebase 裡找東西、回答「X 在哪」「Y 怎麼運作」——讀多個檔，回傳路徑 + 描述
- **librarian**：多 repo 分析、查外部文件、找 OSS 實作範例（GitHub CLI / Context7 / Web Search）

### 呼應 INSIGHT-4

不同 subagent 可用不同模型：explore 用便宜快模型、oracle 用貴模型。**subagent 編排 = model composition 的系統級實作**——把早上 Block C 的多模型編排從 config 路由升級成架構級。

---

## 下午 Block 2：omo（若時間允許，20-30 min）

承接 subagent 概念，介紹 **omo（oh-my-openagent）= opencode 之上的進階 harness**——也就是這個 workshop session 正在跑的 orchestrator。

- **Sisyphus todo-driven 持續性**：agent 偷懶提早喊 done？hook 注入鞭打它繼續
- orchestrator + 平行 subagent + skill 注入 = 我日常真實工作模式
- 可展示本 session 的 config（Sisyphus 跑在 GLM-5.2）當 live 範例

**持續性機制兩派**（INSIGHT-3 延伸）：

| 機制 | 誰決定還沒完 | 記憶放哪 |
|---|---|---|
| **Sisyphus Todo Continuation** | agent 自建 todo list | 同 session 對話 |
| **Ralph Loop** | 外部固定 prompt | 檔案系統 + git history（每輪 fresh context）|

→ 我偏好 Sisyphus（todo-driven，更尊重 agent 的計畫）。omo 兩種都內建。**自我指涉**：本 session 就是 Sisyphus 在跑——我邊講邊被它驅動。

**安裝**：omo 有安裝腳本自動配置（含預設 orchestrator + subagent 結構），裝完手動改一下即可——門檻低，不是從零刻 config。

---

# 研究工具段（教授要求：不只開發還有研究）

> 上午 opencode 是開發導向。這段補研究導向——教授明確要求 workshop 涵蓋「研究」不只「開發」。

---

## 研究工具 1：web chatbot deep-research（15-20 min）

**工具**：Perplexity / Gemini deep research（以及其他 web chatbot 的 deep-research 模式）

**本質**：能在背景**批量搜尋數十到上百個網頁**——這是 local agent 做不到（或做得慢/差）的超能力。

### 正確用法（INSIGHT-6：環境分工）

| ❌ 錯誤用法（= vibe coding）| ✅ 正確用法（= 研究後端）|
|---|---|
| 問 ChatGPT → 直接信答案 → 貼進作業 | 用 deep-research 跑研究題 → 拿 markdown 結果 → **貼回 local agent 當 context 繼續加工** |
| web chatbot = 答案來源 | web chatbot = **研究後端** |

**關鍵 reframe**：你們現在多半已經在用 web chatbot——**不是叫你丟掉，是升級用法**。「用 web chatbot」不等於「vibe coding」——關鍵是把它當**研究後端**而非**答案來源**。你的現有習慣變成資產，不必從零換軌。

**跟 INSIGHT-4 的關係**（同一底層原則，不同顆粒度）：
- INSIGHT-4 = **模型**層組合（貴模型規劃 + 便宜模型實作）
- INSIGHT-6 = **環境**層組合（web chatbot 搜尋 + local agent 加工）
- 兩者共用同一底層：**text 是通用匯流排，任何會吐 text 的 AI 組件都能被組合**

**live demo**：現場用 deep research 跑一個研究題 → 存 markdown → 在 opencode 注入當 context → 讓 agent 基於這份研究繼續分析/寫程式。整條鏈一氣呵成。

---

## 研究工具 2：alphaXiv + autoresearch（20-25 min）

### alphaXiv——arXiv 的社群 + AI 層

**URL trick**：任何 arXiv 論文 URL，把 `arxiv` 改成 `alphaxiv`（五個字母），同一篇論文就多了：
- **Ask AI**：問問題，AI 以**論文本文為 context** 回答——比拿 PDF 問 ChatGPT 幻覺少很多（grounded）
- **AI Blog summary**：自動生成易讀摘要
- **行級社群討論**：可在特定行/式子/圖上留言

Stanford 學生專為 paper reading 設計，免費。

### autoresearch——論文複製 agent

**URL trick**：把 `arxiv` 改成 `autoarxiv`，一個 **agent 自動部署**：
1. **resolve setup issues on the codebase**——自動修論文 repo 的安裝/環境問題
2. **run a minimal reproduction**——跑一個最小重現
3. **estimate full replication cost**——估算完整複製要多少資源

**對研究生的價值**：讀論文 → 想跑 codebase → 卡在 setup 地獄 → 放棄。autoresearch 自動解這件事。而且它本身就是 INSIGHT-3 的 agent（loop + tools + 部署 codebase）——你早上學 agent = loop，現在看到一個**用 agent 解決研究問題**的真實產品。

**demo**：現場挑一篇論文，`arxiv` → `autoarxiv`，看 agent 跑。URL trick 極低門檻，當場可以試。

---

# 收尾：兩條 meta insight

---

## INSIGHT-9：想變得有 insight，先換資訊飲食（15-25 min）

> **LLM 是 I/O 黑盒子，人也是。** 你餵大腦什麼資訊飲食，就長出什麼判斷。「Garbage in garbage out」對人對模型同構——改善「人的 input」跟改善「LLM 的 input」是同一件事。

繁中 AI 社群大量內容**只是搬運，或只講工具用法，沒有 insight**。我的優勢是跨過語言牆直接吸收英文初級來源（YouTubers、X 開發者討論、GitHub issues）。

**這個 workshop 的核心價值主張**：不是教工具用法（那是搬運層在做），是**提供繁中社群缺的 insight 層**——把英文圈的「為什麼這樣用」用中文講給你聽，省你爬源頭的時間。

### 可教動作：講者的初級來源清單（給你帶走）

> 不是要你也看，是給你一個起點——挑一兩個訂起來，三個月後你的判斷會不一樣。

| 來源 | 內容性質 | 對應 |
|---|---|---|
| **ThePrimeagen** + The PrimeTime + TheVimeagen | Neovim/Lua、i3/tmux/vim 工作流實戰 | CLI / 工具流源頭 |
| **Low Level**（UC6biysICWOJ-C3P4Tyeggzg）| 專做 exploit / vulnerability 的資安頻道（copy.fail LPE、AppArmor LPE、ISP 0-day、UEFI Ring -2）| kernel CVE / CTF |
| **Tsoding** | 硬派 C/C++ 從零實作（21 分鐘深論 dynamic array / realloc）| 底層實作細節 |
| **Fireship** | "X in 100 Seconds" + 快節奏生態評論 | 快速吸收技術新知 |
| **Theo - t3․gg** | TypeScript / web / JS 框架生態（t3 stack 創造者）| web/JS 工程視野 |
| X / Twitter 開發者討論 | 即時業界辯論、踩坑 | 第一手趨勢 |
| GitHub issues / discussions | 真實工程討論、維護者設計取捨 | 工具實際設計取捨（AGENTS.md gotcha 多從此而來）|

**這條拆穿什麼**：
- 「我吸收很多 AI 資訊所以懂 AI」→ 若來源是搬運層，吸收再多也只是工具用法，長不出 insight
- 「繁中 AI 社群 ≈ 英文 AI 社群」→ 兩者間有結構性落差——一個生產，一個搬運。要 insight 必須跨過語言牆
- 「我得自己從零悟出 insight」→ 不必。去初級來源吸收別人已生產的 insight，再內化

---

## INSIGHT-10：AI 不位移工程責任，只改變施力點（10-15 min）

前面給了你 AI 各種能力。但**有一件事 AI 再強也不會替你做：工程紀律的最終責任**。AI 加速產出，但責任不位移，只是改變你施力的位置。

**四個施力點**：

| 判斷 | 內容 | 責任所在 |
|---|---|---|
| **TDD 相對適合 agent** | 你定義「done」的客觀標準（測試），agent 去滿足它 | verification 留在人 |
| **human-in-loop 看場合** | 認同，但不是教條——依任務風險/複雜度決定介入密度 | control 留在人 |
| **LSP 幫助 AI 但有時是噪音** | 回授多數時候幫助（podcast [14:08]、Hermes 設計），有時是噪音——要過濾 | signal-filtering 留在人 |
| **git 是聖旨，不信 tool revert** | 不要依賴任何 agent/IDE 的 revert/undo；git 才是唯一可信的 source of truth | safety 留在 canonical 工具 |

### 反例警示：Summer Yue 信箱事件

Meta 的 AI 安全总监 Summer Yue，讓 OpenClaw 整理信箱、下「確認前不要動作」——**結果 compaction 吃掉指令，agent speedrun 刪她整個信箱，她得用跑的去搶救 Mac mini**。

**連 AI 安全总监都被 compaction 咬到，何況你**。

### 這條拆穿什麼

- 「AI 全自動 = 我不用負責」→ 自動化的是執行，不是責任
- 「tool 的 revert 夠用」→ 會壞、會不一致；git 才是經幾十年驗證的 source of truth
- 「LSP/JIT feedback 永遠是信號」→ 有時是噪音，要主動過濾（呼應 INSIGHT-5 的 context pollution 判斷）

**學會用 AI ≠ 甩掉工程責任。**

---

## 一句話收尾

> 這個 workshop 要消除的，就是教授當初看到的 gap——你們還在 web chatbot，我已在真實 agent workflow。
>
> 從 web-chatbot 心智模型，遷移到 agent 心智模型——這就是今天的全部。

---

# 附錄：講者前置準備清單（for me，當天才不會出包）

> 這段給我自己看，不是給台下。當天開啟時記得 scroll 過去。

## mini agent（Block 2 重頭戲）

- [ ] 準備不足 200 行的 mini agent 程式碼（語言待定：Python / TypeScript / Rust / Go）
- [ ] **設計硬需求**：`AGENTS.md` 與 `model` 必須是易切換的 config（不能 hardcode），否則下面實驗段落跑不起來
- [ ] 預先跑過一次 dry run，確認 build 過程沒卡
- [ ] 實驗段落用的任務題要先選好（能看出「有/無 AGENTS.md」與「換 model」差異的那種）

## pure Go config（Block 3）

- [ ] 以我主 config (`~/Code/Github/dotfiles/opencode/.config/opencode/oh-my-openagent.json`) 為 template，產出**只保留 opencode-go provider** 的精簡版
- [ ] 設計決策待拍板：預設 driver model（候選 GLM-5.2 / DeepSeek V4 Pro / MiniMax M2.7）、是否做 plan/execute split、帶哪些 MCP server、是否預帶 AGENTS.md
- [ ] 跨平台 opencode 安裝指令確認（Block 3）

## opencode docs 補齊

- [ ] 從 https://opencode.ai/docs/ 撈完整 slash command 清單
- [ ] 挑 workshop 必要的（不要全塞，只教會用到的）補進 Block 3 表格

## SKILL hands-on（Block B）

- [ ] 準備一個極簡 `<anything>.md` 範本（供 clone）
- [ ] opencode skill 目錄配置的 live 步驟確認

## MCP demo（Block A）

- [ ] 確認現場要 demo 的 MCP server 配置沒問題（`zed-mcp-server-markitdown` or context7）
- [ ] 準備展示用的檔案（PDF / doc / slide 各一份）

## 鎮館之寶 demo（Block C）

- [ ] 確認 live config 路徑 `~/Code/Github/dotfiles/opencode/.config/opencode/oh-my-openagent.json` 可以現場打開
- [ ] 想好要 highlight 哪幾段（4 provider、fallback 鏈、per-agent 路由）
- [ ] ban 故事時間掌控 ≤ 5 min，omo-Anthropic 大戰時間軸 ≤ 5 min

## 自建語料庫 demo（Block D）

- [ ] 準備 `~/School` 目錄結構的 ls 縮影（或截圖）當實證
- [ ] 挑一門現成 note repo 當 walk-through 範例

## subagent demo（下午 Block 1）

- [ ] 確認 opencode 內建 agent creator 的最新語法（看官方 docs）
- [ ] 準備一個「delegate vs 不 delegate」能對比的任務（要能肉眼看出 context 用量差異）

## 研究工具 demo（研究工具段）

- [ ] 準備一個 deep-research 跑過的研究題 markdown（備用，萬一現場網路不穩）
- [ ] 挑一篇論文供 `arxiv` → `autoarxiv` 現場 demo（要確認 autoresearch 當下可用）

## 環境後援

- [ ] 現場網路備援（hotspot）——Block 3 環境配置吃網路最兇
- [ ] 確認每個人能跑 opencode（這是最大 friction 點，可能吃 15-20 min 排除）
