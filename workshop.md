# AI Agent Workshop — 從 web chatbot 到 agent 心智模型

> **講者**：G36maid（NTNU CS/ME 大四）
> **形式**：整天 workshop，9am ~ 下午，約 3-6 小時
> **核心**：帶你從 web-chatbot 心智模型，遷移到 agent 心智模型。

---

## 議程（at a glance）

> 這整張講稿是我當天開著念、也給台下看的同一份。

### 上半場（早上）：pure opencode

| 段落 | 時間估計 | 對應 insight |
|---|---|---|
| Block 1：自我介紹 | 10-15 min | INSIGHT-9（誠實定位）|
| Block 2：祛魅 — AI / Agent 到底是什麼 + Mini Agent 現場實作 + 實驗 | 60-90 min | INSIGHT-1, 2, 3 |
| Block 3：環境配置 + First run | 30-40 min | INSIGHT-3, 8 |
| 主場 Block A：MCP 是什麼、直接配起來、兩種不同的設計思路 | 40-60 min | INSIGHT-5 |
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

> 講者備註：上述時間僅供參考

---

## 這個 Workshop 不是什麼 / 是什麼

**不是**：單純的工具教學（那是搬運工才做的事）、不是教你怎麼操作 Cursor，更不是教你「養龍蝦」。

**是**：一次**心智模型遷移**。很多人只把 ChatGPT 當作解答機——複製答案後貼上到 IDE。但我想帶大家看到的是：LLM 本質上是一個 I/O 黑盒子，而 Agent 就是圍繞著它運作的一個 loop。你完全可以控制餵進去的 input，我們要思考的是如何真正善用這些工具，來完成人類需要的任務，進而大幅加速我們的開發與研究。

**定位**：今天我會分享自己的心路歷程，把英文圈的精華 insight 消化後直接講給你聽，幫你省下去爬原文的時間。此外，我也會隨性聊聊一些我自己想分享的觀察。

---

# 上半場（早上）：pure opencode

整個早上，我們都會在 **OpenCode**（一款開源的 Coding Agent）裡面跑。這也是我平常開發的 Daily Driver（主力工具）。
你可以把它想像成是開源版的 Claude Code。

🔗 https://opencode.ai/

### 什麼是 OpenCode？

OpenCode 是一個開源的 AI Agent，能協助你在終端機 (Terminal)、IDE 或是桌面應用程式中編寫程式碼。

**核心特色：**
*   **支援 LSP**：能為 LLM 自動載入合適的 LSP (Language Server Protocol)。
*   **多工作階段 (Multi-session)**：允許在同一個專案中，平行啟動多個 Agent 處理不同任務。
*   **分享連結**：能將任意工作階段生成連結，分享給其他人參考或協助 Debug。
*   **整合 GitHub Copilot**：可透過 GitHub 登入，直接連接並使用你的 Copilot 帳號。
*   **整合 ChatGPT Plus/Pro**：可透過 OpenAI 登入，直接使用你的 ChatGPT Plus/Pro 帳號。
*   **支援任意模型**：透過 Models.dev 介接超過 75 家 LLM 供應商，也支援串接 Local（本地端）模型。
*   **支援任意環境**：提供終端機介面、桌面版 App，以及 IDE 擴充套件等多種使用形式。

📚 官方文件：https://opencode.ai/docs/

---

## Block 1：自我介紹（10-15 min）

### 關於我 (Who am I)

🔗 GitHub: https://github.com/G36maid

我熱衷於系統工程與資安領域的研發，並活躍於開源社群。我是 **Zed** (Rust-based Editor) 的 Contributor，同時也是 Zed Guild Bug Bashers 的成員，曾為 Zed 與 OpenCode 貢獻過程式碼。

*   **開源里程碑**：我開發的 [`zed-mcp-server-markitdown`](https://zed.dev/extensions?filter=context-servers) 在 Zed 擴充商店已累積近 3 萬次下載。
*   **技術守備範圍**：日常使用 Arch Linux、熱愛 Rust、有在打 CTF，也是個 Homelab 玩家。
*   **我的 AI 哲學**：我看待 AI 的方式，就和我看待 OS Kernel 的方式一樣。

let's all love lain." 
Arch user, 
homelab host, 
Rust enthusiast. 
CS / ME @NTNU  
- building systems, breaking illusions

https://github.com/G36maid 

### 🍟 開胃菜

> 「你們有人把 ChatGPT / Claude / Gemini 的訂閱，接進去其他工具的 Plugin 使用過嗎？」

你們有想過，要如何用**最少、最低的成本**打完一場 CTF 嗎？
或者是，嘗試將一整個學期的魔王課程，甚至是公司累積的 Jira Tickets，**全部外包給 AI 處理，而且還能做得盡善盡美？**

如果你覺得這還不夠瘋狂，那有沒有試過：
*   **【架構理解】**：面對一個萬行起跳的未知開源專案，在己分鐘內讓 Agent 幫你摸透底層邏輯，並直接畫出系統架構圖？
*   **【基礎設施】**：丟一張隨手說的架構草圖，讓 AI 直接幫你寫完所有 Docker Compose 或 Kubernetes 的設定檔，一鍵部署到你的 Homelab？
*   **【資安與逆向】**：打 CTF 時，把一顆完全看不懂的 Binary 丟進去，讓 Agent 幫你做逆向分析，甚至連 Pwntools 的 Exploit Script 都順手幫你寫好？
*   **【程式碼重構】**：面對一坨公司的祖傳 Legacy Code，讓 Agent 像外科醫生一樣，精準地把這坨義大利麵重構成安全的程式碼？

這就是我們今天要聊的：**當你把 LLM 裝上「手腳」變成 Agent 後，它能做到的極限在哪裡。**


---

## Block 2：祛魅 —— AI / Agent 到底是什麼（60-90 min）

這段是整個上午的知識核心。接下來的三個 Insight，將是完成「心智模型遷移」的階梯：**一旦你看穿 Agent 根本不是魔法，就會發現 OpenCode 說穿了，就只是一個「刻得很好的 Loop」而已。**

---

### INSIGHT-1：LLM 本質上就是個 I/O 黑盒子

不管外面包裝成 Chatbot、Agent，**LLM 說到底就是一台根據 Input 吐出 Output 的機器**。這跟最陽春的 Web Chatbot **在最底層沒有任何本質上的差別**。

**要改善 Output 的品質，你手上只有兩根槓桿**：
1. **改善 Input（也就是 Context，上下文）** ← 這是今天 80% 的重點。
2. **換一個更強的模型**。

市面上其餘所有花俏的名詞與技術（例如 Prompt、RAG、MCP、Skills、LOOP、HOOK⋯⋯），**全部都只是用來「改善 Input/O」的不同實作方式而已**。

**這個觀念能幫我們打破什麼迷思？**
*   **「AI 是魔法」** → 根本沒有魔法，純粹就是 I/O。
*   **「Vibe Coding」**（無腦按 Enter，不去塑造 Input） → 這等於是把產出的品質，完全交給模型當下的隨機性來決定，但我們可以改善他。
*   **「換個工具就會變強」** → 很多時候，新工具只是換了一種「包裝 Context 的方法」而已。

**💻 Live Demo**：
等等我會現場展示：同一個模型，在不同 Input 下，Output 會如何天差地別（我從早期的 Zed Text-thread 時代，就是靠這招來徹底搞懂 Context 運作原理的）。

---

### INSIGHT-2：把 LLM 當作系統來 Debug

LLM 雖然是個黑盒子，但不代表我們不能研究它——**工程師面對任何未知的黑盒子，用的其實都是同一套經驗與方法**。把 LLM 當作系統來 Debug，而不是把它當成「神諭」來求神問卜。

**四個 Debug 手法**（其實都是你日常開發早就在用的技巧）：

| LLM 操作手法 | 對應的工程概念 | 在 LLM 上的實質意義 |
| :--- | :--- | :--- |
| **重新 Roll 一次 (Re-generate)** | 重新跑一次測試 | 探索 Output 的機率分佈——這個答案是真正穩健，還是剛好運氣好？ |
| **修改 Input + Re-roll** | 調整參數後重跑 | 呼應 INSIGHT-1 的主迴圈：不斷迭代並塑造更好的 Context。 |
| **Fork 對話 / 雙 Thread A/B 測試** | 進行受控實驗 | 每次只變動一個維度並比較 Output，藉此釐清究竟是哪個 Input 因子發揮了作用。 |
| **偷看 Thinking Process (思考過程)** | 查閱 Stack Trace | 稍微打開黑盒子，檢查它的推理鏈 (Reasoning Chain) 在哪一步走偏了。 |

**實驗**：
用同一道題目，讓大家一起 Re-roll，親眼見證結果的差異。模型單次給出的 Output，永遠只是機率分佈裡的「其中一個樣本」，有時候多抽幾次，才能找到我們真正需要的答案。

---

這段內容是整個 Workshop 最具震撼力的高潮！透過實際展現一段簡單的程式碼來打破迷思（祛魅），非常有說服力。

我幫你增強了講述時的「戲劇張力」與「工程師直覺」，把程式碼的註解稍微對齊，並優化了表格與實驗段落的敘述，讓台下的聽眾能更順暢地跟著你的邏輯走。

```markdown
### INSIGHT-3：Agent 說穿了就是一個 Loop

> 💡 **觀念出處**：這段源自 Adam 在 ThePrimeagen Standup Podcast [04:32] 中的定義：「Agent = LLM + Tools + Loops」。這也是我建構這個心智模型的起點。

所謂的「AI Agent」根本不是什麼神祕的新科技，**它本質上就是一個迴圈 (Loop)**：

1. 給 LLM 一組 System Prompt 與工具定義（如 Read / Write / Edit / Bash 等）。
2. LLM 根據 Input 吐出 Output。
3. 若 Output 符合呼叫工具的格式 → 執行該工具，並將執行結果回灌到 Context 中。
4. 將更新後的 Context 再次送給 LLM。
5. 不斷重複，直到 LLM 判斷任務完成並自己決定停止。

**所謂的「Agentic 魔法」，說穿了就只是這五行 `while loop`。**

* **「Agent 是某種新型態的 AI」** → 錯，Agent = LLM + While Loop + Tools，核心依舊是那個 I/O 黑盒子。
* **「Agent 具備自主思考能力」** → 它並沒有真的在「想」，每一次的迴圈依然是死板的「給 Input、吐 Output」。
* **「各家 Agent 框架都很神祕高深」** → 無論是 Claude Code、Cursor Agent、Gemini CLI、Zed Agent、OpenCode 還是 Cline⋯⋯**底層全都是這個 Loop 的不同實作而已**。

---

### 🛠️ Mini Agent 現場實作（Block 2 重頭戲）

我現在直接從零刻一個 Mini Agent 給你看。**不到 200 行程式碼**，核心結構大概長這樣：

```python
system_prompt = load("AGENTS.md")            # ← 預告 INSIGHT-8：AGENTS.md 就是 System Prompt
tools = [read, write, edit, bash]            # ← 預告 INSIGHT-5：這些是「內建工具」，MCP 則是擴充來源
model = config["model"]                      # ← Config-driven，可隨時切換（稍後實驗段落會用到）

messages = [{"role": "system", "content": system_prompt}]
messages.append({"role": "user", "content": user_task})

while True:                                  # ← INSIGHT-3 本體：Agent 就是這個 Loop
    response = llm_call(model, messages, tools)
    messages.append(response)

    if response.has_tool_call():
        result = execute_tool(response.tool_call)   # 執行工具
        messages.append(tool_result(result))        # 將結果回灌至 Context
    else:
        break                                       # LLM 判斷結束，自行停止

```

**這段簡單的 Code，同時展示了我們今天談到的多個 Insight**：

* **INSIGHT-1**：Loop 裡的 `llm_call` 依然是那個單純的 I/O 黑盒子。
* **INSIGHT-3**：Agent 的核心 Loop 結構。
* **INSIGHT-4 (預告)**：`config["model"]` 是可以切換的——暗示同一個 Loop，裝上不同的 Model 就等於換了個大腦（這會在主場 Block C 深入探討）。
* **INSIGHT-8 (預告)**：`AGENTS.md` 在系統中的定位就是 System Prompt。
* **INSIGHT-5 (預告)**：`read/write/edit/bash` 是基本工具，而 MCP 將是未來擴充工具的來源。

**Demo 結束後**，我會指著 OpenCode 告訴大家：「**OpenCode 其實就是這個東西。它只是內建了更多工具、把 Context 管理做得更精細，並加上了 Production-ready 的打磨而已。**」——當你親眼看透了原型，OpenCode 對你來說就不再是魔法了。

---

### 🧪 Mini Agent 實驗段落（互動）

寫完 Agent 不是重點，接下來我們直接把這支 Mini Agent 當作實驗台：

| 實驗目標 | 測試做法 | 我們會看見什麼？ |
| --- | --- | --- |
| **AGENTS.md 的威力** | 同一個任務，先在「沒有」AGENTS.md 的情況下跑一次，加上後再跑一次。 | Agent 的行為天差地別——當場驗證**寫不寫 AGENTS.md，表現真的差很多**。 |
| **各家 Model 大亂鬥** | 同一個 Agent + 同一份 AGENTS.md，抽換成不同的 LLM 去跑同一個任務。 | 同一個 Loop，換不同模型 → 品質、風格、能力落差一目了然，同時也為 Block C 的「多模型編排」埋下伏筆。 |

**為什麼要做這組實驗？**
因為這完美示範了「同一個 Agent、只改變一個維度、比較 Output 差異」的過程。這正是我們在 INSIGHT-2 提到的實驗手法，讓你在實作中直接內化這個 Debug 心法。


## Block 3：環境配置（30-40 min）

接下來的環節，我們要把環境架起來，確保大家都能在自己的電腦上實際跑動 Agent。

### 1. 安裝 OpenCode

```bash
# YOLO
curl -fsSL https://opencode.ai/install | bash

# Package managers
npm i -g opencode-ai@latest        # or bun/pnpm/yarn
scoop install opencode             # Windows
choco install opencode             # Windows
brew install anomalyco/tap/opencode # macOS and Linux (recommended, always up to date)
brew install opencode              # macOS and Linux (official brew formula, updated less)
sudo pacman -S opencode            # Arch Linux (Stable)
paru -S opencode-bin               # Arch Linux (Latest from AUR)
mise use -g opencode               # Any OS
nix run nixpkgs#opencode           # or github:anomalyco/opencode for latest dev branch
```

---

### 2. 訂閱 OpenCode Go（首月 $5，夠跑一整天）

**為什麼推薦用 OpenCode Go 方案？**
因為門檻低、直接打包 14 款強大的開源模型、給的額度用來打滿一整天的 Workshop 綽綽有餘。

**📊 方案細節：**

| 項目 | 內容說明 |
| --- | --- |
| **月費** | **首月 $5 USD**（之後 $10/月） |
| **5 小時上限** | 等同 $12 USD 的用量（對單一 Session 來說非常夠用） |
| **每週上限** | 等同 $30 USD 的用量 |
| **每月上限** | 等同 $60 USD 的用量 |
| **伺服器節點** | 美國 (US) / 歐洲 (EU) / 新加坡 (Singapore) |
| **隱私政策** | **Zero Data Retention（零資料留存）** |
| **取消與加值** | 可隨時取消；若額度打乾了也可以隨時手動加值 |

---

### 3. 運作方式與連線流程

OpenCode Go 的運作邏輯，就跟你在 OpenCode 裡串接任何其他 LLM 供應商一樣簡單：

1. **取得金鑰**：登入 OpenCode Zen 平台，訂閱 Go 方案，然後複製你的 API Key。
2. **終端機連線**：在你的 TUI (終端機介面) 中輸入 `/connect` 指令。
3. **貼上金鑰**：選擇 `OpenCode Go`，接著貼上剛剛複製的 API Key。
4. **確認模型**：在 TUI 中輸入 `/models`，就能看到所有透過 Go 方案解鎖的模型清單。

**Go 方案收錄的 14 款模型陣容：**

* GLM-5.1 / GLM-5.2
* Kimi K2.6 / Kimi K2.7 Code
* MiMo-V2.5 / MiMo-V2.5-Pro
* MiniMax M2.7 / MiniMax M3
* Qwen3.6 Plus / Qwen3.7 Plus / Qwen3.7 Max
* DeepSeek V4 Flash / DeepSeek V4 Pro


### 基本指令

| 指令 | 作用 | 為什麼需要 |
|---|---|---|
| `/init` | 初始化 session / 專案設定 | 進任何 repo 第一步——呼應 INSIGHT-8（AGENTS.md）|
| `/compact` | 壓縮對話 context | 對話太長時搶救——context 是有限資源 |
| `/session` | session 管理（list / resume / **fork**）| 呼應 INSIGHT-2 的 fork A/B |
| `/models` | 切換模型 | mini agent 的 model-swap 實驗，現在換你操作 |
| 其他 slash commands | 直接在 opencode 裡面看 | 自己去玩～|


### First run

給一個簡單任務，看 loop 跑——你剛學 agent = loop，現在親眼看見 loop。

### GLM 軌跡 hook

> 為什麼這個 workshop 選擇跑在 GLM 上？大約在 2026 年 1 月，我看到 Eno Reyes（Factory）在 X 上發文提到：「Opus plan + GLM-4.7 execute = same performance as Opus, fraction of tokens」——這正是我接觸開源 GLM 的起點。從 GLM-4.7、5.1 到現在的 5.2，我一路見證了它的發展軌跡。如今的 GLM-5.2 不僅已經達到 Opus 級別的水準，更是目前**最強的開源模型**。
>
> 至於為什麼堅持使用「開源最強」，而不是追求「絕對最強」？因為我曾經有過帳號被 ban 的慘痛教訓。關於這段完整的故事，我們留到主場的 Block C 再聊。

---

## Block A：MCP 到底是什麼（以 OpenCode 為例）— 40-60 min

### 🌉 從 Mini Agent 到 MCP 的橋樑

回想一下我們剛剛寫的 Mini Agent，裡面只有 `read / write / edit / bash` 這四個**Hardcode（寫死）**進去的基礎工具。

但在 OpenCode 裡，工具清單是**動態的**。**MCP 的強大之處在於：你只需要修改 Config 就能輕鬆擴充工具，完全不需要動到 Agent 的底層程式碼。**

---

### 🔌 MCP 的本質

**MCP（Model Context Protocol）說穿了，就是一個「通訊協定」**。
它的作用，是把 Local 端或 Remote 端的 RPC 服務，包裝成「Tool（工具）」加上「Tool Description（工具描述）」，然後掛載到 Agent 的可用清單底下。對 Agent 來說，呼叫這些外部擴充工具，就跟呼叫內建的 `bash` 一樣自然。

> 💡 **常常有人說：「MCP 就是 AI 模型的 USB 介面」**
> 這裡面沒有任何魔法。它純粹就是賦予 Agent 更多外掛能力。

---

### 🚀 現場實戰：直接 Configure 起來用！

講再多不如直接動手。現在我們直接在 OpenCode 的 Config 裡新增 MCP Server，大家可以親眼看看 Agent 是如何自動辨識、決定並呼叫這些新工具的。

**🛠️ 準備掛載的 MCP 工具陣容：**
*   **Context 7**：即時更新的函式庫資訊
*   **Exa Web Search**：網路搜尋與檢索能力
*   **Grep_app**：大規模程式碼搜尋
*   **MarkItDown**：將"任何"文件轉為 Markdown
*   **DeepWiki**：提供最新且可互動的文檔

**🔥 加碼展示 (Extra)：**
如果時間允許，我們再來掛載更硬核的工具：
*   **Ghidra**：讓 Agent 直接幫你做 Binary 逆向工程！
*   **Playwright**：賦予 Agent 操控瀏覽器、執行自動化測試的能力。

### INSIGHT-5：MCP 絕對不是越多越好 —— MCP 的兩種設計哲學

配置完 MCP 工具後，我要立刻戳破一個常見的迷思：「工具越多，Agent 就越強」。
錯了，**MCP 絕對不是越多越好**。這不是憑空猜測，而是來自多方實測與論文數據的血淋淋教訓：

| 觀測指標 | 驚人數據 / 發現 | 資料來源 |
| :--- | :--- | :--- |
| **Tool-selection 準確率** | **從 43%（4 個工具）暴跌至 2%（51 個工具）**——在同模型、同任務下，僅改變工具數量。 | GPT-4o 控制實驗 |
| **Speakeasy Benchmark** | 10 個工具時拿滿分 → 107 個工具時任務完全失敗。 | 基準測試 |
| **Anthropic 官方警示** | Claude 在塞入 30-50 個工具後能力明顯衰退 → 逼得他們必須開發 Tool Search 來補救。 | Anthropic |
| **血淋淋的真實案例** | 掛載 4 個 Server / 167 個工具 = 任務還沒開始，**光是讀工具描述就吃掉 60K Tokens**。 | 社群實測 |
| **平台硬性上限** | Cursor 限制 40 個工具、Copilot 限制 128 個、Zed 甚至為此設計了 Profiles 切換功能。 | 各大 IDE 限制 |
| **業界高姿態退場** | Perplexity CTO 甚至在 2026 年 3 月公開表示棄用 MCP。 | 業界動態 |

---

既然工具不能無腦塞，那我們該怎麼設計？**MCP 工具的設計其實分為兩種模式**：

| 設計模式 | 工具數量 | 代表範例 | 軟體工程類比 |
| :--- | :--- | :--- | :--- |
| **A. 少量深實作 (Fat Tool)** | 1~3 個 | Context7、 MarkItDown | 「公開少量 API，內部深度實作」——**把複雜度在工具內部消化掉**。 |
| **B. 多量薄實作 (Thin Tool)** | 數十個 | GitHub MCP、Postgres MCP | 「提供大量 API，內部極薄實作」——**把編排的複雜度推給上層**。 |

**這兩種模式對 Agent 的影響天差地別：**
*   **A 模式是「幫模型開外掛」**：LLM 不需要知道怎麼去抓文件、怎麼解析，工具直接把「最乾淨、最相關的 Context」餵給它。
*   **B 模式是「讓 LLM 做苦工」**：LLM 必須自己判斷要呼叫哪個工具、按什麼順序組合。這會把編排負擔全部推給 LLM，有時候會導致 **Context 嚴重污染**，大幅壓低 Tool-call 成功率。如果你用弱模型去跑 B 模式，結果會很慘。

---

### 緩解手法（預告主場 Block C：INSIGHT-4 應用）

如果你真的非得用 B 模式（大量薄工具）不可，該怎麼辦？
這裡有一個實戰手法：**先讓強模型（如 GPT-4o / Claude 3.5 Sonnet）跑一遍建立「示範軌跡 (Trajectory)」，然後再切換給弱模型接手。**

弱模型雖然規劃能力差，但非常擅長「模仿」強模型已經走過的 Tool-call 序列。這正是我們下午主場 Block C 要深入探討的核心思路：**「昂貴模型負責規劃 + 便宜模型負責實作」**。

---

## 主場 Block B：SKILL 到底是什麼 + 現場手搓一個（20-30 min）

回顧一下我們的 Mini Agent：我們已經有了 Repo 級別的 System Prompt（`AGENTS.md`），也有了動態擴充的 Tools（MCP）。
**而 SKILL，就是我們的第三層架構——「任務級別 (Task-level)」的模組化 Context 注入。**

---

### 🧠 SKILL 的本質

說穿了，SKILL 就是一個 Markdown 檔，裡面定義了某個特定任務或領域的指令與先備知識。
它的本質，就是一個**「模組化、可隨選呼叫的 Prompt」**——你可以把它想像成專案級別 `AGENTS.md` 的縮小版，但它聚焦於單一任務，並且可以透過 Slash Command (`/`) 在你需要的時候才動態觸發。

---

### 🛠️ Hands-on 實戰：每個人手搓一個專屬 SKILL

接下來，我們不講理論了，大家直接動手做。

1. **定義主題**：寫（或是 Clone）一個 `<anything>.md`——挑一個你自己關心或熟悉的主題（例如：你的獨門讀書法、某種程式語言的 Design Pattern、Paper 研究方法、甚至是任何你想自動化的瑣事）。
2. **掛載進系統**：在 OpenCode 中使用 `@` 直接提及這個檔案，或是將它配置到系統的 Skill 目錄下。
3. **實際觸發**：在對話框用 Slash Command (`/`) 呼叫並操作它。

> 💡 **Tip**：
> 如果你當下腦袋空白想不到要寫什麼，也可以去 GitHub 上找星星數很高的現成 Skill 直接 Clone 下來玩玩看（例如社群很有名的 `ponytail`）。

---

## 主場 Block C: 多模型編排 + live config show-and-tell（40-50 min）

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
| **開源 vs 閉源** | GLM、Kimi、Qwen、MiniMax 開源 |

→ 把 text（markdown / 純文字）當成模型之間的橋樑，就能讓「貴但短」的模型負責規劃、「便宜但長」的模型負責實作、「有眼睛」的模型負責 OCR。

### 三個 compose pattern（我在實習時為最大化每月 API 用量發展出來的用法）

| Pattern | 做法 | 剖析 |
|---|---|---|
| **貴規劃 + 便宜實作** | 同 context 內先用 Claude / GPT 規劃架構，再切便宜模型實作 | 用便宜模型實作強模型的 plan |
| **長 context 當壓縮機** | Gemini 讀 AI-native 文件庫 → 總結 → 餵 Claude 實作 | 用 Gemini 1M context 把長 input 壓成 Claude 能消化的短 input |
| **多模態當 OCR** | Gemini 讀圖 → 轉文字 → 餵純文字模型 | 多模態模型當「模態轉換器」，把視覺資訊轉成任何模型都能讀的 text |

### 切身故事：被 Google ban 帳號 ＋ omo ↔ Anthropic 大戰（短講，10 min）

- **我被 Google ban 帳號的血淚史**：2026 年上半年，我用了一個名為 `opencode-antigravity-auth` 的 plugin，這工具能把 Google Antigravity IDE 的模型額度反向代理到 OpenCode 裡面。用得很爽，但沒過多久，我的帳號就直接被 Gemini 官方封鎖了。
- **同樣的邏輯，引爆了 omo ↔ Anthropic 大戰**：omo（也就是我們這個 session 正在跑的 orchestrator）當初把每月 $200 的 Claude Max 訂閱 OAuth token 直接接進 OpenCode，用來驅動龐大的 multi-agent 架構。
- **成為大廠眼中釘**：omo 的多 Agent 編排簡直是個「Token Burner」，讓訂閱帳號的 token 消耗量呈倍數暴增，遠超一般人類的使用極限。這股異常流量立刻引起了 Anthropic 的警戒。
- **封鎖與律師函**：Anthropic 隨即展開反擊。他們先是在 2026 年 1 月 9 日從伺服器端全面阻斷了第三方的 OAuth 存取，接著在 3 月 19 日直接祭出律師函，強硬要求 OpenCode 移除所有與 Claude 相關的整合。這場風波之大，連開發者後來都公開承認：「*Anthropic blocked OpenCode because of us [omo].*」

---

## 主場 Block D：自建 context 資料庫庫 + AGENTS.md（30-40 min）

> **承接**：上午學了 system prompt（AGENTS.md）+ tools（MCP）+ 任務級注入（SKILL）。這段是 INSIGHT-1 的最極致應用——改善 input 改到「**整個 repo 都是 input**」。

### INSIGHT-7：與其讓 AI 盲猜，不如主動把資訊搬進它的 Context

在 INSIGHT-1 中我們談到「改善 Input」。而改善 Input 最極致的做法，並不是去寫花俏的 Prompt，而是**為 Agent 預先打造一個專屬的、具備版本控管的 Markdown 知識庫，讓它直接在裡面工作**。

以我自己為例，針對**每門修課**，我有一套固定的 Routine：

1. **抓取素材**：下載所有的 slide、PDF、作業與講義。
2. **AI-Native 轉換**：把這些檔案全部轉成 Markdown 格式（這是 INSIGHT-1 的直接應用）。
3. **建置 Git Repo**：為這門課建立專屬的 Note Repo（包含 `course-materials/`、`notes/`、`exam/` 等標準目錄）。
4. **Context 內發問**：直接在這個 Repo 裡喚醒 Agent，讓它**自動以整門課的知識為背景**來回答問題，徹底告別盲猜。
5. **模組化引用**：當要做期末專題或寫作業時，直接把這個 Repo 當作 Submodule 引入。作業一開工，Agent 就自動繼承了整門課的背景知識。

這套流程，說穿了就是**「徒手搓出一個超越 NotebookLM 或 RAG 的系統」**。它比 NotebookLM 更強大，因為它具備版本控管、可自由組合（透過 Submodule）、可攜帶（純 Markdown），而且完全掌握在你手中。

---

### Context 架構三件套（我的 `~/School` 實證）

這套「Context 架構」的核心概念是將**知識庫**與**工作專案**分離，並用 Agent 操作手冊來當作橋樑。以下是三個核心組件：

| 組件 | 角色定位 | 真實案例 |
|---|---|---|
| **Note Repo（語料庫）** | 該領域的完整 Markdown 知識庫 | `ntu-2025fall-advanced-compiler-note`（包含 20 份 Markdown + 9 份簡報 + 5 份 PDF） |
| **Work Repo（作業/專題）** | 實際的工作產出，透過 Submodule 引用語料庫 | 某堂課的 `hw1`，或是引用了 4 個作業 Repo 的 `cs-computer-graphics` |
| **AGENTS.md（操作手冊）** | 告訴 Agent 在這個 Repo 裡該怎麼工作 | 在我的 `~/School` 目錄下，就有超過 15 處配置了 AGENTS.md |

---

### 為什麼這套 Workflow 最值得你立刻學起來？

*   **零門檻**：每個學生都要修課，且這套流程**不需要任何進階環境或付費 API**，現在就能開始做。
*   **一石四鳥**：在建置的過程中，你同時學會了 **Git、Markdown、Context Engineering 以及撰寫 Agent 操作手冊**，還能立刻提升課業與專題效率。
*   **心智模型的躍遷**：把「AI 輔助學習」從「把講義丟給 ChatGPT 幫我摘要」的層次，徹底升級成「**親手建一個讓 Agent 住進去的知識庫**」。

**這套做法能打破哪些迷思？**

*   ❌ **「有事問 AI 就對了」** → ✅ 「問」之前，請先決定你要在什麼 Context 裡問。同一個問題、同一個模型，在專屬語料庫裡問，跟在空白對話框裡問，結果絕對是天差地別。
*   ❌ **「一定要會弄 RAG 或向量資料庫才能玩這套」** → ✅ 只要你會用 Git、寫 Markdown，再加上任何一個能讀檔的 Agent，就能做出比向量 RAG 更可控、更透明、可重組的版本。
*   ❌ **「NotebookLM 是一種神奇的新科技」** → ✅ 它的底層邏輯就只是「語料庫 + LLM」，而我們已經用手邊的開源工具，搓出了一個威力更強的超級強化版。

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
