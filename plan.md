# AI Workshop 大綱

> 受眾：實驗室大學/碩士生（光譜寬：中學生 ~ Claude Max token-maxxing 朋友）
> 形式：整天 workshop，9am ~ 下午，3-6 小時
> 講者：G36maid（NTNU CS/ME 大四）
> 設計立場：**演講者驅動**——「我想講我想講的」，不為受眾落差最佳化。北極星 = 帶聽眾從 web-chatbot 心智模型遷移到 agent 心智模型。

---

## 場次結構

| 場次 | 內容 | 備註 |
|---|---|---|
| **上半場（早上）** | pure opencode | 講者日常 driver 場景，即興 demo，不切換工具 |
| **下半場（下午）** | omo（條件性）| 若上午 opencode 講不完 → omo 順延。上半場優先級 > omo |

---

## 上半場（早上）：pure opencode

### 開頭 arc（約 90-130 分鐘）

> 開頭的任務：建立「為什麼聽我講」+ 拆穿 AI 魔法 + 讓每個人跑起來。祛魅講完自然滑進 pure opencode 主場——因為 INSIGHT-3（agent = loop）一旦建立，opencode 就只是「一個刻得好的 loop」，不是魔法。

#### Block 1：自我介紹（10-15 min）

| 元素 | 來源 | 作用 |
|---|---|---|
| LLM 土著（2022-11 GPT-3.5 同步起步）| `personal-info.md` §1 | 同世代、可信、不是後來跟風 |
| Zed Guild Contributor + OSS（markitdown MCP 29k 下載）| §4 | 我不只用它，我造工具給這個生態 |
| 系統工程 / 資安 / 開源 偏好（一兩句帶過）| §1, §2 | 人格定位 |

**Credibility framing**：同儕不是教授——深度是權威來源，不是頭銜。

**講古 hook（輕提）**：被 Google Antigravity ban 的故事（§5.1）——一句話帶過建立「這人玩真的、會燙到」的份量。完整版留到 INSIGHT-4 重講。**不反 Anthropic/Google 宣教**（§8 已警告風險）。

#### Block 2：關鍵說明（10-15 min）

三句話 framing：

1. **這個 workshop 不是什麼**：不是工具教學（那是搬運層在做），不是教你怎么按 Cursor
2. **這個 workshop 是什麼**：心智模型遷移——web-chatbot → agent（北極星）
3. **誠實定位**（INSIGHT-9）：我直接把英文圈的 insight 用中文講給你聽，省你爬源頭的時間

這裡也誠實說「我想講我想講的」——設下「演講者驅動場」的期待。

#### Block 3：知識環節 — 祛魅層 INSIGHT-1~3（40-60 min）

開頭的智識重心。三條 insight 是心智模型遷移的階梯：

| Insight | 核心 | 教材 |
|---|---|---|
| **INSIGHT-1** LLM = I/O 黑盒子 | 兩根槓桿：input + model。其他全是「改善 input」的實作 | live demo：同模型、不同 input → output 天差地別（§6.2 text-thread 經驗源頭）|
| **INSIGHT-2** 把 LLM 當系統 debug | re-roll / 改 input / fork A/B / 偷看 thinking = 工程 debug 招式 | 全班同題 re-roll → 親眼看見變異 |
| **INSIGHT-3** Agent = loop | 5 行 while loop 解釋全部 agent 魔法 | **現場 build 一個 mini agent**（見下）|

**INSIGHT-3 provenance**：Adam 在 ThePrimeagen Standup podcast **[04:32]** 定義「Agent = LLM + Tools + Loops」（見 `references.md` §7.4）。

##### Mini agent 現場實作（Block 3 重頭戲）

**做法**：講者在現場從零寫出一個 mini agent，不到 200 行。結構：

| 組件 | 內容 | 對應的 insight |
|---|---|---|
| **System prompt**（= AGENTS.md）| 寫一段告訴 LLM「你是 agent，你有這些工具」| 預告 INSIGHT-8（AGENTS.md = repo 級 system prompt 注入）|
| **Tools**：`read` / `write` / `edit` / `bash` | 每個工具的定義 + 呼叫格式 + 執行邏輯 | 預告 INSIGHT-5（這些就是「內建工具」，MCP 是其擴充來源）|
| **while loop** | LLM output → 若符合工具呼叫格式 → 執行 → 結果回灌 context → 重送 | INSIGHT-3 本體 |

**參考**：Theo（t3․gg，見 §5.12）做過類似示範，不到 200 行——講者據此規劃。

**為什麼比只展示 20 行抽象 loop 強**：
- **看得見 agent 被生出來**——祛魅最徹底的形式
- **一個 build 同時示範多條 insight**：INSIGHT-1（loop 裡的 LLM call 就是 I/O 黑盒子）+ INSIGHT-3（loop 結構）+ INSIGHT-8 預告（system prompt）+ INSIGHT-5 預告（工具）
- **無縫銜接 pure opencode 主場**：build 完後指著 opencode 說「它就是這個，只是工具更多、context 管理更精細、加上生產級 polish」——學生親眼看過原型，opencode 從此不是魔法

**前置 to-do**：講者需準備好 mini agent 的程式碼（可預寫，現場邊貼邊講；或從空白逐步 build）。語言選什麼待定（Python / TypeScript / Rust 皆可，看講者偏好與學生消化度）。**設計要求**：AGENTS.md 與 model 必須是易切換的 config（不能 hardcode），這樣下面的實驗段落才跑得起來。

##### Mini agent 實驗段落（互動）

Build 完不是結束——同一個 mini agent 立刻當實驗台，用控制變因示範多條 insight：

| 實驗 | 做法 | 示範的 insight | 看見什麼 |
|---|---|---|---|
| **有/無 AGENTS.md** | 同一任務，先沒 AGENTS.md 跑一次，加上 AGENTS.md 再跑一次 | **INSIGHT-8**（system prompt 注入）| agent 行為天差地別——「寫不寫 AGENTS.md，agent 表現差很多」當場被驗證 |
| **各家 model 對照** | 同一 agent + 同一 AGENTS.md，換 Go 的不同模型（GLM-5.2 / Kimi / MiniMax / DeepSeek 等）跑同一任務 | **INSIGHT-1**（model 槓桿）+ **INSIGHT-2**（系統性比較）| 同一個 loop、不同模型 → 品質/風格/能力落差一目了然 |
| **學生自己玩** | （在 Block 4 環境配置後）學生拿自己的 Go 訂閱，改 AGENTS.md、換 model，跑自己的任務 | 綜合 INSIGHT-1/2/4/8 | 主動實驗 → 親身驗證，不是聽講 |

**為什麼這組實驗強**：
- **有/無 AGENTS.md** 是最直接的「INSIGHT-8 不是形式主義」證明——學生親眼看到差別，不用講道理
- **各家 model 對照** 把 INSIGHT-1 的「換模型」槓桿變成可操作的肌肉記憶，同時預告 INSIGHT-4（model 是可組合組件，不是「選錯就卡死」）
- **學生自己玩** 把 Block 3 從 demo 變成 active learning——而且只需改 config，不用寫 code，門檻極低
- 整組實驗都是「**同 agent、變一個維度、比 output**」——這正是 INSIGHT-2「把 LLM 當系統 debug」的 controlled experiment 手法，學生邊玩邊內化

**流程銜接**：講者在 Block 3 demo 前兩個實驗（有/無 AGENTS.md + 各家 model）；Block 4 學生裝好環境後，用自己的 Go 訂閱 replay 這些實驗——是 Block 3 → Block 4 → opencode 主場的天然橋樑。

**INSIGHT-3 延伸（omo 預告）**：持續性機制兩派（Sisyphus todo-driven vs Ralph loop prompt-reinjection）——當下午場 omo 的餌。

#### Block 4：環境配置（30-40 min）

| 步驟 | 備註 |
|---|---|
| opencode 安裝 | 講者 Arch pacman；學生可能 Mac/Windows——**要備跨平台指令** |
| Go 訂閱 $5 + API key | 見 `notes.md` §1 |
| **Pure Go config 套用** | 見 `notes.md` §3（待產出的 to-do，cost safety boundary）|
| First run：給簡單任務，看 loop 跑 | 呼應 INSIGHT-3——學生剛學 loop，現在親眼看到 loop |
| 確認每個人能跑 | **friction 點**，可能吃時間 |

**講古 hook**：GLM 軌跡（4.7→5.1→5.2，§5.1 + Eno Reyes X 貼文 provenance）——為什麼這個 workshop 跑在 GLM 上 / 為什麼推薦 Go（開源模型陣容對齊 no-lock-in 哲學）。

##### 基本指令教學（Block 4 子段）

opencode 裝完配完，學生需要知道怎麼**操作**它——不然裝了不會用。關鍵指令（**完整清單與語法以 opencode docs 為準**）：

| 指令 | 作用 | 為什麼學生需要 |
|---|---|---|
| `/init` | 初始化 session / 專案設定 | 進任何 repo 第一步——呼應 INSIGHT-8（AGENTS.md）|
| `/compact` | 壓縮對話 context | 對話太長時搶救——INSIGHT-1 的 context 管理實作 |
| `/session` | session 管理（list / resume / fork）| 呼應 INSIGHT-2 的 fork A/B——session 就是可 fork 的實驗單位 |
| `/models` | 切換模型 | 直接對應 mini agent 的 model-swap 實驗——學生已看過效果，現在亲手操作 |
| 其他 slash commands | 待補 | **參考 opencode docs 補齊** |

**教學連結**：
- `/models` 是 mini agent model 對照實驗的「現在換你自己操作」環節——Block 3 demo 過 → Block 4 學生自己用 `/models` 換模型
- `/session` fork 對應 INSIGHT-2 的「fork chat 雙 thread A/B」——把講者的 debug 手法變成學生的操作肌肉記憶
- `/compact` 是 INSIGHT-1「context 是有限資源」的 live 體驗

**前置 to-do**：從 opencode docs（https://opencode.ai/docs/）撈完整 slash command 清單，挑 workshop 必要的（不要全部塞，只教會用到的）。

### 講古 hook 落點總表（穿插，非獨立塊）

| 故事 | 落點 | 作用 |
|---|---|---|
| 被 Google ban（§5.1）| Block 1 輕提 / **INSIGHT-4 重講** | 份量、性格 |
| Text-thread 演化（§6.1-6.2）| INSIGHT-1 | 我怎麼懂 context 的 |
| Prime podcast Adam [04:32] | INSIGHT-3 | agent=loop 的出處 |
| GLM 軌跡 + Eno Reyes 貼文 | Block 4 / INSIGHT-4 | 為什麼用 GLM |
| vibe coding / 養龍蝦（嗤之以鼻）| INSIGHT-1 | 我們不是這派人 |
| Zed agent 時間軸（§6.1）| INSIGHT-3 | 我看著它從無到有 |

### 開頭之後（pure opencode 主場）

> 祛魅 + 環境就緒後，上午主場深入「構造 input 層」。以下為已確認的 block，其餘待補。

#### 主場 Block A：MCP 是什麼、本質、直接配置起來用（in opencode）

| 部分 | 內容 | 對應 |
|---|---|---|
| **MCP 是什麼** | 一個 protocol：把 local/remote RPC 包成 tool + tool 描述，掛在 agent 的 tool 清單下。agent 就像呼叫 `read`/`write`/`edit`/`bash` 一樣呼叫它 | INSIGHT-3 的「Tools」擴充來源——mini agent 的內建工具是固定四個，MCP 是「幫 agent 加更多工具」的標準協議 |
| **本質** | 「模型的 USB」（§5.9，gemini-cli 社群比喻）——沒有魔法，就是給 agent 更多可呼叫的工具。接上就有，拔掉就沒有 | 連接 INSIGHT-3：MCP server = loop 裡 tool dispatch 的擴充來源 |
| **直接配置起來用** | 在 opencode config 裡加一個 MCP server，現場使用——看 agent 自動呼叫它 | INSIGHT-5 預告（A vs B 典範判斷）|

**關鍵教學連結**（mini agent → MCP 的無縫橋樑）：
- Block 3 的 mini agent 有 `read`/`write`/`edit`/`bash` 四個**硬編譯**工具
- opencode 的工具清單是**動態的**——MCP 讓你用 config 加工具，不用改 code
- **現場對照**：mini agent 的工具是寫死的 → opencode 用 MCP 配一個工具 → 學生看到「同一個 loop，工具可插拔」

**可用 MCP 範例**（待講者選）：
- 講者自己的 `zed-mcp-server-markitdown`（A 典範，29,963 下載，§5.9）——「看到缺口 → 自己補上 → 近 3 萬人採用」的激勵案例
- 或 context7（抓最新 doc 餵給模型，本 session 就在用）——A 典範，即時有用

**講古 hook**：講者從 gemini-cli 社群聽到「MCP = 模型的 USB」這個比喻前去了解（§5.9 接觸歷程）。

**INSIGHT-5 預告（震撼材料）**：配置完 MCP 後，點出「不是越多越好」——引用 `references.md` §4 的硬數據（tool-selection 43%→2% @ 4→51 工具；Anthropic 30-50 工具衰退門檻）。為 INSIGHT-5（A vs B 典範）鋪墊，後續深講。

#### 主場 Block B：SKILL 是什麼、本質、手搓一個（早上 finale，if time permits）

**承接主場三層**：mini agent 有 system prompt（AGENTS.md）+ 有 tools（MCP 擴充）。SKILL 是第三層——**任務級的模組化 context 注入**。

| 部分 | 內容 | 對應 |
|---|---|---|
| **SKILL 是什麼 / 本質** | 一個 markdown 檔，定義某任務/領域的指令與知識。本質 = **模組化的、可呼叫的 system prompt**——像 AGENTS.md（repo 級）但縮到任務級，用 slash command 按需觸發 | INSIGHT-1「改善 input」的模組化實作；INSIGHT-7 微觀版（單一任務的精煉 context）；跟 INSIGHT-8 同源（markdown 定義行為），但 task-scoped |
| **Hands-on** | 每人寫（or clone）一個 `<anything>.md` → 在 opencode `@` 這個 file → 配置到 skill 目錄 → 用 slash command 操作它 | 完整閉環練習 |

**為什麼這是好的 morning finale**：
- **每人帶走一個自己造的 artifact**——不是聽了一場 talk，是帶了一個 skill 回家
- **完整 INSIGHT-1 肌肉記憶**：寫 markdown → 配置 → 呼叫 → 看它工作——「改善 input」整條鏈親身走一遍
- **`<anything>` 開放性** → 學生挑自己關心的主題 → 投入度高（不論是讀書法 / 程式 pattern / 研究方法 / 任何東西）
- **clone 選項** → 寫不出的學生也能參與，門檻極低
- **預告 omo（下午）**：omo 的 explore / oracle / librarian / metis / momus 都是 skill 驅動的 subagent——學生早上寫過 skill，下午看 omo 就懂其結構

**講者參考**：`ctf-arsenal` 的 `.agents/skills/*/SKILL.md` 結構（§5.3，pwn/web/ics/crypto/forensics 五個 skill 模組化）是現成範本。

**前置 to-do**：講者準備一個極簡的 `<anything>.md` 範本（供 clone），以及 opencode skill 目錄配置的 live 步驟。

---

#### 主場其他 block — 待講者補充

預期方向（推論）：
- **INSIGHT-5 深講**：MCP 設計兩典範（A 少量深實作 vs B 多量薄實作）+ 緩解手法（強模型示範 → 弱模型模仿）
- **INSIGHT-7**：自建 context 語料庫（`~/School` 三件套，至今最可轉移 workflow）
- **INSIGHT-8 深講**：AGENTS.md 業界標準、教學 gotcha
- **鎮館之寶登場**：講者 live config（4 provider 混合 + fallback 鏈，§5.1）show 出來

---

## 下半場（下午）：subagent + omo（條件性）

> 若上午 opencode 講不完 → 下午順延。上午優先級 > 下午。

### 下半場 Block 1：subagent 概念 + 配置（核心）

**承接早上**：早上學了 agent = loop（INSIGHT-3）、工具可插拔（MCP）、任務級 context 注入（SKILL）。subagent 是這三者的組合升級——**loops within loops**。

| 部分 | 內容 | 對應 |
|---|---|---|
| **subagent 是什麼 / 本質** | 一個被 orchestrator 委派的**獨立 agent loop**，有自己獨立的 context 視窗。orchestrator 不必自己做所有事，而是 spawn 一個 subagent 在**它的** context 裡做，只收回結果 | INSIGHT-3 的延伸（loop 裡 spawn loop）；接 SKILL（subagent 是 skill 驅動的實體）|
| **為什麼節省 context** | orchestrator 的 context 是有限資源（INSIGHT-1）。不 delegate = orchestrator 自己讀 20 個檔 → context 灌爆 → 沒空推理。delegate 給 explore = explore 在**自己**的 context 讀完 → 只回傳「auth 在 src/auth/，token flow 是 X→Y→Z」→ orchestrator 的 context 保持乾淨 | INSIGHT-1 的系統級 context 管理 |
| **配置一個 explore 或 librarian agent** | live 示範：用 **opencode 內建的 agent creator** + 配 MCP 工具，現場生一個 subagent 出來用（不用手刻 config）| INSIGHT-8 應用 + 接上午 MCP 段——早上學的 MCP 現在拿來裝備 subagent |
| **展示 context 節省** | 同一任務，先不 delegate 跑一次（看 context 灌爆），再 delegate 給 explore 跑一次（看 context 保持乾淨）——**controlled experiment，INSIGHT-2 手法** | INSIGHT-2 的系統級版 |

**兩個候選 subagent（講者選一個 demo）**：

| Subagent | 做什麼 | 節省什麼 |
|---|---|---|
| **explore** | 「Contextual grep for codebases」——在 codebase 裡找東西、回答「X 在哪」「Y 怎麼運作」。讀多個檔，回傳路徑 + 描述 | orchestrator 不必自己讀遍所有檔 |
| **librarian** | 多 repo 分析、查外部文件、找 OSS 實作範例（GitHub CLI / Context7 / Web Search）| orchestrator 不必自己爬一堆外部資源 |

**為什麼這段是下午的 anchor**：
- **把「context 是有限資源」從概念變成可操作**——學生親眼看到 context 被省下來
- **預告 omo 的本質**：omo 的 explore / oracle / librarian / metis / momus 就是 subagent 編排的生產級版——學生下午配過一個 subagent，就看懂 omo 整個 orchestrator + subagent 架構
- **呼應 INSIGHT-4**：不同 subagent 可用不同模型（explore 用便宜快模型、oracle 用貴模型）——subagent 編排 = model composition 的系統級實作

### 下半場 Block 2：omo（若時間允許）

承接 subagent 概念，介紹 omo（oh-my-openagent）= opencode 之上的進階 harness：
- **Sisyphus todo-driven 持續性**（早上 INSIGHT-3 預告過的兩派之一）
- orchestrator + 平行 subagent + skill 注入 = 講者日常真實工作模式
- 可展示本 session 的 config（Sisyphus 跑在 GLM-5.2）當 live 範例

**安裝**：omo 有安裝腳本自動配置（含預設 orchestrator + subagent 結構），裝完學生手動改一下即可——門檻低，不是從零刻 config。

---

## 研究工具段（教授要求：不只開發還有研究）

> 上午 opencode 是開發導向。這段補研究導向的工具——教授明確要求 workshop 涵蓋「研究」不只「開發」。

### 研究工具 1：web chatbot deep-research（大範圍搜尋）

**工具**：Perplexity / Gemini deep research（以及其他 web chatbot 的 deep-research 模式）

**本質**：能在背景**批量搜尋數十到上百個網頁**——這是 local agent 做不到（或做得慢/差）的超能力。

**怎麼用（INSIGHT-6 的核心）**：

| ❌ 錯誤用法（= vibe coding）| ✅ 正確用法（= 研究後端）|
|---|---|
| 問 ChatGPT 問題 → 直接信答案 → 貼進作業 | 用 deep-research 跑一個研究題 → 拿 markdown 結果 → **貼回 local agent 當 context 繼續加工** |
| web chatbot = 答案來源 | web chatbot = **研究後端** |

**對學生的 reframe（關鍵教學價值）**：
- 學生現在多半已經在用 web chatbot——**不是叫他們丟掉**，是**升級用法**
- 「用 web chatbot」不等於「vibe coding」——關鍵是把它當**研究後端**而非**答案來源**
- 現有習慣變成資產，不必從零換軌

**live demo 候選**：現場用 Perplexity / Gemini deep research 跑一個研究題 → 存 markdown → 在 opencode 注入當 context → 讓 agent 基於這份研究繼續分析/寫程式。整條鏈一氣呵成。

**對應**：`insight.md` INSIGHT-6（環境分工）；`personal-info.md` §5.10（講者 routine）

### 研究工具 2：alphaXiv + autoresearch（arXiv 論文閱讀與複製）

**來源**：[@askalphaxiv 2026-06-18 推文](https://x.com/askalphaxiv/status/2067593673072877833)（478K views）

#### alphaXiv 本體——arXiv 的社群 + AI 層

**URL trick**：任何 arXiv 論文 URL，把 `arxiv` 改成 `alphaxiv`（五個字母），同一篇論文就多了：
- **Ask AI**：問問題，AI 以**論文本文為 context** 回答——比拿 PDF 問 ChatGPT 幻覺少很多（grounded）
- **AI Blog summary**：自動生成 1,500-2,500 字的易讀摘要（像 blog 文），附圖關鍵 claim 拉出來
- **行級社群討論**：可在特定行/式子/圖上留言討論

Stanford 學生專為 paper reading 設計，免費。

#### autoresearch（推文新功能）——論文複製 agent

**URL trick**：把 `arxiv` 改成 `autoarxiv`，一個 **agent 自動部署**：
1. **resolve setup issues on the codebase**——自動修論文 repo 的安裝/環境問題
2. **run a minimal reproduction**——跑一個最小重現
3. **estimate full replication cost**——估算完整複製要多少資源

**對 workshop 的價值**：
- **直接是 agent 應用**——autoresearch 本身就是 INSIGHT-3 的 agent（loop + tools + 部署 codebase），學生早上學 agent=loop，下午看到一個**用 agent 解決研究問題**的真實產品
- **研究生的痛點**：讀論文 → 想跑 codebase → 卡在 setup 地獄 → 放棄。autoresearch 自動解這件事
- **URL trick 極低門檻**：改五個字母，不用安裝、不用帳號——當場可以試
- **demo 候選**：現場挑一篇論文，`arxiv` → `autoarxiv`，看 agent 跑——直接展示「agent 幫你做研究」

**對應**：agent = loop（INSIGHT-3）；INSIGHT-6 環境分工（alphaXiv 是 web 端研究工具，跟 local opencode 互補）

### 研究工具 3~N：待講者補充

---

## 待辦

- [ ] 產出 pure Go config（見 `notes.md` §3）
- [ ] **準備 mini agent 程式碼**（Block 3 重頭戲，不到 200 行，語言待定；設計要求：AGENTS.md 與 model 必須 config-driven 易切換，實驗段落才有得玩）
- [ ] **從 opencode docs 撈 slash command 清單**，挑 workshop 必要的教（Block 4 子段）
- [ ] **準備 SKILL hands-on**：極簡 `<anything>.md` 範本（供 clone）+ opencode skill 目錄配置 live 步驟
- [ ] 補齊開頭之後的 pure opencode 主場結構
- [ ] **準備 subagent demo**：用 opencode 內建 agent creator + MCP 配一個 explore/librarian subagent + 一個能對比「delegate vs 不 delegate」context 用量的任務（下半場 Block 1 核心；agent creator 語法見 opencode docs）
- [ ] 跨平台 opencode 安裝指令（Block 4 需要）
