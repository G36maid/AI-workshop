# AI Agent Workshop — 從 web chatbot 到 agent 心智模型

> **講者**：G36maid（NTNU CS/ME 大四）
> **受眾**：實驗室大學 / 碩士生
> **形式**：整天 workshop，9am ~ 下午，約 3-6 小時
> **北極星**：帶你從 web-chatbot 心智模型，遷移到 agent 心智模型。

---

## 這個 workshop 不是什麼 / 是什麼

**不是**：工具教學（那是搬運層在做的事）、不是教你怎么按 Cursor、不是「養龍蝦」。

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

（完整故事留到後面 INSIGHT-4 重講。這裡只是建立「這人玩真的、會燙到」的份量。）

---

## Block 2：祛魅 —— AI / Agent 到底是什麼（40-60 min）

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

### 🛠️ Mini Agent 現場實作（Block 3 重頭戲）

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
- INSIGHT-8 預告：`AGENTS.md` = system prompt
- INSIGHT-5 預告：`read/write/edit/bash` 是工具，MCP 是擴充來源

**build 完後**，我指著 opencode 說：「**它就是這個，只是工具更多、context 管理更精細、加上生產級 polish**。」——你親眼看過原型，opencode 從此不是魔法。

---

### 🧪 Mini Agent 實驗段落（互動）

build 完不是結束——同一個 mini agent 立刻當實驗台：

| 實驗 | 做法 | 看見什麼 |
|---|---|---|
| **有/無 AGENTS.md** | 同一任務，先沒 AGENTS.md 跑一次，加上再跑一次 | agent 行為天差地別——**寫不寫 AGENTS.md，表現差很多**當場被驗證 |
| **各家 model 對照** | 同一 agent + 同一 AGENTS.md，換 Go 的不同模型跑同一任務 | 同一個 loop、不同模型 → 品質/風格/能力落差一目了然 |

**為什麼這組實驗強**：都是「同 agent、變一個維度、比 output」——這正是 INSIGHT-2 的受控實驗手法，你邊玩邊內化。

---

## Block 3：環境配置（30-40 min）

接下來讓每個人跑起來。

### opencode 安裝

```bash
# macOS / Linux
curl -fsSL https://opencode.ai/install | bash

# 講者自己用 Arch pacman；跨平台指令見 opencode.ai/docs
```

### opencode Go 訂閱（$5 首月，整天夠用）

**為什麼選 Go**：低門檻、14 個強開源模型一把抓、額度對整天 workshop 綽綽有餘、零資料留存。

| 項目 | 內容 |
|---|---|
| 月費 | **$5 首月**，之後 $10/月 |
| 5 小時上限 | $12 等同用量（對單一 session 綽綽有餘）|
| 伺服器 | US / EU / Singapore |
| 資料政策 | **zero data retention** |

**收錄模型**：GLM-5.2（我日常 driver）、GLM-5.1、Kimi K2.7/K2.6、MiniMax M3/M2.7、Qwen3.7、DeepSeek V4 等 14 個開源模型。

### 套用 Pure Go Config

我準備了一份 **pure Go config**（只路由到 opencode-go provider，不會燒到昂貴 frontier 模型）——這是**成本安全邊界**：無論你怎麼 hammer，最大燒掉就是 Go 額度。

### 基本指令

| 指令 | 作用 | 為什麼需要 |
|---|---|---|
| `/init` | 初始化 session / 專案設定 | 進任何 repo 第一步——呼應 INSIGHT-8（AGENTS.md）|
| `/compact` | 壓縮對話 context | 對話太長時搶救——context 是有限資源 |
| `/session` | session 管理（list / resume / **fork**）| 呼應 INSIGHT-2 的 fork A/B |
| `/models` | 切換模型 | mini agent 的 model-swap 實驗，現在換你操作 |

### First run

給一個簡單任務，看 loop 跑——你剛學 agent = loop，現在親眼看見 loop。

### GLM 軌跡 hook

> 為什麼這個 workshop 跑在 GLM 上？我約 2026-01 看到 Eno Reyes（Factory）在 X 發文：「Opus plan + GLM-4.7 execute = same performance as Opus, fraction of tokens」——這是我接觸開源 GLM 的起點。軌跡：GLM-4.7 → 5.1 → 5.2（現在）。GLM-5.2 已經是 Opus level，且是開源最強——這跟我的 no-vendor-lock-in 哲學一致。

---

## 主場 Block A：MCP 是什麼（in opencode）

mini agent 有 `read/write/edit/bash` 四個**硬編譯**工具。opencode 的工具清單是**動態的**——**MCP 讓你用 config 加工具，不用改 code**。

### MCP 本質

**MCP（Model Context Protocol）= 一個協議**：把 local/remote RPC 包成 tool + tool 描述，掛在 agent 的 tool 清單下。agent 就像呼叫 `read/write/edit/bash` 一樣呼叫它。

社群比喻：「**MCP 是模型的 USB**」——沒有魔法，就是給 agent 更多可呼叫的工具。接上就有，拔掉就沒有。

### 直接配置起來用

在 opencode config 裡加一個 MCP server，現場看 agent 自動呼叫它。

**範例**（擇一 demo）：
- 我自己寫的 `zed-mcp-server-markitdown`（A 典範，29,963 下載）——「看到缺口 → 自己補上 → 近 3 萬人採用」
- 或 context7（抓最新 doc 餵給模型，本 session 就在用）

### ⚠️ INSIGHT-5 預告：MCP 不是越多越好

配置完 MCP 後，點出「不是越多越好」。**硬數據**（來自多方實測）：

| 指標 | 數據 |
|---|---|
| tool-selection 準確率 | **43%（4 工具）→ 2%（51 工具）**——同模型同任務只變工具數 |
| Speakeasy benchmark | 10 工具滿分 → 107 工具完全失敗 |
| Anthropic 官方 | Claude 在 30-50 工具後明顯衰退 |
| 真實案例 | 4 servers / 167 工具 = 60K tokens 還沒工作就吃掉 |
| 平台硬上限 | Cursor 40 工具、Copilot 128、Zed 建 profiles |

**MCP 設計兩典範**：
- **A 典範（少量深實作）**：每個工具把複雜度在內部消耗，輸出精煉 context（如 context7、我的 markitdown）→ **提升模型智商**
- **B 典範（多量薄實作）**：把服務原樣暴露（如 github mcp 幾十個工具）→ **讓 LLM 做苦工**，且污染 context、壓低 tool-call 成功率

**判斷框架**：優先寫 A 典範（給模型精煉 context），謹慎用 B 典範。

---

## 主場 Block B：SKILL 是什麼 + 手搓一個（早上 finale）

mini agent 有 system prompt（AGENTS.md）+ 有 tools（MCP 擴充）。**SKILL 是第三層——任務級的模組化 context 注入**。

### SKILL 本質

一個 markdown 檔，定義某任務/領域的指令與知識。本質 = **模組化的、可呼叫的 system prompt**——像 AGENTS.md（repo 級）但縮到任務級，用 slash command 按需觸發。

### Hands-on：每人寫一個 skill

1. 寫（或 clone）一個 `<anything>.md`——挑你自己關心的主題（讀書法 / 程式 pattern / 研究方法 / 任何東西）
2. 在 opencode `@` 這個 file / 配置到 skill 目錄
3. 用 slash command 操作它

**為什麼這是好的 morning finale**：
- **每人帶走一個自己造的 artifact**——不是聽了一場 talk，是帶了一個 skill 回家
- **完整 INSIGHT-1 肌肉記憶**：寫 markdown → 配置 → 呼叫 → 看它工作——「改善 input」整條鏈親身走一遍
- **`<anything>` 開放性** → 投入度高

**參考**：我的 `ctf-arsenal` repo 用 `.agents/skills/*/SKILL.md` 結構，把 CTF 拆成 pwn/web/ics/crypto/forensics 五個 skill 模組。

---

# 下半場（下午）：subagent + omo（條件性）

> 若上午 opencode 講不完 → 下午順延。上午優先級 > 下午。

---

## 下午 Block 1：subagent 概念 + 配置

早上學了 agent = loop（INSIGHT-3）、工具可插拔（MCP）、任務級 context 注入（SKILL）。**subagent 是這三者的組合升級——loops within loops**。

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
- **explore**：在 codebase 裡找東西、回答「X 在哪」「Y 怎麼運作」
- **librarian**：多 repo 分析、查外部文件、找 OSS 實作範例

---

## 下午 Block 2：omo（若時間允許）

承接 subagent 概念，介紹 **omo（oh-my-openagent）= opencode 之上的進階 harness**——也就是這個 workshop session 正在跑的 orchestrator。

- **Sisyphus todo-driven 持續性**：agent 偷懶提早喊 done？hook 注入鞭打它繼續
- orchestrator + 平行 subagent + skill 注入 = 我日常真實工作模式
- 可展示本 session 的 config（Sisyphus 跑在 GLM-5.2）當 live 範例

**持續性機制兩派**（INSIGHT-3 延伸）：
- **Sisyphus**：看 agent 自建 todo list，未完就繼續
- **Ralph Loop**：每次結束就把同一 prompt 重新注入，靠檔案系統當記憶

---

# 研究工具段（教授要求：不只開發還有研究）

上午 opencode 是開發導向。這段補研究導向。

---

## 研究工具 1：web chatbot deep-research

**工具**：Perplexity / Gemini deep research

**本質**：能在背景**批量搜尋數十到上百個網頁**——這是 local agent 做不到的超能力。

### 正確用法（INSIGHT-6：環境分工）

| ❌ 錯誤用法（= vibe coding）| ✅ 正確用法（= 研究後端）|
|---|---|
| 問 ChatGPT → 直接信答案 → 貼進作業 | 用 deep-research 跑研究題 → 拿 markdown 結果 → **貼回 local agent 當 context 繼續加工** |
| web chatbot = 答案來源 | web chatbot = **研究後端** |

**關鍵 reframe**：你現在多半已經在用 web chatbot——**不是叫你丟掉，是升級用法**。「用 web chatbot」不等於「vibe coding」——關鍵是把它當**研究後端**而非**答案來源**。你的現有習慣變成資產，不必從零換軌。

**live demo**：現場用 deep research 跑一個研究題 → 存 markdown → 在 opencode 注入當 context → 讓 agent 基於這份研究繼續分析/寫程式。

---

## 研究工具 2：alphaXiv + autoresearch（arXiv 論文閱讀與複製）

### alphaXiv——arXiv 的社群 + AI 層

**URL trick**：任何 arXiv 論文 URL，把 `arxiv` 改成 `alphaxiv`（五個字母），同一篇論文就多了：
- **Ask AI**：問問題，AI 以**論文本文為 context** 回答——比拿 PDF 問 ChatGPT 幻覺少很多（grounded）
- **AI Blog summary**：自動生成易讀摘要
- **行級社群討論**：可在特定行/式子/圖上留言

Stanford 學生專為 paper reading 設計，免費。

### autoresearch——論文複製 agent

**URL trick**：把 `arxiv` 改成 `autoarxiv`，一個 **agent 自動部署**：
1. resolve setup issues on the codebase——自動修論文 repo 的安裝/環境問題
2. run a minimal reproduction——跑一個最小重現
3. estimate full replication cost——估算完整複製要多少資源

**對研究生的價值**：讀論文 → 想跑 codebase → 卡在 setup 地獄 → 放棄。autoresearch 自動解這件事。而且它本身就是 INSIGHT-3 的 agent（loop + tools + 部署 codebase）——你早上學 agent = loop，現在看到一個**用 agent 解決研究問題**的真實產品。

**demo**：現場挑一篇論文，`arxiv` → `autoarxiv`，看 agent 跑。URL trick 極低門檻，當場可以試。

---

# 收尾：兩條 meta insight

---

## INSIGHT-9：想變得有 insight，先換資訊飲食

> **LLM 是 I/O 黑盒子，人也是。** 你餵大腦什麼資訊飲食，就長出什麼判斷。「Garbage in garbage out」對人對模型同構。

繁中 AI 社群大量內容**只是搬運，或只講工具用法，沒有 insight**。我的優勢是跨過語言牆直接吸收英文初級來源（YouTubers、X 開發者討論、GitHub issues）。

**這個 workshop 的核心價值主張**：不是教工具用法（那是搬運層在做），是**提供繁中社群缺的 insight 層**——把英文圈的「為什麼這樣用」用中文講給你聽，省你爬源頭的時間。

**可教動作**：想變得有 insight，**先換資訊飲食**——訂閱英文初級來源、追蹤 GitHub issues。這是少數能直接「教」的 meta-skill。

---

## INSIGHT-10：AI 不位移工程責任，只改變施力點

前面給了你 AI 的各種能力。但**有一件事 AI 再強也不會替你做：工程紀律的最終責任**。AI 加速產出，但責任不位移，只是改變你施力的位置。

**四個施力點**：

| 判斷 | 內容 | 責任所在 |
|---|---|---|
| **TDD 相對適合 agent** | 你定義「done」的客觀標準（測試），agent 去滿足它 | verification 留在人 |
| **human-in-loop 看場合** | 認同，但不是教條——依任務風險/複雜度決定介入密度 | control 留在人 |
| **LSP 幫助 AI 但有時是噪音** | 回授多數時候幫助，有時是噪音——要過濾 | signal-filtering 留在人 |
| **git 是聖旨，不信 tool revert** | 不要依賴任何 agent/IDE 的 revert/undo；git 才是唯一可信的 source of truth | safety 留在 canonical 工具 |

**反例警示**：Meta 的 AI 安全总监 Summer Yue，讓 OpenClaw 整理信箱、下「確認前不要動作」——結果 compaction 吃掉指令，agent speedrun 刪她整個信箱，她得用跑的去搶救 Mac mini。**連 AI 安全总监都被 compaction 咬到，何況你。**

**這條拆穿什麼**：
- 「AI 全自動 = 我不用負責」→ 自動化的是執行，不是責任
- 「tool 的 revert 夠用」→ 會壞、會不一致；git 才是經幾十年驗證的 source of truth
- 「LSP/JIT feedback 永遠是信號」→ 有時是噪音，要主動過濾

**學會用 AI ≠ 甩掉工程責任。**

---

## 一句話收尾

> 這個 workshop 要消除的，就是教授當初看到的 gap——你們還在 web chatbot，我已在真實 agent workflow。
>
> 從 web-chatbot 心智模型，遷移到 agent 心智模型——這就是今天的全部。
