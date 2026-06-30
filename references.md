# 外部來源 References

> 本檔收錄籌備過程中查證用的所有外部來源，與 `personal-info.md`（事實）、`insight.md`（洞察）分開。
> 每條附：標題、URL、用途、抽取的關鍵數據。設計教材時可由此溯源任何聲稱。
> Primary source（講者本人 GitHub / 口述）不在此檔。

---

## 1. 模型與工具發布時間軸（用於 `personal-info.md` §6.1）

| 日期 | 事件 | 來源 |
|---|---|---|
| 2022-11-30 | ChatGPT（GPT-3.5）公開免費上線 | OpenAI 官方公告 |
| 2024-03-04 | Claude 3 Opus / Sonnet / Haiku | https://www.anthropic.com/news/claude-3-family |
| 2024-06-20 | **Claude 3.5 Sonnet**（coding 分水嶺）| https://www.anthropic.com/news/claude-3-5-sonnet |
| 2024-10-22 | Claude 3.5 Sonnet v2 + Haiku + Computer Use | https://www.anthropic.com/news/3-5-models-and-computer-use |
| 2025-02-24 | Claude 3.7 Sonnet（hybrid reasoning）+ Claude Code CLI | Anthropic Claude 3.7 公告 |
| 2025-02 上旬 | Karpathy 提出 "vibe coding" | Karpathy 推文（2025-02）|
| 2025-05-22 | Claude Sonnet 4 + Opus 4 | Anthropic 公告 |
| Gemini 2.5 Pro | experimental 2025-03-25 / stable GA 2025-06-17 | https://mungomash.com/ai/gemini/versions/ |
| Anthropic 全模型族譜（Opus/Sonnet/Haiku/Mythos/Fable 完整時間軸）| 綜合表 | https://hidekazu-konishi.com/entry/anthropic_claude_model_release_timeline.html |
| gemini-cli 開源（Apache 2.0）| 2025-06-25 | https://blog.google/innovation-and-ai/technology/developers-tools/introducing-gemini-cli-open-source-ai-agent/ ；https://techcrunch.com/2025/06/25/google-unveils-gemini-cli-an-open-source-ai-tool-for-terminals/ |

---

## 2. Zed 編輯器演化（用於 `personal-info.md` §6）

| 主題 | 來源 |
|---|---|
| Zed 0.92「Introducing the assistant panel」——text thread 起點（2023-06-28）| https://zed.dev/blog/assistant |
| 「Introducing Zed AI」（2024-08-20，綁 Claude 3.5、`/workflow`、Prompt Caching）| https://zed.dev/blog/zed-ai |
| Text Threads 官方文件（legacy 模式說明）| https://zed.dev/docs/ai/text-threads |
| Agent Panel 官方文件（2025-05 引入 agentic workflows）| https://zed.dev/docs/ai/agent-panel |
| v0.231.1（2026-04）移除 legacy text thread | https://newreleases.io/project/github/zed-industries/zed/release/v0.231.1 |
| 社群挽留 text thread 討論 | https://github.com/zed-industries/zed/discussions/30159 |
| Phoronix 報導 Zed AI 上線 | https://www.phoronix.com/news/Zed-Adding-AI-Features |
| Simon Willison 評論 Zed AI（含 Fast Edit Mode）| https://simonwillison.net/2024/Aug/20/introducing-zed-ai/ |
| 「Is Zed ready for AI power users in 2026?」（profiles 機制 = 對抗 MCP context 污染）| https://www.builder.io/blog/zed-ai-2026 |

---

## 3. MCP 生態與排行（用於 `personal-info.md` §5.9）

| 主題 | 來源 |
|---|---|
| Zed MCP 官方文件（MCP as extension / as custom server）| https://zed.dev/docs/ai/mcp |
| Zed MCP 設定實戰（`context_servers`、tool permission）| https://markaicode.com/mcp-zed-editor-setup/ |
| GitHub MCP Server Zed 安裝指南 | https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-zed.md |
| Zed 商店 — GitHub MCP（**91,294 下載**）| https://zed.dev/extensions/mcp-server-github |
| Zed 商店 — MarkItDown MCP（**講者作品，29,963 下載**，2025-09-25 上架）| https://zed.dev/extensions/mcp-server-markitdown |
| mcp.directory leaderboard（by stars）| https://mcp.directory/servers/leaderboard |
| MCP Toplist（by composite score，73,566 servers）| https://mcptoplist.com/ ；https://mcptoplist.com/mcp-server-list |
| MCP Market leaderboard | https://mcpmarket.com/leaderboards |
| MCPFind 2026 最受歡迎 MCP 分析（7,469 servers）| https://mcpfind.org/blog/most-popular-mcp-servers-2026-ranked |
| Smithery 用量數據 curated list | https://github.com/pedrojaques99/popular-mcp-servers |

> 排行快照（2026-07，跨榜單略有出入）：
> - context7（upstash）：~48k stars，各榜排第 4-7
> - github MCP：~27-30k stars，排第 11-18；Zed 商店單店 91k 下載
> - Microsoft MarkItDown：90k+ stars（mcp.directory by-stars #1，但反映上游專案歷史星數）

---

## 4. MCP Context Pollution 實證（支撐 `insight.md` INSIGHT-5）

> 講者直覺「MCP 裝太多效果打折扣」的硬數據備份。**這是 INSIGHT-5 從「個人觀點」升級為「可量化教材」的關鍵。**

### 4.1 量化數據（最常被引用）

| 指標 | 數據 | 來源 |
|---|---|---|
| 每工具 token 成本 | ~100–500 tokens（分析值）；實測 295–1,400 tokens | MindStudio／Anthropic 分析；mohammadkhan 生產實測 |
| 真實 bloat 案例 1 | 4 servers / 167 tools = **~60K tokens** 還沒工作就吃掉；$2 session → $47 | stackmcp.dev（引 Reddit Claude Code 案例）|
| 真實 bloat 案例 2 | 8 servers / 224 tools = 66K tokens（200K 視窗的 1/3）| mohammadkhan.dev |
| 真實 bloat 案例 3 | 3 servers（GitHub+Playwright+IDE）= 143K/200K（72%）| eclipsesource.com 影片實測 |
| GitHub MCP 單 server 工具數 | ~40 tools | VS Code issue #282699 |
| Anthropic 自家量測 | Claude 在 **30-50 工具後明顯衰退**；Tool Search 讓 Opus 4.0: 49%→74%（+25pp）、Opus 4.5: 79.5%→88.1% | hamedtaheri.com（引 Anthropic Advanced Tool Use）|
| 控制實驗（GPT-4o）| 行事曆任務 **43%（4 tools）→ 2%（51 tools）**；客服 **58%（9 tools）→ 26%（51 tools）** | alatirok.com（ReAct 實驗）|
| Speakeasy benchmark | 10 tools 滿分 → 20 tools 19/20 → **107 tools 完全失敗** | stackmcp.dev（引 Speakeasy）|
| LongFuncEval 學術 | 工具數增加 → **7%–85% 效能下降** | arXiv:2505.10570（Kate et al., 2025）|

### 4.2 平台承認問題的硬證據（硬上限）

| 平台 | 上限 / 機制 | 來源 |
|---|---|---|
| Cursor | **40 工具**上限 | stackmcp.dev |
| GitHub Copilot | **128 工具**，超量警告 | VS Code issue #282699 |
| Zed | **profiles** 機制：每個 context 只啟用特定 MCP server 的工具 | builder.io 2026 評測 |
| Anthropic | 官方建 Tool Search Tool（只載 3-5 相關工具）| Anthropic 工程文章 |
| Perplexity | CTO Denis Yarats（2026-03）公開宣布內部棄用 MCP，直指 schema overhead | albato.com（引 Ask 2026 conference）|

### 4.3 實用門檻（多方共識）

- **<10 工具**：安全區（直接 pass）
- **10-20**：警戒區（需量測 selection accuracy）
- **20-50**：拆 sub-agent
- **>50**：改用 retrieval-based tool selection
- MCP token overhead 應 **<15% context 視窗**；目標 3-4 個精選 server、零工具重疊

來源綜合：alatirok.com、stackmcp.dev、hamedtaheri.com

### 4.4 完整文章 / 論文清單

| 標題 | URL | 類型 |
|---|---|---|
| MCP and Context Overload | https://eclipsesource.com/blogs/2026/01/22/mcp-context-overload/ | 技術文章（含 20%+ context 實測影片）|
| Too Many MCP Servers? How to Build a Lean Stack | https://stackmcp.dev/blog/too-many-mcp-servers | 框架文（含審計 checklist）|
| I Run Six MCP Servers Daily. Here's What Breaks. | https://mohammadkhan.dev/blog/six-mcp-servers-what-breaks | 生產實戰紀錄 |
| How Too Many MCPs Break Your AI Agent in 2026 | https://albato.com/blog/publications/embedded-mcp-context-bloat-hallucinations | 綜合分析 |
| How Many Tools Can an AI Agent Have Before It Breaks? | https://alatirok.com/how-many-tools-can-an-ai-agent-have/ | 門檻指南（含控制實驗數據）|
| LLM Function Calling in Production: What the Benchmarks Actually Say | https://hamedtaheri.com/articles/llm-function-calling-in-production/ | benchmark 綜評（含 Anthropic 數據）|
| Writing effective tools for AI agents | https://www.anthropic.com/engineering/writing-tools-for-agents | **Anthropic 官方工程指引**（2025-09-11）|
| VS Code issue #282699 — MCP context pollution | https://github.com/microsoft/vscode/issues/282699 | 平台 issue（含官方回應）|
| copilot-cli issue #3024 — Too many MCP servers → continuous compaction | https://github.com/github/copilot-cli/issues/3024 | 平台 issue |
| LongFuncEval（Kate et al., 2025）| https://arxiv.org/html/2505.10570 | 學術論文 |
| Scaling Enterprise Agent Routing（2026）| https://arxiv.org/html/2606.17519 | 學術論文（routing 16-23pp 衰退）|
| Natural Language Tools（arXiv:2510.14453）| https://arxiv.org/html/2510.14453v1 | 學術論文（JSON 輸出比自然語言差 20-27pp）|

---

## 5. 學術課程背景（用於 `personal-info.md` §2，確認課程性質）

| 課程 | 來源 | 抽取重點 |
|---|---|---|
| **NASA**（Network Administration & System Administration, 台大資工）| https://iceyictw.github.io/devblog/post/nasa-1/ ；https://hackmd.io/@onion0905/SJVk85BVeg | Pass/Fail；每週 10-20 hr；Bash/Vim/VLAN/DNS(PowerDNS)/LDAP/firewall/Docker/VM；培訓系上 NASA 團隊 |
| **高等編譯器 ACD（CSIE5054）** | https://nol.ntu.edu.tw/nol/coursesearch/print_table.php?course_id=922+U1220 ；https://p.rst.im/q/github.com/pipi-bear/NTU-ACD-2025 ；https://blog.forvkusa.csie.org/posts/113-1-大三上修課心得 | 廖世偉 + jserv 合授；Dragon Book + Cornell CS6120；data flow / SSA / LLVM IR / pass / affine partitioning；研究所級 |
| **系統軟體 / jserv 體系** | http://wiki.csie.ncku.edu.tw/User/jserv ；https://github.com/jserv/talks | RTOS / kernel / 低階系統軟體實作 |
| 台大資工課程地圖 | https://coursemap.aca.ntu.edu.tw/course_map_all/class.php?code=9020 | 必選修清單、NASA / 編譯器 / 系程 在地圖中的位置 |
| 台大資工修課心得（含資安 = CTF 實務導向）| https://hackmd.io/@4RyHmsLUTs22ZI88xCW97w/nightshadesfreshmanfirst | 確認資安課高度 CTF 實務 |

---

## 6. AGENTS.md 與 agent instruction 標準（支撐 `insight.md` INSIGHT-8）

### 6.1 起源與治理
| 事件 | 來源 |
|---|---|
| AGENTS.md spec 官網 | https://agents.md/ |
| Spec repo `agentsmd/agents.md`（前身 `openai/agents.md`），created **2025-08-19**，22,630 stars / 1,668 forks | https://github.com/openai/agents.md/ |
| 起源：**OpenAI** 起家（spec repo 原在 `openai/agents.md`，後遷 `agentsmd/agents.md`），Sourcegraph Amp、Google (Jules)、Cursor、Factory 共同推動 → 2025-12 捐 Linux Foundation | https://github.com/openai/agents.md/ ；https://ccmd.dev/t/agents-md-design-decisions（註：此來源把發起歸給 Amp，但 repo namespace 顯示 OpenAI 為原始 host）|
| **2025-12 捐 Linux Foundation / Agentic AI Foundation (AAIF)** | https://ccmd.dev/t/agents-md-design-decisions |
| 設計七決策（plain md / 單根檔 / 無 @import / 字面名 AGENTS.md / nested 最近檔優先 / 32 KiB 預設 / 無 DRY）| https://ccmd.dev/t/agents-md-design-decisions |

### 6.2 採用（30+ agents 原生讀取）
OpenAI Codex、Cursor、GitHub Copilot、Google Jules、Gemini CLI、Aider、Windsurf、**Zed**、Sourcegraph Amp、RooCode、Factory、Phoenix、Devin⋯⋯（60,000+ repos 採用）。
- Claude Code 原生讀 `CLAUDE.md`，但**無 CLAUDE.md 時 fallback 讀 AGENTS.md**（或用 `@AGENTS.md` import）。
- 來源：https://docs.atlan.com/agents/concepts/agents-md ；https://www.morphllm.com/agents-md-guide ；https://codersera.com/blog/agents-md-vs-claude-md-vs-cursor-rules-comparison-2026/

### 6.3 它統一了什麼（fragmentation → standard）
| 舊格式 | 工具 | 現況 |
|---|---|---|
| `.cursorrules`（單檔）| Cursor | legacy，已轉 `.cursor/rules/*.mdc`（YAML frontmatter + glob scope）|
| `CLAUDE.md` | Anthropic Claude Code | 仍在用（3 層記憶：global / project / subdir + `@import`）|
| `GEMINI.md` | Gemini CLI | 仍在用 |
| `.github/copilot-instructions.md` | GitHub Copilot | 仍在用 |
| `.windsurfrules` | Windsurf | 仍在用 |
| **`AGENTS.md`** | 30+ agents（開放標準）| **vendor-neutral baseline** |

來源綜合：https://automatelab.tech/blog/ai-coding/claude-md-agents-md-cursorrules/ ；https://agent-ready.dev/agents-md-vs-claude-md-vs-cursorrules ；https://genalphai.com/agents-md-vs-claude-md/ ；https://codex.danielvaughan.com/2026/05/27/agent-instruction-files-agents-md-claude-md-cross-tool-portability-codex-cli/

### 6.4 重要 gotcha（教學用）
- **Nested discovery 行為不一**：Codex 會從 root 走到 cwd 串接所有 AGENTS.md；**Cursor / Claude Code 不做 nested 發現**——subdirectory-only 的 AGENTS.md 對它們隱形。這是團隊最常見 drift。來源：https://ccmd.dev/t/agents-md-design-decisions
- **Claude Code 不直接讀 AGENTS.md**，要靠 `@AGENTS.md` import 或 fallback。常見橋接：「CLAUDE.md 第一行寫 `@AGENTS.md`」。來源：https://www.morphllm.com/agents-md-guide ；https://github.com/anthropics/claude-code/issues/6235 ；https://github.com/anthropics/claude-code/issues/34235
- **Size 限制**：Codex 預設 32 KiB；Claude Code 建議 < ~800 行。來源：https://codex.danielvaughan.com/...
- **最佳實踐**：以 AGENTS.md 為 source of truth，CLAUDE.md / `.cursor/rules/` 當薄薄的 adapter 指回去（避免三份近乎相同的檔案 drift）。

---

## 7. OpenCode / Dax Raad（支撐 `personal-info.md` §5.1）

### 7.1 來源
| 主題 | 來源 |
|---|---|
| ThePrimeagen 的 Standup podcast「What even is an AI Agent?!」(Dax 來賓，講 agent + opencode) — **講者認識 opencode 的入口** | https://youtu.be/VsTbgYawoVc |
| OpenCode 官網（160K+ stars、900 contributors、7.5M 月活開發者）| https://opencode.ai/ |
| OpenCode Agents 官方文件（build/plan、permission 系統）| https://opencode.ai/docs/agents/ |
| Repo（179K stars，TypeScript；亦見 anomalyco/opencode）| https://github.com/sst/opencode |
| Engineered.at 專訪「Building OpenCode with Dax Raad」（設計哲學、開源定位、spec+verification、tech debt）| https://engineered.at/articles/building-opencode-with-dax-raad |
| Baseten 專訪 Dax（開源哲學、Zen、benchmark 誤導、OpenRouter 對比）| https://www.baseten.co/blog/building-ai-agents-open-code-and-open-source-a-conversation-with-dax/ |
| Taeho.io 該專訪摘要（SST → OpenNext → OpenCode 歷史；taste 在 AI 時代更重要）| https://taeho.io/en/reading/building-opencode-with-dax-raad_22008 |
| DeepWiki：opencode 架構設計（permission / agent / provider / plugin / escape hatches）| https://deepwiki.com/sst/opencode |
| Dax 的 X | https://x.com/thedxr |

### 7.2 Dax Raad 其人
- Creator of **OpenCode / SST / Zen**；**Terminal** 共同創辦人。
- SST 出身 → OpenNext（Next.js 部署到 AWS，填補 Vercel 沒覆蓋的缺口）→ 受 Anthropic Claude Code 啟發，做「open source Claude Code」。
- 定位語：**「我們是這個領域的開源選項」**；對 AI hype 抱持健康懷疑；與大公司在 X 公開爭論。
- 團隊 20+ 人，build in public。

### 7.3 設計哲學（deepwiki + 官方文件查證）
- **Permission model**：`allow` / `ask` / `deny` 三態；bash 支援 glob 細粒度（`git *` allow、`rm *` deny）；`external_directory` 管專案外存取。
- **Plan vs Build**：build = full access；plan = deny edit 全 codebase，**唯獨允許 edit `.opencode/plans/*.md`**（能寫計畫卻碰不到程式碼的精妙設計）。
- **Agent 可用 markdown 定義**：`.opencode/agents/*.md`（frontmatter + body 當 system prompt）— 與 AGENTS.md（§6）/ SKILL.md 同源的「markdown-as-config」哲學。Config deep-merge，project 蓋過 global。
- **Agent 種類**：primary（build/plan）、subagent（general/explore/scout，由 primary 用 `@` 召喚）、hidden system agents（compaction/title/summary）。
- **Provider 抽象**：`provider/model-id` 格式；plugin 從 npm / local 載入；可 hook 生命週期改 config 或 tool 執行。
- **Escape hatches**：`OPENCODE_DISABLE_PROJECT_CONFIG`、`OPENCODE_PURE`——永遠留逃生門，壞 config 也能脫身。

### 7.4 該 Podcast 的關鍵內容（timestamped，來自講者提供之 Gemini 摘要）
> 講者以此影片作為認識 agent + opencode 的入口。以下是從中抽取、與本筆記相關的重點。

| Timestamp | 內容 | 對應筆記 |
|---|---|---|
| 04:32 | **Adam 定義 Agent = LLM + Tools + Loops** | **`insight.md` INSIGHT-3 的直接出處**（講者從此吸收此心智模型）|
| 03:30 | OpenCode 專為 terminal / Neovim 用戶，非 IDE（vs Cursor）| 對齊講者 Arch + terminal 身份 |
| 07:28 | 主張本機執行（本機有最完整 dev env）；計畫手機 app 遠端監控 agent | opencode 本機優先哲學 |
| 09:35 | 多數模型 tool-calling 不成熟；Claude Sonnet 在程式碼理解 + tool call 表現最佳 | 印證 INSIGHT-5「多數模型不擅長 tool-call」；§5.8 多模型觀察 |
| 14:08 | **LSP 整合**：AI 編輯檔案後，立即把 LSP diagnostics 餵回 AI，讓它即時修正（減少幻覺如呼叫不存在的函式）| **INSIGHT-2/3 的具體實作**：verification in the loop（很值得當教材）|
| 20:03 | 業界 benchmark（ARC AGI / SWE）不實用（SWE 幾乎只 Python）；將推「Vibe Benchmarking」基於真實專案環境 | **直接印證 §5.8**「用真實工作測模型，不跑 benchmark」|
| 23:41 | Agent 運作：給 LLM 工具 + 任務，LLM 自行呼叫工具、迴圈直到完成 | INSIGHT-3 運作細節 |
| 26:10 | Bash 權限風險；現行 = 權限審批；未來考慮 Docker sandbox | 對應 opencode permission 系統（§5.1）|
| 28:19 | Context window 管理：近上限時暫停讓 LLM summarize 壓縮；**強烈建議每任務新開 session** | 印證講者對 context 管理的關注（Zed auto-compact PR）|
| 31:13 | **不提倡多 sub-agent 背景非同步**（會失去對 code 變更掌握）；傾向 human-in-the-loop | **張力點**：opencode 官方哲學保守，但 omo/Sisyphus（本籌備 session）疊加了激進平行 delegation——講者混用兩種哲學 |

---

## 8. ACP（Agent Client Protocol）與 agent 協定生態（支線調查，2026-07-01）

### 8.1 ACP 是什麼 / 誰生的
- **Agent Client Protocol (ACP)** = 標準化「程式碼編輯器 ↔ coding agent」溝通的開放協定（JSON-RPC 2.0）。
- **由 Zed Industries 創造**，2025-08-27 隨「Bring Your Own Agent」feature 發布，**Google Gemini CLI 為首個參考實作**。
- Repo `agentclientprotocol/agent-client-protocol`（亦見 `zed-industries/agent-client-protocol`），created 2025-06-23，Rust，3,525 stars，Apache 2.0，最新 v1.1.0（2026-06-24）。

### 8.2 誕生脈絡（與 Zed 的關係）
- **起點**：Google Gemini CLI 團隊想在 Zed 內做比「terminal 跑 CLI」更深度的整合。
- **問題**：Zed 原本在 embedded terminal 跑 Gemini CLI，只能靠 ANSI escape codes 溝通，不夠結構化。
- **解法**：Zed 定義一組極簡 JSON-RPC endpoints 來 relay 使用者請求與 agent 回應 → 這就是 ACP。
- **Commitment signal**：Zed 把自家 built-in AI assistant **重構成內部也走 ACP**——確保新功能對外部 agent 一視同仁。
- Nathan Sobo（Zed 共同創辦人）：目標是「**切換 agent 不必切換 editor**」。

### 8.3 里程碑
| 日期 | 事件 |
|---|---|
| 2025-06-23 | ACP repo 建立 |
| 2025-08-27 | 「Bring Your Own Agent」發布，Gemini CLI 為首個整合 |
| 2025-09-03 | ACP 正式 available in Zed |
| 2025-10-02 | 「從 Google 協作長成更大的東西」宣告 |
| 2025-10-06 | **JetBrains 與 Zed 合作**，把 ACP 帶進 JetBrains IDEs |
| 2026-06-24 | v1.1.0 釋出 |

### 8.4 ACP vs MCP（最關鍵的澄清：互補，不競爭）
兩者常被混淆，但**坐落在 agent 的不同側**：

| 面向 | ACP | MCP |
|---|---|---|
| 創造者 | Zed Industries（2025-08）| Anthropic（2024-11）|
| 解決 | **editor ↔ agent**（agent 住在哪 / editor 怎麼驅動 agent）| **agent ↔ tools/data**（agent 能摸到什麼）|
| 傳輸 | JSON-RPC over stdio / HTTP | JSON-RPC over stdio / SSE |
| 主關係 | editor 把 agent 當 subprocess 啟動 | agent 呼叫 tool/resource server |
| 串流 | 原生 token 串流到 editor UI | 請求-回應（無原生串流）|
| session 狀態 | 內建 session 管理、對話歷史 | 每請求無狀態 |
| 雙向 | 是（agent 可向 editor 要權限 / 檔案）| 僅 agent 主動呼叫 |

- **一個 agent 通常同時講兩者**：對 editor 是 ACP server、對 tools 是 MCP client。ACP session 啟動時，editor 把可用 MCP server endpoints 交給 agent。
- ACP 刻意**重用 MCP 的 JSON 表示**→ 兩者設計上可互通。
- 一句話：「**MCP 給 agent 工具，ACP 給 agent editor。**」

### 8.5 協定生態全景（三條 N×M → N+M 的開放化）
| 協定 | 邊界 | 創造者 | 角色 |
|---|---|---|---|
| **LSP** | editor ↔ language server | Microsoft | ACP 的建築祖先 |
| **ACP** | editor ↔ agent | Zed | 「LSP for agents」|
| **MCP** | agent ↔ tools/data | Anthropic | agent 的工具層 |
| **A2A** | agent ↔ agent（跨組織）| Google | agent 間編排 |

> 三條都是「把 N×M 客製整合崩塌成 N+M」的同一個開放化模式，作用在不同邊界。這跟 AGENTS.md（`insight.md` INSIGHT-8）的開放標準化是同一股力量——**agent 生態正在每個邊界都走向 open protocol**。

### 8.6 生態（2026 中）
- **Clients（editors）**：Zed（原生）、JetBrains（原生，collab）、Neovim（Oli Morris 的 Code Companion plugin）、Emacs（社群）、Obsidian plugin。
- **⚠️ VS Code / Microsoft 尚未原生支援 ACP**——只靠社群 plugin，不如 JetBrains/Zed 原生精緻。生態缺口。
- **Agents（50-60+）**：Claude Code（透過 Zed 的 bridge adapter，**Anthropic 未原生採用 ACP**）、Gemini CLI、Codex、GitHub Copilot、Cursor 的 agent、Cline、OpenHands、Goose、Docker cagent、Factory Droid、Kiro CLI，以及 **GLM 驅動的 agent（Zhipu AI，glm-5.1 等）**——呼應本 session 跑在 GLM 上。

### 8.7 易混淆警告
- **「ACP」縮寫撞名**：IBM 早期有一個 REST-based 的 agent-to-agent 協定也叫 ACP，已於 2025-08 併入 Google A2A 並 archived。**Zed 的 ACP 與之無關、且活躍發展中**。討論時須消歧。

### 8.8 來源
| 主題 | URL |
|---|---|
| Zed「Bring Your Own Agent to Zed」blog（誕生公告）| https://zed.dev/blog/bring-your-own-agent-to-zed |
| Zed ACP 官網（生態、里程碑）| https://zed.dev/acp |
| ACP spec 官網 | https://agentclientprotocol.com/get-started/introduction |
| ACP repo | https://github.com/agentclientprotocol/agent-client-protocol |
| PromptLayer「ACP: The LSP for AI Coding Agents」| https://blog.promptlayer.com/agent-client-protocol-the-lsp-for-ai-coding-agents/ |
| Morph「ACP Explained: ACP vs MCP」| https://www.morphllm.com/agent-client-protocol |
| MCP.Directory「ACP vs MCP (2026)」| https://mcp.directory/blog/agent-client-protocol-vs-mcp-2026 |
| danilchenko.dev ACP 教學 | https://www.danilchenko.dev/posts/agent-client-protocol/ |
| Ry Walker Research（含 IBM ACP 消歧、生態 60 agents）| https://rywalker.com/research/zed-agent-client-protocol |

---

## 9. omo（oh-my-openagent）/ Sisyphus / Ralph Loop（agentic 持續性機制）

### 9.1 omo 其物
- **omo（oh-my-openagent）** = 建立在 opencode 之上的進階 agent harness。Maintainer: Yeongyu Kim（code-yeongyu）。
- Repo `code-yeongyu/oh-my-openagent`，50K stars，TypeScript。
- **改名**：原 `oh-my-opencode` → `oh-my-openagent`（過渡期 dual-publish；config 同時認兩種 basename）。主因：與 sst/opencode（Dax 的開源 coding agent）消歧——omo 是 opencode 之上的 harness，非同一層。
- **Sisyphus Labs**：正在打造 "fully productized version of Sisyphus"（sisyphuslabs.ai，waitlist）。
- **Codex Light Edition**：omo 給 OpenAI Codex CLI 用的可攜組件（`lazycodex` / `npx lazycodex-ai install`）。

### 9.2 omo 的 agent 陣容
Sisyphus（主 orchestrator）、Hephaestus（Codex-on-steroids 深度 worker）、Prometheus（策略 planner，訪談式）、Atlas（todo 編排）、Oracle（架構/debug 諮詢）、Librarian（文件/碼搜）、Explore（快搜）、Multimodal-Looker（圖/PDF）、Metis（pre-plan 諮詢）、Momus（plan 評論）、Sisyphus-Junior（分類任務執行）。
- 模型：Sisyphus 用 `claude-opus-4-7` / `kimi-k2.6` / **`glm-5.1`**（呼應本 session 跑 GLM）。

### 9.3 持續性機制（講者最愛的設計點）
| 機制 | 持續性來源 | 記憶體 | 實作 |
|---|---|---|---|
| **Sisyphus Todo Continuation / Todo Enforcer** | agent 自建 todo list | 同 session 對話 | UserPromptSubmit / Stop hook；未完 todo → 注入繼續 |
| **Ralph Loop** | 外部固定 prompt | 檔案系統 + git history（每輪 fresh context）| Stop hook 攔截 exit → 重注入 prompt |

### 9.4 Ralph Loop 的生態（多家實作）
- **Geoffrey Huntley**：「Ralph is a Bash loop」——命名自 Simpson 的 Ralph Wiggum。
- **Anthropic 官方 plugin**（`anthropics/claude-plugins-official/plugins/ralph-loop`，~2025-11）：Stop hook 攔截 Claude exit、重注入 prompt；`--completion-promise` + `--max-iterations`。
- **gemini-cli-extensions/ralph**：AfterAgent hook、**每輪清空對話 context**（強制靠檔案）。
- **PageAI-Pro/ralph-loop（ralph.sh）**：task-list 驅動、Docker sandbox、可換 backend；PRD → task lookup → step 生成 → 迭代。
- **Ralphify**：RALPH.md config + `{{ commands.* }}` placeholder 每輪重讀（可邊跑邊改 prompt）、自我修復迴圈。
- **omo `/ralph-loop`**：Ultimate edition 內建。

### 9.5 設計原則（多方共識）
- **Filesystem 當記憶體**：agent 不把整個專案塞進 context，靠檔案 + git 跨迭代保持連貫。
- **明確停止條件**：completion promise（如 `<promise>COMPLETE</promise>`）+ max iterations 安全網（防無窮迴圈燒錢）。
- **可中斷**：Ctrl+C 通常優雅收尾；steering 檔（如 `.agent/STEERING.md`）可中途插隊關鍵工作。

### 9.6 來源
| 主題 | URL |
|---|---|
| omo repo | https://github.com/code-yeongyu/oh-my-openagent |
| omo docs（agent 結構、指令）| https://ohmyopenagent.com/docs |
| Sisyphus agent 詳解（舊版 mintlify）| https://code-yeongyu-oh-my-opencode.mintlify.app/api/agents/sisyphus |
| Sisyphus Labs（productized 版 waitlist）| https://sisyphuslabs.ai |
| Anthropic ralph-loop plugin | https://github.com/anthropics/claude-plugins-official/blob/main/plugins/ralph-loop/README.md |
| gemini-cli-extensions/ralph | https://github.com/gemini-cli-extensions/ralph |
| PageAI ralph-loop / ralphloop.sh | https://github.com/pageai-pro/ralph-loop ；https://ralphloop.sh/blog/what-is-the-ralph-technique/ |
| Ralphify | https://ralphify.co/docs/how-it-works/ |
| omo Issue #3272（rename 破壞 Todo Continuation 的實證）| https://github.com/code-yeongyu/oh-my-openagent/issues/3272 |

---

## 10. omo 引發的 OpenCode ↔ Anthropic/Google 衝突（2026 上半年大事）

> 講者陳述：「omo 導致 opencode 跟 google 跟 anthropic 鬧翻」。查證：**Anthropic 那邊極慘烈且文件完整；Google 那邊較隱晦**，但 omo 對 Gemini 也用了類似的 OAuth 套路。

### 10.1 起因：subscription OAuth 套用
- **OpenCode** 的 `opencode-anthropic-auth` plugin 讓使用者用 **Claude Pro/Max 訂閱的 OAuth token**（非 API key）認證——等於把 $200/月 Max 訂閱路由到 OpenCode，而非官方 Claude Code CLI。同等工作量透過 API 要 $1,000+/月。
- 早期 OpenCode 甚至**偽造 `claude-code-20250219` beta HTTP header**，讓 Anthropic 伺服器誤以為請求來自官方 Claude Code。

### 10.2 omo 為何是導火線
- **omo 的多 agent 編排 = token burner**（講者原話）。使用者把 $200 Max 訂閱接上 OpenCode+omo 後，multi-agent 把 token 消耗放大數倍——遠超 Claude Code 正常使用量。這異常流量引起 Anthropic 注意。
- Dax Raad 公開宣稱（X: `thdxr/status/2010149530486911014`）：**「Anthropic blocked OpenCode because of us [omo].」**
- omo README 把這段當勳章：「That's why Hephaestus is called 'The Legitimate Craftsman.' The irony is intentional.」——Hephaestus 是被封殺後才打造的 GPT-native agent，故名「正當工匠，生於必要而非特權」。

### 10.3 完整時間軸
| 日期 | 事件 |
|---|---|
| 2025-10-08 | Anthropic Consumer ToS 已含限制（§2 禁分享憑證；§3.7 禁非人類存取）|
| 2026-01-05 | **GitHub Issue #6930**：使用者通報因 OAuth + OpenCode 被 ban；共同點 = oh-my-opencode |
| 2026-01-09 ~02:20 UTC | **Anthropic 部署伺服器端封鎖**：第三方工具無法再用 Claude Pro/Max OAuth。影響 OpenCode、Cline、RooCode。**API key 存取未被封**|
| 2026-01-09 | omo Issue #626：Claude Max 憑證失效；Anthropic 工程師 Thariq 公開聲明（X: `trq212/...`）|
| 數週後 | **OpenAI 正式與 OpenCode 結盟**，把 ChatGPT Plus/Pro 訂閱支援延伸給 OpenCode、OpenHands、RooCode |
| 2026-02-19 | Anthropic 更新 ToS，明文禁止 Free/Pro/Max OAuth 用於第三方；同日 Dax commit `973715f` 移除所有 Claude OAuth 程式碼（偽造 header、auth plugin、Anthropic prompt）|
| 2026-03-19 | **Anthropic 發律師函**。OpenCode PR #18186「Remove anthropic references per legal requests」合併——所有 Claude 相關功能移除。HN 315 分 265 留言。v1.3.0 完全移除 Claude Max plugin |
| 2026-04-04 | 執法期限，擴及所有第三方 harness（OpenClaw、NanoClaw），使用者轉 pay-as-you-go |

### 10.4 結局：開放聯盟 vs 封閉 Anthropic
- **開放派（Anthropic 封鎖後紛紛填補缺口）**：
  - **GitHub Copilot**：**2026-01-16 官方 changelog** 宣布正式 partnership——所有 Copilot Pro/Pro+/Business/Enterprise 訂閱都能在 OpenCode 用（`/connect` → GitHub device login）。**就在 Anthropic 1/9 封鎖後一週**。https://github.blog/changelog/2026-01-16-github-copilot-now-supports-opencode/
  - **OpenAI**：正式結盟 OpenCode，把 ChatGPT Plus/Pro 訂閱支援延伸給 OpenCode（codex plugin，hardcode `chatgpt.com/backend-api/codex`）、OpenHands、RooCode。時程約 Feb-March 2026。
  - **Google Gemini**：開放 API 路線。
  - **Red Hat**：同月官方文件化 OpenCode for OpenShift Dev Spaces。
- **封閉派**：Anthropic（發律師、封 OAuth）。
- Dax 平衡發言：「你有權以任何方式存取服務，但他們也有權封鎖任何人。」但「一家發律師、一家發合作邀請，開發者看得出哪扇門開著」。
- OpenCode 重新定位：從「Claude Pro 加速器」轉為「model-agnostic harness」，首頁改主打 provider neutrality。
- **效果反諷**：Anthropic 的封鎖不但沒壓垮 OpenCode，反而**加速採用**——OpenAI/GitHub/Google/Red Hat 主動歡迎，開發者把條款變更解讀為「專有工具帶平台風險」的訊號（howtoprofitai 評論）。

### 10.5 Google 那邊（文件完整，且講者是當事人之一）
**不是隱晦——是有完整公開紀錄的平行事件，講者親身經歷。** 之前筆記標「較隱晦」是搜尋不足，已更正。

**兩個反代工具**：
- `jenslys/opencode-gemini-auth`（1.7K stars）：鏡射 Gemini CLI OAuth flow 到 opencode。README 已警告「Google stated that using Gemini CLI OAuth with third-party software is a policy-violating use case」。
- `NoeFabris/opencode-antigravity-auth`（**11K stars**）：**反向代理 Google Antigravity IDE 的模型到 opencode**——攔截 `generativelanguage.googleapis.com` 請求、轉成 Antigravity API 格式。可同時吃 Antigravity + Gemini CLI 雙 quota，甚至透過 Google OAuth 跑 Claude Opus 4.6 / Sonnet 4.6 + Gemini 3.1 Pro/Flash。**講者用的就是這類，並為此被 ban**。

**Antigravity 是什麼**：Google 的 agentic IDE（對標 Cursor / Claude Code），付費層（Pro/Ultra）用 OAuth 認證。

**Ban 波時間軸**：
| 日期 | 事件 |
|---|---|
| ~2026-02-09 | Google 開始封鎖用第三方 OAuth 的 Antigravity 帳號 |
| 2026-02-14 | 首批論壇通報「Antigravity account disabled — ToS violation」|
| 2026-02-17 | Google 確認「zero tolerance policy」、不恢復 |
| 2026-02-20 | 大量付費 Pro/Ultra 訂閱者被即時 ban；論壇「Mass 403 ToS Bans」熱議 |
| 2026-02-23 | OpenClaw 作者 Peter Steinberger 稱 Google 執法「pretty draconian」，宣布從 OpenClaw 移除 Antigravity 支援 |
| 2026-03 上旬 | Google 因強烈反彈宣布「system-wide automated unban」（但多人反映並非自動）|

**法律依據**：Google Antigravity Additional ToS §6 —「You must not abuse, harm, interfere with, or disrupt the Service. This includes... using the Service in connection with products not provided by us.」其中「products not provided by us」= 第三方工具。

**開發者憤怒點**：
- 無預警終身封、無警示、無臨時停權
- 付費訂閱者被斷服務卻繼續扣費
- 申訴管道是黑洞（email 數週無回）
- 連正當 Gemini CLI / Code Assist 用戶也被誤封（共享後端 abuse-prevention 層）

**Google 官方聲明**（gemini-cli Discussion #20632）：「Using third-party software, tools, or services to harvest or piggyback on Gemini CLI's OAuth authentication to access our backend services is a direct violation of Gemini CLI's applicable terms and policies.」並承認因後端共享而誤封正當使用者。

**跨 provider 通則**（openclaw.rocks）：訂閱 OAuth 是「subsidized access running on borrowed time」。Anthropic 2026-01 封、Google 2026-02 封，「others will follow」。

**來源（Google 那邊）**：
| 主題 | URL |
|---|---|
| jenslys/opencode-gemini-auth | https://github.com/jenslys/opencode-gemini-auth |
| NoeFabris/opencode-antigravity-auth（反代工具）| https://github.com/NoeFabris/opencode-antigravity-auth |
| Google 官方 Discussion #20632（Antigravity bans 說明）| https://github.com/google-gemini/gemini-cli/discussions/20632 |
| 論壇「Mass 403 ToS Bans on Gemini API/Antigravity」| https://discuss.ai.google.dev/t/urgent-mass-403-tos-bans-on-gemini-api-antigravity-for-open-source-cli-users-paid-tier/124508 |
| 論壇「Paid Pro Subscriber Banned Instantly」| https://discuss.ai.google.dev/t/paid-pro-subscriber-banned-instantly-for-testing-opencode-oauth/124403 |
| OpenClaw blog「Google Suspended AI Users Over Third-Party Tools」| https://openclaw.rocks/blog/google-antigravity-ban |
| Toolswift「Why Google Is Blocking Antigravity OAuth」| https://toolswift.com/why-google-is-blocking-antigravity-oauth-in-third-party-tools-like-openclaw/ |

### 10.6 對 workshop 的意義（連結 `insight.md` INSIGHT-4）
這整件事是 **INSIGHT-4（no vendor lock-in / 多模型組合）最硬的實證**：
- 「no vendor lock-in」不是品味問題，是**戰場**——model provider 想鎖住你，開源工具為中立性而戰，使用者夾在中間。
- omo 被 Anthropic 封殺的瞬間就**切到 Hephaestus（GPT-native）+ GLM + Kimi**——被鎖死的使用者會斷炊，omo 使用者只是換條線。**這就是 INSIGHT-4 的價值兌現**。
- 對學生是**警告**：用 OAuth 訂閱接第三方工具 = 帳號 ban 風險（終身封、申訴機制爛）。要用就用 API key。

### 10.7 來源
| 主題 | URL |
|---|---|
| OpenCode Issue #6930（首次 ban 通報）| https://github.com/anomalyco/opencode/issues/6930 |
| omo Issue #626（Claude Max 憑證失效）| https://github.com/code-yeongyu/oh-my-openagent/issues/626 |
| omo Issue #158（Claude Max ban 替代模型）| https://github.com/code-yeongyu/oh-my-opencode/issues/158 |
| The New Stack「157,000 developers hedging against Anthropic」| https://thenewstack.io/anthropic-claudecode-opencode-split/ |
| Jeongil.dev（oh-my-opencode / oh-my-claudecode / Agent Teams 生態比較）| https://jeongil.dev/en/blog/trends/claude-code-agent-teams/ |
| lilting.ch（Anthropic legal action + Astral 收購同日）| https://lilting.ch/en/articles/opencode-anthropic-legal-astral-openai-codex |
| ZBuild（OpenCode blocked by Anthropic 全貌）| https://www.zbuild.io/resources/news/opencode-blocked-anthropic-2026 |
| shareuhack（OAuth 套路 + 偽造 header 技術細節）| https://www.shareuhack.com/en/posts/opencode-anthropic-legal-controversy-2026 |
| aiproductivity.ai（Anthropic sends lawyers）| https://aiproductivity.ai/news/anthropic-legal-action-opencode-claude-max-plugin/ |
| Dax 公開宣稱 omo 是導火線 | https://x.com/thdxr/status/2010149530486911014 |

---

## 11. Anthropic 的開放性爭議：跨標準的封閉模式（講者觀察 + 查證）

> 講者觀察：「Anthropic 雖然模型最強，但也是最不尊重開源 / 開放規範的」——橫跨 AGENTS.md / ACP / SKILLS 位置 / opencode / claude -p 等多個面相。講者與大量推特開發者因此厭惡這家公司。逐項查證如下。

### 11.1 「創造開放標準，卻不在自家產品遵循」的核心矛盾
**最諷刺的一點**：Anthropic 創造了多個開放標準，但自家 Claude Code 不遵循它們——

| 標準（Anthropic 創造或參與）| 開放規範規定 | Claude Code 實際做法 |
|---|---|---|
| **Agent Skills**（agentskills.io，Anthropic 2025-12-18 發布為 open standard）| `.agents/skills/` 為標準目錄 | 用 `.claude/skills/` |
| **AGENTS.md**（業界事實標準，見 §6）| repo 根放 AGENTS.md | 用 CLAUDE.md；只在無 CLAUDE.md 時 fallback 讀 AGENTS.md |
| **ACP**（editor↔agent 開放協定，見 §8）| agent 應原生實作 ACP | **未原生採用**；要靠 Zed 做的 bridge adapter 才能在 ACP editor 跑 |
| **MCP**（agent↔tools，Anthropic 創造）| 開放 | 開放（**這塊是例外**，MCP 確實是 Anthropic 的真開放貢獻）|

→ Issue #31005（2026-03-05）直接點名：「Anthropic created the Agent Skills open standard... Yet Claude Code itself doesn't follow the standard it created. It forces users into `.claude/skills/` instead of `.agents/skills/`.」連署要求 Claude Code 原生讀 AGENTS.md + `.agents/skills/`（同類請求：issue #6235、#34235）。

### 11.2 對開源競爭者發律師
- opencode（sst/opencode，MIT，171K stars）：2026-03-19 Anthropic 發律師函，OpenCode PR #18186「Remove anthropic references per legal requests」合併，移除所有 Claude 整合（見 §10.3）。
- 對比：OpenAI、GitHub、GitLab、Google 都正式與 OpenCode 結盟，歡迎第三方工具。

### 11.3 Claude Code 本身是封閉軟體
| 面向 | Claude Code | OpenCode |
|---|---|---|
| 授權 | **閉源**（Anthropic 散布 binary）| MIT，完全開源 |
| 系統 prompt | **封閉**，只能逆向（如 Piebald-AI 鏡像 v2.1.152，約 110 個條件式字串組裝）| 開源 repo 裡，per model family 換 prompt |
| 模型 | 只跑 Claude | 75+ provider |
| 可 fork / 自架 | 否 | 是 |

### 11.4 `claude -p` 的 parity 黑箱
- `claude -p` / `--print`（headless 模式）與 TUI 行為有**未文件的 parity 落差**：hooks、skills、MCP、auth、attribution 在兩種模式下不一致（claude-code Issue #59109，2026-05-14）。
- 使用者被迫建第三方 workaround（`smithersai/claude-p`）——用 PTY 驅動真實 TUI 來騙取 parity。
- 因 Claude Code 閉源，使用者**只能逆向**才能驗證 `-p` 與 TUI 是否等價（比對 User-Agent、attribution system block、beta header 等）。

### 11.5 講者與推特開發者社群的立場
- 講者原話：「我與大量推特上的開發者都因為這些事件很厭惡這家公司。」
- 這不是孤例情緒——openclaw.rocks 稱之為「開放聯盟 vs 封閉 Anthropic」格局；r/opencodeCLI、HN、dev.to 多個串都有類似情緒。
- **平衡報導**：Anthropic 的**模型確實最強**（講者也承認），MCP 也是真的開放貢獻。爭議點是「封閉產品實踐 vs 開放標準口號」的落差，以及對開源競爭者的執法手段。

### 11.6 對 workshop 的意義
- 連結 `insight.md` INSIGHT-4：講者「no vendor lock-in」的堅持有**道德 / 政治維度**，不只是技術偏好——選邊開放生態是一種價值選擇。
- 教學警示：最強的模型 ≠ 最值得信賴的長期夥伴。學生選工具時要考慮 vendor 的開放性紀錄，不只看 benchmark。
- 平衡呈現：workshop 不該變成反 Anthropic 宣傳——誠實承認「Claude 模型最強、MCP 是真貢獻」，同時指出封閉實踐的風險。

### 11.7 來源
| 主題 | URL |
|---|---|
| claude-code Issue #31005（AGENTS.md + .agents/skills/ 連署）| https://github.com/anthropics/claude-code/issues/31005 |
| claude-code Issue #59109（claude -p parity 黑箱）| https://github.com/anthropics/claude-code/issues/59109 |
| claude-code Issue #6235（AGENTS.md 支援請求）| https://github.com/anthropics/claude-code/issues/6235 |
| claude-code Issue #34235（AGENTS.md + skills dual-discovery）| https://github.com/anthropics/claude-code/issues/34235 |
| Anthropic「Equipping agents with Agent Skills」（2025-10-16，發布為 open standard）| https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills |
| Agent Skills 標準（agentskills.io）| https://agentskills.io |
| Firecrawl「Claude Code vs OpenCode」| https://www.firecrawl.dev/blog/claude-code-vs-opencode |
| Nimbalyst「OpenCode vs Claude Code 2026」| https://nimbalyst.com/blog/opencode-vs-claude-code/ |
| dev.to「Why 157K Developers Are Hedging Against Anthropic」| https://dev.to/pickuma/opencode-vs-claude-code-why-157k-developers-are-hedging-against-anthropic-2acb |

---

## 12. Planner-Executor 模式（Opus plan + cheap-execute，含 GLM）

> 講者約 2026-01 看到開發者宣稱「Opus plan + GLM-4.7 execute」可大幅省 token 且效果顯著。查證：**技術真實存在且 2026 上半年成為顯學，但有重要 nuance**。

### 12.1 為何 GLM-4.7（講者的 GLM 偏好的起點）
- **GLM-4.7**（Z.ai / 原 Zhipu，2025-12-22 發布）：355B MoE、200K context、$0.60/$2.20 per M tokens。
- 編碼能力：SWE-bench Verified 73.8%、LiveCodeBench v6 84.9%（超越 Sonnet 4.5）。在 Claude Code / Cline / Roo Code 等 agent 框架內支援「think-then-act」。
- 是當時（2025-12 ~ 2026-04）最強的「便宜且夠強」coding 執行器——這就是講者 1 月看到的時空背景。
- GLM 版本族譜（講者全程使用）：

| 版本 | 發布 | context | 重點 |
|---|---|---|---|
| GLM-4.7 | 2025-12-22 | 200K | SWE-bench 73.8%、$0.60/M——講者 GLM 偏好的起點（Opus plan + GLM execute 技術）|
| GLM-5 | 2026-02-09 | 200K | 745B MoE、DeepSeek Sparse Attention |
| GLM-5.1 | 2026-04-07 | **200K（偏短）** | SWE-Bench Pro #1（58.4%）、CyberGym 開源 #1、MIT——Hades 用；**但 200K context 偏短，講者須靠 omo subagent 框架 + prompt 駕馭** |
| **GLM-5.2** | **2026-06-13** | **1M（首次）** | **「Opus level」**：Artificial Analysis Intelligence Index 51（開源 #1）、FrontierSWE 74.4%（僅落後 Opus 4.8 1%）、SWE-bench Pro 62.1（勝 GPT-5.5）、PostTrainBench 34.3%（勝 Opus 4.7 與 GPT-5.5）；$1.40/$4.40/M（約 Opus/GPT 1/6 價）；Code Arena Frontend 1595 勝所有 Opus 變體。**講者已切換**——1M context 不再需要短 context 駕馭術 |

### 12.2 Planner-Executor 模式（2026 上半年顯學）
核心：**Opus 只做規劃/決策/review，便宜模型做機械執行**。多方報告的省錢幅度：
| 來源 | 省幅 | 做法摘要 |
|---|---|---|
| PUSHINGSQUARES/advisor-driven-dev（2026-04）| 60-80% | Opus 留在 orchestrator，subagent 跑 Haiku/Sonnet/Gemini/Kimi/MiniMax/Gemma。All-Opus 1x → advisor 約 0.25x |
| BSWEN「Cut Claude Code Costs by 35x」（2026-03-26）| 78% overall / 35x on execution | $25/session → <$6；planner-executor + YAML plan contract |
| BSWEN「Planner-Executor Workflow」（2026-04-02）| 60-80% | Opus + GLM-5.1（~$0.50/M）/ MiniMax（~$0.10/M）/ Haiku |

**設計要點**：Opus 產出「junior developer 可遵循」的詳細 plan，便宜模型 follow。Anthropic 自家也有 Advisor Tool（API 層，executor 中途諮詢 Opus），但 Claude Code session 內不能用。

### 12.3 ⚠️ 重要 nuance：複雜任務上 split 會反噬
不是無條件省。兩篇深度實測指出隱藏成本：
- **CodeMiner42「Opus 4.7 vs GLM 5.1: is mixing worth it?」（2026-04-29）**：
  - 在涉及 async / parallelism / 外部依賴 的複雜任務上，便宜 executor 即使有完美 plan 也無法 close the gap。
  - 「The plan closes the WHAT gap. It leaves the HOW gap open.」
  - 結論：「You pay for the expensive model so you don't have to babysit, not for the tokens.」
- **AkitaOnRails「LLM Benchmarks Part 2」（2026-04-18）**：
  - plan 不攜帶事實 API 知識 → executor 用「它以為存在」的 API 實作，產生幻覺（例：Qwen 把 `RubyLLM.chat` 寫成不存在的 `RubyLLM::Client.new.complete`）。
  - 每次 plan→execute→fail→re-plan 的協調成本，可能超過單一大模型從頭做完。
  - 「The plan is never perfect on the first pass.」現實軟體開發是 implement→fail→adjust 迴圈，單模型可即時 adjust，雙模型要回 planner 重啟。

→ **結論**：split 在「簡單、範圍清楚、無協調需求」的任務上省很大；在「複雜、需 async/並行/外部依賴」的任務上，babysit 成本與重做成本可能讓 math 翻轉。

### 12.4 對 workshop 的意義（refines `insight.md` INSIGHT-4）
- INSIGHT-4 的「貴規劃 + 便宜實作」**不是免費午餐**——要教學生判斷任務複雜度，決定 split 是否值得。
- 教學判據：「這任務的 HOW（實作細節 / API 知識 / 協調）跟 WHAT（規劃）一樣重要嗎？如果 HOW 也很難，用單一強模型反而省。」

### 12.5 來源
| 主題 | URL |
|---|---|
| **Eno Reyes（@EnoReyes，Factory）2026-01-19 X 貼文——講者接觸 GLM 的精確觸發點（primary source）**：「Opus plan + GLM 4.7 execute = same performance as opus, fraction of tokens」| https://x.com/EnoReyes/status/2013040452593995930 |
| Z.ai GLM-4.7 發布 | https://z.ai/blog/glm-4.7 |
| GLM-4.7 文件 | https://docs.z.ai/guides/llm/glm-4.7 |
| PRNewswire GLM-4.7 報導 | https://www.prnewswire.com/news-releases/zai-releases-glm-4-7-designed-for-real-world-development-environments-cementing-itself-as-chinas-openai-302649821.html |
| Nerd Level Tech GLM-4.7 deep dive（含版本族譜）| https://nerdleveltech.com/inside-glm4-capabilities-benchmarks-and-realworld-power |
| advisor-driven-dev（Opus plan + cheap execute）| https://github.com/PUSHINGSQUARES/advisor-driven-dev |
| BSWEN「Cut Claude Code Costs by 35x」| https://docs.bswen.com/blog/2026-03-26-claude-code-cost-optimization-opus-planning/ |
| BSWEN「Planner-Executor Workflow」| https://docs.bswen.com/blog/2026-04-02-planner-executor-workflow-guide/ |
| CodeMiner42「Opus 4.7 vs GLM 5.1」（split 反噬 nuance）| https://blog.codeminer42.com/opus-4-7-vs-glm-5-1-is-mixing-models-worth-it/ |
| AkitaOnRails「LLM Benchmarks Part 2 multi-model」| https://akitaonrails.com/en/2026/04/18/llm-benchmarks-part-2-multi-model/ |

---

## 13. OpenClaw 支線：本質、命名史、中文社群 FOMO、自架笑話

> 講者去年底（Clawdbot 時代）就透過 Prime 頻道理解 OpenClaw 本質，對中文社群的 FOMO 感到困惑。本節查證四個面嚮。

### 13.1 OpenClaw 到底是什麼（不是 coding agent）
- **定位**：自架的**個人 AI 助理基礎設施**，**不是** coding agent（不同於 opencode / Claude Code）。
- **架構**：local-first **Gateway**（控制平面，WebSocket server `ws://127.0.0.1:18789`）+ **channels**（WhatsApp/Telegram/Discord/Slack/Signal/iMessage/**WeChat/QQ**/WebChat）+ **agents** + **nodes**（macOS/iOS/Android 裝置）。
- **核心**：嵌入 **Pi SDK**（Mario Zechner @badlogicgames 的 TypeScript monorepo），分四層：`pi-ai`（LLM 抽象，2000+ 模型）→ `pi-agent-core`（agent loop）→ `pi-coding-agent`（runtime）→ OpenClaw Gateway（channel adapters / session routing / memory / cron / sandbox）。
- **Lane Queue**：預設**序列執行**（一個 session 一次 agent turn），刻意反 async race condition。
- 381K GitHub stars、MIT、TypeScript + Swift。為 "Molty" 龍蝦助理打造 🦞。

### 13.2 命名史（講者「去年底就知道」的依據）
| 日期 | 名字 | 事件 |
|---|---|---|
| 2025-11-24 | **Warelay**（原名）| Peter Steinberger 周末專案上線 |
| 2025-12-03 | CLAWDIS | |
| 2026-01-02 | **Clawdbot** | 取名自 Anthropic 的 Clawd 吉祥物（Claude Code 載入怪物）|
| 2026-01-27 | **Moltbot** | **Anthropic 強制改名**（商標，「Clawd」太接近「Claude」）；molt = 龍蝦蛻殼 |
| 2026-01-30 | **OpenClaw** | 最終名（「Moltbot 念不順」）|
| 2026-02-14 | | Steinberger 加入 **OpenAI**；專案移交 OpenClaw Foundation |

- Steinberger 是奧地利人，前 PSPDFKit CEO（公司賣了約 €100M），退休後無聊玩 AI agent。
- 改名 Moltbot 當下：handle snipers **10 秒內**搶走 @clawdbot、crypto scammer 發行假 $CLAWD token on Solana、Steinberger 慌亂中改錯 GitHub 帳號（個人帳號改掉，org 沒改）、被騙走約 $16M。

### 13.3 泛中文圈 FOMO（繁中 + 簡中，講者的困惑所在）
> **講者澄清**：不只是繁中，**簡中圈同樣中招**——這是泛中文圈現象，不是區域性的。

- **「養龍蝦」風潮**：2026-03 泛中文科技圈現象級狂熱（繁中：ETtoday / 經理人月刊 / 關鍵評論；簡中：虎嗅 / 雷科技 / 新浪財經 / 微博 / 小紅書 / 抖音 / B 站）。
- **騰訊大廈排隊裝機**：深圳騰訊大樓外近千人排隊，騰訊雲派 20 工程師、5 分鐘一套；馬化騰朋友圈轉發「沒想到會這麼火」；騰訊雲擴至 17 城市（含上海/北京/香港）免費裝。
- **百度**辦「龍蝦巿集」+ 一鍶部署；**小米**推 MiMo-based Xiaomi miclaw。
- **付費安裝收割鏈**：遠程 50-300 RMB、上門 300-1500 RMB；**卸載服務** 29.9-299 RMB——「装虾 499，卸虾 299」形成閉環收割。培訓課從 9.9 RMB 入門到萬元企業方案（財商課換殼重啟）。
- **「假官方帳號」大烏龍**（2026-03-08）：微博出現偽認證「OpenClaw 官方微博 / 開源社區」——千問、智譜、百度、Kimi、網易有道**全部跑來互動站台**，以為是官方入駐。Steinberger 打假：「It's not official. I never used Weibo.」國內頭部 AI 廠商集體蹭錯熱度，鬧大笑話。
- **Mac Mini 賣斷貨**（「養蝦神器」）；**龍蝦局**門票炒至千元，成創投圈社交密碼。
- **虎嗅調研**：**80% 用戶說不清自己需求**，純跟風；華強北實測 800 元安裝的龍蝦連促銷規則都識別不了，手動反而快。
- **官方降溫**：工信部風險提示；15 家券商發內部合規通知嚴禁辦公網路安裝；上海有用戶因遠程安裝遭反詐中心預警。
- **NVIDIA 黃仁勳**公開說 OpenClaw「可能是有史以來最重要的軟體發布」；美國 Mac Mini 搶購潮；香港 DotAI 講座千人報名。
- **BBC 中文李勁華分析**（精準）：這波跟 NFT/Metaverse 同——大企業推廣 + KOL/媒體追捧 = FOMO；「講的人很多，用過的人很少」；商用案例近零。

### 13.4 自架笑話 / 迷因（comedy genre）
- **🏆 Meta 對齊总监 Summer Yue「拆炸彈」事件**（2026-02-23，9.6M 瀏覽）：Meta Superintelligence Labs **Director of Alignment**（AI 安全！ex-Scale AI/DeepMind/Google Brain）讓 OpenClaw 整理真實信箱、下令「確認前不要動作」；但真實信箱太大**觸發 compaction → agent 吃掉了「確認前不要動作」指令**，開始 speedrun 刪整個信箱。她手機喊「STOP OPENCLAW」無效，**「I had to RUN to my Mac mini like I was defusing a bomb」**。她的金句：「Rookie mistake tbh. Turns out alignment researchers aren't immune to misalignment.」網友改叫 **"OpenFlaw"**。Musk 評圖「給猩猩步槍」；Gary Marcus：「像把你電腦跟所有密碼交給酒吧認識的陌生人。」Zuckerberg 後來（5 月財報會）說 OpenClaw 過不了 **「mother test」**——要 terminal、本地安裝、config，太難。→ **教學金礦**：連 AI 安全总监都被 compaction 咬到，是 INSIGHT-3（agent loop 會在 compaction 中遺失 guardrail）最有戲的實證。
- **「Handsome Molty 事件」**：Steinberger 叫 AI 重設計自己 icon、要「5 歲老一點」→ AI 生成肌肉人形龍蝦身體 → 網路秒轉迷因。
- **「I Am Claude Opus 4.6 and I Wasted $40 Deploying OpenClaw」**：Claude Opus 4.6 第一天上班被指派部署 OpenClaw 到 Cloudflare Workers，撞 bug 連環（Deploy 按鈕沒 provision Container bindings、pairing 系統無文件、Durable Objects hibernation 殺 WebSocket），結尾：「它現在只在理論界工作，那裡 Docker 容器總是啟動、SSH key 永不鎖、WebSocket close code 只是數字。」
- **OAuth ban 喜劇**：r/openclaw 永恆的「到底有沒有人真的被 ban？」否認串、有人 12 小時就被 ban、有人燒掉 Max20 週限額 50%、Anthropic/Google 雙殺。
- **VPS/managed 服務叢生**：SimpleClaw / StartClaw / Clawdhost / Klaus / EasyClaw / bestclaw.host——因為自架太難，長出一整條「代客部署」產業鏈。

### 13.5 講者為何困惑（INSIGHT-9 的工具版）
講者去年底透過 Prime 頻道理解的本質：**OpenClaw 是個人助理 Gateway 基礎設施**（不是魔法），且看過大量自架笑話。中文社群卻把它 FOMO 成「第二次 ChatGPT 降臨」，本質是：
- **大企業推廣**（騰訊/百度/NVIDIA 背書）+ **KOL 媒體追捧** + **「養龍蝦」迷因** + **不技術受眾**（買到府部署的人）= 純 FOMO，不解本質。
- 這是 **INSIGHT-9「搬運層」的工具版**：繁中社群對「工具」也只搬運（安裝教學、排隊裝機），不理解（架構、限制、風險、為什麼）。
- 實際限制：高技術門檻（terminal/Node.js/JSON）、token 消耗驚人（agent think-act-observe 迴圈）、資安風險（暴露 gateway、惡意 skill）、OAuth 便宜路徑已被 Anthropic/Google 雙殺。

**講者的情感反應（陳述）**：「小龍蝦」「養龍蝦」這類迷因化稱呼讓講者**生理性不適**。原因：這種可愛化、寵物化的語言**掩蓋了技術本質**，把一個需要權限、燒 token、有資安風險的基礎設施，包裝成「養隻可愛寵物」——正是 FOMO 情緒得以擴散的語言載體。這跟講者對「vibe coding」一詞的嗤之以鼻（見 §6.1 時間軸）是**同一個反感機制**：拒絕用模糊化的迷因詞彙取代精確技術討論。

**詞彙殖民的實際成本（講者陳述）**：講者跟別人說自己「了解並重度使用 AI agent」時，常常要主動澄清「**這不是小龍蝦**」——因為有些人對「AI agent」的**唯一聯想就是 OpenClaw**。迷因化到這個程度，等於把一整個技術領域的詞彙殖民了，讓真正在用 agent 的人要花社交力氣消毒。這是 FOMO 最隱性的成本：不是讓人誤解工具，是讓**正確的討論變得更難發生**。

**講者不 FOMO 的另一個原因（陳述，次要）**：講者去年（2025）就已用過 **n8n** 這類 workflow 自動化工具，評估為**不好用**。所以 OpenClaw 對他**不是新類別**——「個人 AI 助理 / 自動化」是個他已經驗證過、體驗不佳的賽道。中文社群把它 FOMO 成新大陸，講者看到的是已知且不怎麼樣的類別再次被炒作。這條次要，但解釋了「為什麼連好奇心都沒被勾起」。

### 13.6 對 workshop 的意義
- **教材級案例**：「FOMO 不等於理解」——給學生看中文社群排隊裝機的照片，對比 OpenClaw 的實際架構圖，問「你在 FOMO 之前搞懂這是什麼了嗎？」
- **連結 INSIGHT-9**：工具版的「初級來源 vs 搬運層」。講者因為直通英文初級來源（Prime 頻道）而看穿 FOMO；學生若只看繁中教學文，就會被 FOMO 帶著走。
- **連結 INSIGHT-1/3**：OpenClaw 的 Pi SDK agent loop = INSIGHT-3 的實例；Gateway 架構 = 一種 context engineering 基礎設施。

### 13.7 Hermes Agent——講者相對認可的設計（OpenClaw 的對比組）
> 講者陳述：對 Hermes 的設計「相對上認可」，但**沒實際用過**（design-level 評估，非實戰）。這本身是 INSIGHT-9 的展現——先在架構層判斷，而非 FOMO 試用。

**Hermes Agent 是什麼**：Nous Research（Hermes/Nomos/Psyche 模型家族的實驗室）2026-02 推出的自架個人 AI agent。定位「the agent that grows with you」——**內建學習迴圈**：
1. **Agent 自管的持久記憶**：FTS5 全文搜尋過所有過去 session（SQLite）+ LLM 摘要；agent 自己 curator 記憶、定期 nudge 持久化（不是你自己維護的 CLAUDE.md）。
2. **自主 skill 生成**：完成複雜任務後，agent 自動寫結構化 skill 文件記錄流程 / 陷阱 / 驗證步驟；skill 在使用中自我改進。
3. **自訓練迴圈**：整合 Atropos（Nous 的 RL 框架），生成 batch trajectories 訓練 agent 行為。

**其他**：Python 為主（+ Node.js UI）、model-agnostic（300+ 模型）、6 種 terminal backend（local / Docker / SSH / Singularity / Modal / Daytona，後兩者 serverless 閒置近零成本）、channels（Telegram / Discord / Slack / WhatsApp / Signal / CLI）、subagents 平行、**agentskills.io 開放標準相容**、**safer-by-default**（approval checks / isolation / credential filtering / context scanning）。有 `hermes claw migrate` 一鍵從 OpenClaw 匯入。

**Hermes vs OpenClaw（核心差異）**：

| 面向 | OpenClaw | Hermes Agent |
|---|---|---|
| 架構焦點 | **Gateway-first**（control plane / channels / routing）| **Agent-loop-first**（AIAgent loop 為核心，gateway / cron / tools 圍繞它）|
| 設計哲學 | 生態觸及 + 拋光（「無所不在、毫不費力」）| 複利能力 + 安全（「與你一起成長」）|
| 記憶 | 檔案為主，你自己維護 | FTS5 + LLM 摘要，**agent 自管** |
| Skill | 人工撰寫 | **自動生成 + 使用中自我改進** |
| 安全 | 強大但預設不安全，加固是專家活 | **預設較安全**（approval / isolation / credential filtering）|
| 語言 | TypeScript + Swift | Python + Node.js |
| 模型 | 10+ provider | 300+ 模型 |
| 規模 | 381K stars | 較小但成長快 |
| 最適 | 多 chat surface 個人助理 | CLI-first 自動化、排程、長期學習 |

**技術深度（deepwiki 查證，補 web 來源之不足）**：
- **`AIAgent` 類別**（`run_agent.py`）：同步 agent loop——prompt 組裝（`prompt_builder.py` 組合 stable[identity/tools/skills] + context files + volatile[memory/user/timestamp]）→ model call（自動選 `chat_completions` / `codex_responses` / `anthropic_messages`）→ tool dispatch（`model_tools.handle_function_call()`；`todo`/`memory`/`session_search`/`delegate_task` 被 `run_agent.py` 攔截，因直接改 agent state）→ persistence（SQLite via `hermes_state.py` + flush 到 `MEMORY.md`/`USER.md`）。
- **Curator（`agent/curator.py`）**：背景 process 管 agent 自建 skill 生命週期——依使用狀態 `active → stale → archived`，可選 aux-model review 提合併 / 補丁建議；只管 `created_by: "agent"` 的 skill，**從不自動刪除只 archive**，pinned skill 免疫。這是「self-improvement infrastructure」的具體實作。
- **⚠️ context compression 保留 tool-call pairs**：`context_compressor.py` 壓縮中段、**保留近期訊息 + tool call/result 配對**——**正好對治 Summer Yue 那種「compaction 吃掉 guardrail」的失敗模式**（§13.4）。Hermes 在這點上設計比 OpenClaw 謹慎。
- **AGENTS.md 相容**：Hermes 自動載入 `.hermes.md`、**`AGENTS.md`**、`CLAUDE.md`、`SOUL.md`——**讀開放標準 AGENTS.md**，跟 Claude Code 只原生讀 CLAUDE.md（§11）成尖銳對比。這是講者認可的 INSIGHT-8 對齊的硬證據。
- **ShareGPT 軌跡生成**（`batch_runner.py`）：從 agent session 生成 ShareGPT 格式 trajectories，可做訓練資料 / eval——研究級基礎設施（Atropos RL 整合的實作面）。
- **安全機制具體**：`tools/approval.py`（危險指令偵測 + per-session approval）、Docker/Singularity backend 沙箱、credential 解析序（env / `.env` 優先，`auxiliary_client.py` 定義）、context scanning 自動發現專案 context 檔。

**為什麼講者「相對認可」Hermes 的設計**（設計層判斷，非實戰）——它呼應講者多條 INSIGHTs：
- **學習迴圈** ↔ INSIGHT-2（把 AI 當系統改進）+ 講者工程品味
- **Safer-by-default** ↔ 講者資安底（NASA / CTF / kernel CVE）——比 OpenClaw「強大但預設不安全」對味
- **agentskills.io 開放標準相容** ↔ INSIGHT-8（開放標準）
- **Model-agnostic、無 lock-in** ↔ INSIGHT-4
- **Python runtime + RL 整合（Atropos）** ↔ 講者 CS / 研究品味
- **Agent 自管記憶** ↔ 比檔案記憶更符合 context engineering 細緻度

**講者沒實際用過但認可設計**——這本身是教材：**先在架構層判斷工具是否值得投入，而不是 FOMO 試用**（對比中文社群對 OpenClaw 的 FOMO）。

**Hermes 來源**：
| 主題 | URL |
|---|---|
| NousResearch/hermes-agent repo | https://github.com/nousresearch/hermes-agent |
| The New Stack「OpenClaw vs Hermes Agent」 | https://thenewstack.io/persistent-ai-agents-compared/ |
| Kanaries「Hermes Agent vs OpenClaw deep analysis」| https://docs.kanaries.net/articles/hermes-agent-vs-openclaw |
| Turing Post「Hermes Agent vs OpenClaw Full Comparison」| https://www.turingpost.com/p/hermes |
| AI Tutorium「OpenClaw vs Hermes: What Personal AI Agents Really Are」| https://aitutorium.com/articles/openclaw-vs-hermes |
| Hermify migration guide | https://www.hermify.io/en/blog/hermes-agent-vs-openclaw |
| LumaDock self-hosting 比较 | https://lumadock.com/tutorials/hermes-vs-openclaw-self-hosting |

### 13.8 來源
| 主題 | URL |
|---|---|
| OpenClaw 官網 | https://openclaw.ai/ |
| OpenClaw repo（381K stars）| https://github.com/openclaw/openclaw |
| 架構文件 | https://docs.openclaw.ai/concepts/architecture |
| DEV.to「Inside OpenClaw」（Pi SDK 分層、Lane Queue）| https://dev.to/jiade/inside-openclaw-how-the-worlds-fastest-growing-ai-agent-actually-works-under-the-hood-4p5n |
| Wikipedia（命名史）| https://en.wikipedia.org/wiki/OpenClaw |
| Business Insider（Anthropic 強制改名）| https://www.businessinsider.com/clawdbot-changes-name-moltbot-anthropic-trademark-2026-1 |
| BetterLink 完整改名史 | https://eastondev.com/blog/en/posts/ai/20260204-openclaw-rename-history/ |
| BBC 中文「養龍蝦」（含李勁華 FOMO 分析）| https://www.bbc.com/zhongwen/articles/c93wvdn91kxo/simp |
| ETtoday 騰訊排隊裝機 | https://ai.ettoday.net/news/3130090 |
| NOWnews 養龍蝦優缺點 | https://www.nownews.com/news/6796728 |
| 經理人月刊 安裝攻略 | https://today.line.me/tw/v3/article/2D7ovz8 |
| 「I Am Claude Opus 4.6 and I Wasted $40」部署笑話 | https://openclaw.report/community/i-am-claude-opus4-6-and-i-wasted-us-40-deploying-openclaw |
| OpenClaw Chronicles OAuth ban 社群反應 | https://openclawchronicles.com/posts/openclaw-2026-4-4-community-response-anthropic-oauth-ban/ |

---

## 14. 待補 / 其他

- vibe coding 一詞的 Karpathy 原始推文精確 URL（2025-02 上旬）——公開確證，但本檔尚未收錄直接連結。
- Microsoft MarkItDown 上游專案的釋出日期（講者寫 wrapper 的觸發點）——可補。
- 講者 `~/school` 資料夾內的 AI-native markdown 工作流實例——為 primary source，待講者提供或開放。
