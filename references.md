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
| 起源：**Sourcegraph Amp** 團隊發起，後由 OpenAI、Google (Jules)、Cursor、Factory 聯合推動 | https://ccmd.dev/t/agents-md-design-decisions |
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

## 7. 待補 / 其他

- vibe coding 一詞的 Karpathy 原始推文精確 URL（2025-02 上旬）——公開確證，但本檔尚未收錄直接連結。
- Microsoft MarkItDown 上游專案的釋出日期（講者寫 wrapper 的觸發點）——可補。
- 講者 `~/school` 資料夾內的 AI-native markdown 工作流實例——為 primary source，待講者提供或開放。
