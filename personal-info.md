# 講者個人資訊 — G36maid

> 本檔作為 AI Workshop 的「內容源頭」之一。講者的真實經驗 = 教材的黃金來源。
> 之後設計大綱時，會回頭把這裡的條目對應到「可教單元」。

---

## 1. 基本背景

- **身份**：台師大資工系 / 機電工程系雙主修，目前大四
- **升學路徑**：高中程式競賽選手（自評非頂尖）→ 大一深度使用 Arch Linux → 大二接觸 Rust → 開源愛好者
- **AI 資歷（LLM 土著）**：大一（2022-23）就在用 ChatGPT（GPT-3.5，2022-11-30 公開），幾乎與 ChatGPT 同步起步；GPT / Gemini 兩大系列都長期使用至今
- **跨校修課**：透過「台灣大學系統」（NTU / NTNU / NTUST 三校）將台大資工課程修到上限
- **人格特質**：系統工程導向、low-level 偏好、開源貢獻者、自架 homelab
- **社群參與**：AsiaBSDCon 2026 Staff、SITCON 2024/2025 Staff

> 與受眾（大學/碩士生）幾乎同世代，這既是優勢（可親）也是風險（容易預設共同知識）。

---

## 2. 修課紀錄（透過三校系統 @ 台大資工）

> 修課取向高度一致：**系統 + 低階 + 資安 + 理論**。沒有走 web/ML 派，是純血 systems hacker 路線。

| 課程 | 全名 / 性質 | 重點 | 與 workshop 的關聯 |
|---|---|---|---|
| **NASA** | Network Administration & System Administration（台大資工，蔡教授）| Pass/Fail，每週 10–20 hr 作業；Bash、Vim、VLAN、PowerDNS、LDAP、firewall、Docker、VM；培訓系上 NASA 網管團隊 | 你的 infra/terminal/agent 環境觀念源頭 |
| **DSA** | 演算法設計與分析（台大必修）| 演算法核心訓練 | 「知道 AI 該被限制在哪」的判斷力來源 |
| **高等編譯器 (ACD, CSIE5054)** | Advanced Compiler Design（廖世偉 + jserv 合授，研究所級）| Dragon Book + Cornell CS6120；data flow、SSA、LLVM IR、LLVM pass、affine partitioning、DCE/LVN；Bril 作業 | 處理「符號 / 語意等價」的硬底子 |
| **系統軟體設計與實作特論** | 研究所特論（jserv 體系）| RTOS、kernel、低階系統軟體實作 | 你能看穿 AI 對「系統行為」的幻覺的原因 |
| **資訊安全 / 計算機安全** | 台大資安課（高度 CTF 實務導向）| 實戰 CTF | 直接對應你的 `ctf-arsenal` repo |
| **函數式程式設計** | Functional Programming | Haskell / OCaml 類型系統、純函數思維 | 「型別安全、副作用控制」的工程品味 |
| **CUDA** | Introduction to CUDA Parallel Programming | GPU 平行運算 | 對應你的 `cuda-prog` repo |

---

## 3. 技術棧與環境

### 程式語言
Rust（主力）、Go、C / C++、Python、Bash；接觸過 Gleam、Haskell、Solidity、Swift

### OS / 虛擬化 / 儲存
- **OS**：Arch Linux（daily driver）、FreeBSD（長期貢獻目標）
- **WM**：Hyprland（Wayland）
- **虛擬化**：Proxmox Cluster、QEMU、Docker、Kubernetes
- **儲存**：ZFS、Btrfs、TrueNAS
- **網路**：OPNsense、Tailscale、MQTT、Ansible

### 開發工具鏈
- **Terminal**：Kitty + zsh (zim) + tmux
- **Editor**：Zed（Guild Contributor）、Neovim、vim
- **檔案管理**：yazi、lazygit、lazydocker
- **Dotfiles 管理**：GNU Stow（repo: `G36maid/dotfiles`）

### Homelab
Proxmox Cluster 跑 TrueNAS + OPNsense + 多種 Docker 服務，ZFS 底層、Zero-Trust 網路（Tailscale）。是日常實驗與 agent 部署的場域。

---

## 4. 開源貢獻紀錄（GitHub: G36maid）

### 主要貢獻對象
| 專案 | 性質 | 你的貢獻 |
|---|---|---|
| **zed-industries/zed** | 高效能多人協作編輯器（Rust）| Guild Contributor；多個 PR：agent auto-compact on token limit、FreeBSD remote_server 支援、format-on-save 改良、macOS binary name resolution 修復 |
| **opencode (anomalyco/opencode)** | AI agent coding orchestrator | docs PR：Arch Linux pacman 安裝、社群連結 i18n |
| **oh-my-openagent (code-yeongyu)** | opencode 的進階 harness（omo）| PR：GitHub Copilot subscription tier 支援、docs 修正 |
| **sessatakuma 系列** | jpcorrect-backend、org-workflows、Talkuma | 持續協作：CI/CD workflows（golangci-lint）、GORM migration、DB 層重構、後端實作 |
| **rust-minidump/minidump-writer** | Rust crash-handling | FreeBSD 支援 PR |
| **hyprwm/hyprpwcenter, hyprlauncher** | Hyprland 周邊 | zh_TW i18n |
| **Moxa（實習）** | Backend intern | Golang / Headscale 相關；**外部驗證**：雖為大學 intern，能力被評為「比碩士還強」，被當正職工程師看待（多模型調度等 workflow 即在此期間發展）|

### 自己維護的專案
| Repo | 內容 |
|---|---|
| `zed-mcp-server-markitdown` | 自己寫的 MCP server（Rust + Wasm），把 Microsoft MarkItDown 整合進 Zed；**A 典範設計（單一深工具）**；Zed 商店 **29,963 下載**（2025-09-25 上架）|
| `ctf-arsenal` | CTF 工具箱，用 `.agents/skills/*/SKILL.md` 結構模組化（pwn/web/ics/crypto/forensics）|
| `dotfiles` | Arch + Hyprland 完整設定（含 opencode/omo 設定與 `oc()` wrapper）|
| `akartui-rs`、`brainfuck-rs`、`fourbar-linkage-analysis`、`gleam-pacman` | Rust 練習 / 工具 |
| `cpgrader_rs` | NTNU 計程 I/II 自動評分工具 |
| `cuda-prog` | CUDA 作業 |
| `ComputerArchitecture_MDnotes` | NTU 計結筆記（pptx2md 產出）|

---

## 5. AI Agent 實踐（教授看到的 insight 的核心）

> 與「用 ChatGPT 寫程式」派的根本差異：把 agent 當成**可編程的協作系統**，自己打造 orchestrator + MCP + skill 模組。

### 5.1 Agent Orchestrator 當日常 Driver
- **opencode / oh-my-openagent (omo)** 是日常 coding agent harness
- dotfiles 裡自寫 `oc()` zsh function：把 opencode 包進專屬 tmux session（以當前目錄命名）、自動在 4096–5096 選 free port（export 成 `$OPENCODE_PORT`）、可 `--resume`
- 同時跑多個 agent 來源，並用 `agent-quota` 監控訂閱限流

#### 為何選 opencode（哲學對齊）
講者從 **ThePrimeagen 的 Standup podcast**（Dax Raad 來賓，講「agent 是什麼」+ opencode，見 `references.md` §7）認識此工具，**自 v0.1.0 起用**。三個設計理念完全對齊講者：

> **同場加映**：此 podcast 也是 **`insight.md` INSIGHT-3（agent = LLM + Tools + Loops）的直接出處**——Adam 在 [04:32] 給出此定義，講者從此吸收此心智模型。完整 timestamped 內容見 `references.md` §7.4（含 LSP 回授驗證、vibe benchmarking、human-in-loop 等關鍵討論）。

| 設計理念 | opencode 實作 | 對應 insight |
|---|---|---|
| **No vendor lock-in** | 75+ provider（via Models.dev），`provider/model-id` 格式可插任意模型（含 local model）；開源（179K stars / 900 contributors）| INSIGHT-4（模型自由組合）|
| **Plan / Build 雙模式** | `plan`（read-only 分析，**嚴禁 edit codebase，但允許 edit `.opencode/plans/*.md`**——能寫計畫卻碰不到程式碼）vs `build`（full access）。permission 系統 allow/ask/deny，bash 支援 glob（`git *` allow、`rm *` deny）、`external_directory` 管專案外存取 | INSIGHT-7（關注分離）+「用戶極大自定性」|
| **極大自定性** | agent 可用 JSON（`opencode.json`）或 **markdown**（`.opencode/agents/*.md`，frontmatter + body 當 system prompt）定義；primary / subagent / hidden system agents（compaction/title/summary）；config deep-merge；escape hatches（`OPENCODE_DISABLE_PROJECT_CONFIG`、`OPENCODE_PURE`）| markdown 定義 agent 的 pattern 跟 AGENTS.md（INSIGHT-8）/ SKILL.md **同源** |

#### 社群追蹤
常看 **Dax（@thedxr）** 與 SST/OpenCode 團隊在 X 的開發見解，**包含與大公司的公開爭論（理念之爭）**——這是講者 INSIGHT-9 的初級來源之一（直接吸收源頭業界辯論，而非繁中搬運層）。

#### Meta 連結
講者日常用的 opencode/omo，**就是本籌備 session 正在跑的 orchestrator**（其 explore/oracle/librarian/metis/momus subagent 結構 = opencode subagent 系統的訂製版本）。講者「活在自家哲學對齊的工具裡」。

#### omo（oh-my-openagent）的發現與 Sisyphus 偏好
- **發現時序**：opencode 之後，講者繼續 OSS 貢獻、開發與修課期間，發現了 **oh-my-openagent（當時叫 oh-my-opencode）**——建立在 opencode 之上的進階 harness（即本 session 跑的 orchestrator）。
- **改名背景**：npm 包仍名 `oh-my-opencode`（過渡期 dual-publish 為 `oh-my-openagent`）；config 同時認 `oh-my-opencode.json[c]` 與 `oh-my-openagent.json[c]`。改名主因是與 sst/opencode（Dax 的工具）消歧——omo 是 opencode **之上**的 harness，不是同一層。Maintainer: Yeongyu Kim。
- **講者最愛的設計：Sisyphus 的 todo-driven 持續性**。Sisyphus（希臘神話推巨柱者）= omo 主 orchestrator：① 開工前先建 todo list；② 若 LLM 想結束但 todo 未完 → **hook 注入（鞭打）它繼續執行**；③ 持續到所有 todo 完成才允許結束。
- **對比另一派：Ralph Loop**（Geoffrey Huntley 提出，「Ralph is a Bash loop」，命名自 Simpson 的 Ralph Wiggum）。Ralph 不看 todo，而是**每次 agent 結束就把同一 prompt 重新注入**，靠檔案系統 + git 當記憶體，直到吐出 completion promise。

| 機制 | 誰決定還沒完 | 記憶放哪 |
|---|---|---|
| **Sisyphus Todo Continuation** | agent 自建 todo list | 同 session 對話 |
| **Ralph Loop** | 外部固定 prompt | 檔案系統 + git history（每輪 fresh context）|

- 講者**偏好 Sisyphus**（todo-driven，更尊重 agent 的計畫）。omo 兩種都內建（Todo Enforcer 自動 + `/ralph-loop` 指令）。
- **自我指涉**：本 session 就是 Sisyphus 在跑，且 system prompt 那句「YOUR TODO CREATION WOULD BE TRACKED BY HOOK([SYSTEM REMINDER - TODO CONTINUATION])」就是這套機制的觸發條件——**講者邊講邊被它驅動**。
- 完整 omo/Ralph 生態見 `references.md` §9；持續性機制作為 INSIGHT-3 的延伸見 `insight.md` INSIGHT-3。

#### 學術延伸：Hades 資安 agent（cs-special-topics-2 專題）
講者不只是 omo 使用者，更在 NTNU「計算機科學專題二」課程中**以 omo 為基礎打造一個完整的資安 agent 系統（Hades）**——718 行架構報告（`~/School/ntnu/cs-special-topics-2/docs/report.md`）。

- **Hades** = 講者透過 omo config 新增的 primary agent，專責資安分析；整合 VulnClaw（21 skills / 180 references）+ Ghidra-MCP（249 逆向工具）。
- **零代碼整合**：純 config 實現，不改任何開源專案原始碼——展示 omo 的「極大自定性」不是口號，呼應 INSIGHT-8（markdown/config 定義 agent 行為）。
- **多模型分工**：Hades 用 **GLM-5.1**（SWE-Bench Pro #1、CyberGym 開源 #1、MIT 授權、便宜）做主力；Oracle 用 GPT-5.5、Explore/Librarian 用 gpt-5.4-mini。
- **GLM 偏好的起點**：講者於 **2026-01-19** 看到 **Eno Reyes（@EnoReyes，Factory）** 在 X 發布的貼文（131.5K views / 814 likes / 479 bookmarks）：「The most cost effective combination right now is setting Opus as your plan model and **GLM 4.7** or GPT-5.2-Codex as your execution model. Gives you basically the same performance as opus, for a fraction of the tokens.」——這是講者接觸開源 GLM 模型的精確觸發點。GLM-4.7 於 2025-12-22 由 Z.ai 發布（SWE-bench 73.8%、$0.60/M），是當時最強的便宜 coding 執行器。軌跡：**GLM-4.7（2025-12）→ GLM-5.1（2026-04，Hades 用）→ GLM-5.2（本 session 用）**。**這正是本 session 跑在 GLM 上的原因**——講者把這條學習曲線延伸到日常。完整 planner-executor 模式與 nuance 見 `references.md` §12。
- **GLM 偏好的深層理由 = 「最強的開源模型」**：講者選 GLM 不只因便宜，更因它是**開源 + 強**的甜點——MIT 授權、可自架、無 vendor 風險（呼應被 Google ban 的教訓與 INSIGHT-4）。閉源最強是 Claude Fable 5 / Opus 4.8，但講者寧可取「開源最強」也不要「絕對最強但被封閉綁住」。這是價值選擇，不只是效能選擇。
- **GLM-5.1 → GLM-5.2 切換（2026-06，最近）**：講者長期用 GLM-5.1，但 5.1 只有 **200K context**（偏短），必須靠 **omo subagent 框架 + 精細 prompt 把任務拆小**才能駕馭——這是把 INSIGHT-3（agent = loop）+ INSIGHT-4（decomposition）當作「**用 subagent 拆解擊敗單模型 context 上限**」的技術。**GLM-5.2（2026-06-13 發布，1M context）已被獨立評測認定為「Opus level」**（FrontierSWE 74.4% 僅落後 Opus 4.8 1%、Artificial Analysis Intelligence Index 51 開源 #1、PostTrainBench 勝 Opus 4.7 與 GPT-5.5），講者已切換，不再需要短 context 駕馭術。完整 5.2 benchmark 見 `references.md` §12.1。
- **provenance 連結**：這條軌跡是 INSIGHT-9（初級來源）的活體示範——講者直接吸收 Eno Reyes 這位 agent 工具圈核心人物（Factory 是 AGENTS.md 開放標準的聯合推動者之一）的第一手實測意見，而非繁中搬運層。
- **核心創新**：「通用 agent + 領域 skill 注入」——不是為每個分析面向建專門 agent，而是讓通用 agent 在接收任務時動態獲得領域知識，且可同時 spawn 多個 instance 平行分析（INSIGHT-4/7 的進階應用）。
- **workshop 價值**：這份報告本身就是現成的「如何用 omo 構築領域 agent」教材範本，可直接展示。

#### 親身經歷：被 Google Antigravity ban（INSIGHT-4 的切身實證）
講者**親身是 2026 上半年 Google Antigravity ban 波的當事人之一**——用了 `opencode-antigravity-auth`（反代 Google Antigravity IDE 模型到 opencode 的 plugin，11K stars）一段時間後，被 Google 終身封號。完整事件見 `references.md` §10.5。

**這是講者 INSIGHT-4（no vendor lock-in）最切身的來源**：不是理論上的偏好，而是被 vendor 執法燙過後的教訓。講者對「多模型組合、不綁單一 provider」的堅持，部分源自此經歷。

**對 workshop 的價值**：第一手「我試過、我被 ban、後來如何」的故事——比任何二手警告都有說服力。可當開場 hook：「你們有人用過把 ChatGPT/Claude/Gemini 訂閱接進其他工具的 plugin 嗎？我被 ban 過。」

#### 實際 config：多 provider 混合（live，已檢查 dotfiles）

講者的 `~/Code/Github/dotfiles/opencode/.config/opencode/oh-my-openagent.json` 是**多 provider 混合的 live 範本**（INSIGHT-4/8 的生產實作）。混了 **4 個 provider 訂閱 / gateway**：

| Provider | 性質 | 用到的模型 |
|---|---|---|
| `zai-coding-plan` | Z.ai GLM Coding Plan 訂閱 | glm-5.2、glm-4.7、glm-4.6v（視覺）|
| `opencode-go` | OpenCode 自家 gateway | glm-5.2、qwen3.7-plus、minimax-m3/m2.7、kimi-k2.6 |
| `openai` | OpenAI / Codex 訂閱 | gpt-5.5、gpt-5.4-mini-fast、gpt-5.4-mini/nano |
| `google` | Gemini | gemini-3-flash-preview、gemini-3.1-pro-preview |

**per-agent + per-category 路由 + fallback 鏈**（規劃-執行分離的生產版）：
- **orchestrator / 規劃**（Sisyphus、Prometheus）：glm-5.2（zai）主力
- **深度推理**（Oracle、Metis、Momus）：gpt-5.5 high / xhigh
- **深度執行**（Hephaestus、deep category）：gpt-5.5 medium
- **批量執行**（Sisyphus-Junior、Atlas）：glm-5.2 → kimi / minimax fallback
- **快搜**（Explore、Librarian、quick category）：gpt-5.4-mini-fast → glm-4.7 → qwen → minimax → nano
- **視覺**（Multimodal-Looker）：gemini-3-flash → glm-4.6v
- **前端 / 創意**（visual-engineering、artistry）：gemini-3.1-pro
- **困難邏輯**（ultrabrain）：gpt-5.5 xhigh

**關鍵設計**：
1. **fallback 鏈**：每個 agent 都有 2-5 個 fallback——某 provider 掛了自動換下一個（omo model-fallback hook）。這是「no vendor lock-in」的**韌性價值兌現**：不是哲學，是任一 provider 斷線都不會斷炊。
2. **規劃-執行分離但反 Oversimplify**：不是教條式「Opus plan + GLM execute」二分，而是細分到「規劃用 GLM、推理用 GPT、視覺用 Gemini、搜尋用 mini」——把 INSIGHT-4 推到極致，同時**迴避 §12.3 的 split 反噬**（因為不是二分，而是依任務性質多路分配）。
3. **本 session 就是這份 config 的產物**：Sisyphus 設 `zai-coding-plan/glm-5.2`，所以這個 session 跑在 GLM-5.2 上。

→ **workshop 價值**：這份 config 是「show, don't tell」的鎮館之寶——直接展示給學生看「一個真正在用的多 provider config 長這樣」，比十分鐘講 INSIGHT-4 都有用。完整 config 在 dotfiles repo。

### 5.2 自建 MCP Server（給 agent 真實工具）
- `zed-mcp-server-markitdown`（Rust + Wasm）— 自己寫
- 關注並採用：GhidraMCP、bethington/ghidra-mcp（逆向工程 via MCP）、googleworkspace/cli（內建 AI agent skills）

### 5.3 SKILL.md 模組化工作流
- `ctf-arsenal` 整個 repo 用 `.agents/skills/*/SKILL.md` 結構，把 CTF 拆成 5 個可被 agent 自動發現的技能：pwn-exploits、web-exploits、ics-traffic、crypto-tools、forensics-tools
- 每個 skill 內含：SKILL.md（定義與工作流程）、templates、tools、references
- 關注 microsoft/SkillOpt（自動優化 skill 文本的研究）

### 5.4 Agent-based 資安 / 逆向研究
- fork `VulnClaw`（AI Agent + MCP + 渗透 skill 編排，自然語言 → 資訊收集 → 漏洞發現 → 利用 → 報告）
- 使用者層級已安裝 `ghidra` skill（透過 Ghidra MCP 做逆向、函數分析、符號解析）
- 已安裝 `security-research` / `security-review` skill（Team Mode 漏洞獵人 + PoC 工程師編排）

### 5.5 對 Agent UX / 限制的工程判斷
- 對 Zed 提過「agent: Auto-compact when reaching token limit」PR — 在意 context 管理
- 關注 agent-client-protocol（ACP，連接任何 editor 與任何 agent 的協定）
- 關注 openab（Discord ↔ ACP coding CLI 的 harness）

### 5.6 多層 delegation 編排
- 當前 orchestrator（omo / Sisyphus）本身就用 explore / oracle / librarian / metis / momus 等 subagent 做平行 delegation
- 這套「orchestrator + 平行 subagent + skill 注入」是他 daily 的真實工作模式

### 5.7 日常 Context-Engineering 技巧庫（INSIGHT-1/2 的應用案例）

> 以下都是「改善 input」這根槓桿的具體實作，**不是獨立主題**。理論見 `insight.md` INSIGHT-1（黑盒子 + 兩根槓桿）與 INSIGHT-2（debug 手法）。

| 技巧 | 做什麼 | 為什麼有效 |
|---|---|---|
| **Re-roll（重新 roll）** | 同樣 input 再取樣一次 | 看 output 是穩健還是運氣；探索模型分佈 |
| **改 input + re-roll** | 迭代修改 context 後重跑 | INSIGHT-1 的主迴圈，形塑答案 |
| **Fork chat / 雙 thread A/B** | 把對話 fork 成兩條，各跑不同 input | 受控實驗，isolate 哪個 input 因子有效 |
| **偷看 thinking process** | 讀模型的推理鏈 / thinking tokens | 部分打開黑盒子，看推理是否走偏 |

**兩個長期追求的目標**（同樣是 INSIGHT-1 兩根槓桿的應用）：
- **了解怎麼 input 最有效率** → context engineering 本身
- **了解不同模型效果如何** → 模型選擇（常用：GPT 系列、Gemini 系列）

### 5.8 Agent 時代：多模型 / 多模態編排技巧（INSIGHT-3/4 的應用）

> 進入 Zed agent 時代（2025-05 後）發展出的技巧。底層理論見 `insight.md` INSIGHT-3（agent = loop）與 INSIGHT-4（model composition）。

#### Provider 矩陣（講者在 Zed agent 上實際用過）
codex / Claude / GitHub Copilot / Gemini / DeepSeek / self-host Ollama / Grok / OpenRouter。
- 起點：GitHub Copilot student 用量 = pro 級，於是把上面所有模型都試過。
- 主力：Claude 3.5 → 3.7 → **Claude 4**（隨發布升級）；另自帶 Gemini key 並用。
- **模型篩選 + 實測的三層 workflow**（INSIGHT-2 的精緻版）：① **[Artificial Analysis Intelligence Index](https://artificialanalysis.ai/evaluations/artificial-analysis-intelligence-index)** 當第一層篩——9 個 benchmark 加權綜合（Agent 34% / Coding 24% / 科學 24% / 一般 18%），追蹤 535+ 模型，含 Openness Index；② **OpenRouter** 限免窗口把候選模型丟到**真實工作**上驗證（看實戰，不只看分數）；③ **openness 當硬篩選條件**（必須開源，這也是 GLM 勝出的關鍵）。**不是「不跑 benchmark」，而是「benchmark 只當第一層篩，實戰才驗證」**——這修正了「反 benchmark」的過度簡化。
- **模型評測 routine（兩層互補，refines 上一條）**：
  - **第一層：benchmark landscape**——看 [Artificial Analysis Intelligence Index](https://artificialanalysis.ai)（獨立 LLM benchmark 聚合器，混合品質/速度/價格排名）掌握最新模型版圖，當第一層過濾。
  - **第二層：real work 驗證**——在 OpenRouter 試用各種開源模型，丟到真實工作上看實戰表現。
  - **兩層互補**：benchmarks 知道「什麼存在、大概多強」，real work 才是 ground truth。講者先前「用真實工作測、不跑 benchmark」的反 benchmark 立場，**更精確的說法是「不迷信 benchmark 分數，但用它當起點」**。
- **GLM 偏好的哲學根**：GLM 是當時**最強的開源模型**——**同時滿足「技術最強」與「開源」兩個條件**，這是 Claude（最強但閉源）/ GPT（強但閉源）做不到的組合。對一個有開放生態倫理（§8、INSIGHT-4 道德維度）的講者，GLM 是唯一能在「能力」與「價值」兩軸上都過關的選擇。實測支撐見 cs-special-topics-2 報告（§5.1）：GLM-5.1 SWE-Bench Pro #1、CyberGym 開源 #1。

#### 把外部世界塞進 loop 的技巧
| 技巧 | 做法 | 為什麼 |
|---|---|---|
| **curl webpage** | 在 loop 中 curl 抓網頁內容注入 context | 把「即時外部資訊」變成 input 的一部分 |
| **doc/slide → markdown** | 先把 PDF / 簡報 / pptx 轉成 markdown，再讓 AI 讀 | markdown 比 PDF/圖片更 **AI native**（省 token、結構清楚、模型理解更好）|

> 這第二招的產物就是 `zed-mcp-server-markitdown`（自建 MCP server）與 `ComputerArchitecture_MDnotes`（pptx2md 筆記庫）。`~/school` 資料夾下整票都是這類 workflow。
> **這同時是 INSIGHT-1 的應用**：「改善 input」包括「把 input 改成模型最好消化的格式」。

#### 多模型調度技巧（INSIGHT-4 的三個 pattern，實習時為最大化月用量發展出來）
| Pattern | 做法 | 用在哪 |
|---|---|---|
| **貴規劃 + 便宜實作** | 同 context 先 Claude 3.7 規劃，再切 Gemini 實作（模仿強模型行為）| 在量大的實作階段省 token |
| **長 context 當壓縮機** | Gemini 1M 讀文件庫 → 總結 → 餵 Claude 實作/規劃 | 跨過 Claude 短 context 限制 |
| **多模態當 OCR** | Gemini 讀圖 → 文字 → 餵無多模態模型 | 讓純文字模型也能「看」圖 |

### 5.9 MCP（Model Context Protocol）實戰與設計觀察（INSIGHT-5 的應用）

#### 接觸歷程
- 從 gemini-cli 社群聽到 MCP 被形容為「模型的 USB」，前去了解。
- 本質理解：**MCP = 一個協議，把 local/remote RPC 包成 tool + tool 描述，掛在 agent 的 tool 清單下**，agent 就像 `read`/`write`/`edit`/`bash` 一樣呼叫。沒有魔法。
- Zed 是把 MCP 當 first-class extension 的代表編輯器（MCP as extension，可從擴充商店安裝）；其 MCP 支援普遍被評為同類最強之一（「第一個」難絕對證實，Cursor / Claude Desktop 亦為早期玩家）。

#### 從 Zed MCP 商店調查出的設計典範
調查 Zed MCP 商店高下載量伺服器後（GitHub MCP 單一商店 **91,294 下載**；跨榜單 context7 ~48k stars 排第 4-7、github ~27-30k stars 排第 11-18），歸納出兩種設計典範（詳見 `insight.md` INSIGHT-5）：
- **A. 少量深實作**（context7 類）→ 提升模型智商
- **B. 多量薄實作**（github / postgres MCP 類）→ 讓 LLM 做苦工

講者偏好 A 典範；B 典範的 context 污染與 tool-call 成功率下降可用「強模型示範 → 弱模型模仿」緩解（INSIGHT-4 應用）。**此觀點已實證，硬數據與原始來源見 `references.md` §4**（關鍵：tool-selection 準確率 43%→2% @ 4→51 工具；Anthropic 30-50 工具衰退門檻）。

#### 自建 MCP：`zed-mcp-server-markitdown`（A 典範實作）
- **動機**：Microsoft MarkItDown 釋出後，發現沒人幫 Zed 寫 wrapper，於是動手寫。
- **性質**：Rust + Wasm；單一工具，把「PDF / doc / slide → markdown」的複雜度在內部消耗，只回吐乾淨 markdown 給模型——典型 A 典範。
- **成績**：Zed 擴充商店 **29,963 下載**（截至 2026-07；v0.0.1，2025-09-25 上架）；GitHub 24 stars、4 forks。
- **意義**：「看到缺口 → 自己補上 → 真實被近 3 萬人採用」的完整 OSS 閉環，也是 workshop 裡「學生也能做出被大量使用的 MCP」的最佳激勵案例。

### 5.10 環境分工：web chatbot 批量搜尋 ↔ local agent（INSIGHT-6 的應用）

講者雖主力是 local agent，仍持續使用 web chatbot——但只用其**批量網路搜尋**能力：

| 環境 | 比較利益 | 講者用法 |
|---|---|---|
| **Web chatbot**（Perplexity、Gemini deep research）| 背景批量搜尋數十～上百網頁 | 跑研究題、收集資料 |
| **Local agent**（Zed / opencode）| 完整存取 local codebase / context | 接收 deep research 的 markdown 結果，繼續加工、寫程式 |

**routine**：web chatbot 跑 deep research → 把 markdown 結果回貼 local agent 注入 context。
**意義**：text/markdown 兩邊都能消化，「批量搜尋」這件 local agent 做不好的事，外包給專門環境後再回收。理論見 `insight.md` INSIGHT-6。

### 5.11 自建 context 語料庫（INSIGHT-7 的應用）—「手搓 NotebookLM / RAG」

針對實習 + 同時修課的負荷，講者為**每門課**發展出一套 context 構造 routine：

```
拉課程檔案 → 全部轉 markdown → 整理成獨立 git repo（note repo）
       → 在該 repo 內問 agent（agent 自動以整門課為 context）
       → 把該目錄當作業/專題的 submodule（作業一開工即繼承整門課背景）
```

#### 實證：`~/School` 目錄結構（已檢查，2026-07-01）
- `~/School/README.md`：完整命名規範（kebab-case + 學科前綴 cs/me/math/it/ai/ee/fin/mm）、NTNU/NTU 分校、同名課加學校後綴。
- 兩大分類：`ntnu/`（11+ 課）與 `ntu/`（12+ 課），跨資工/機電/數學/電機/財金/多媒體。
- 每門課一個目錄內含獨立 git repo；作業通常再拆成獨立 repo（如 `ntu-2025fall-advanced-compiler-hw1-G36maid`）。

#### context 架構三件套（已在 `~/School` 驗證）
| 組件 | 角色 | 實例 |
|---|---|---|
| **note repo**（語料庫）| 該課完整 markdown 知識庫 | `ntu-2025fall-advanced-compiler-note`：含 `course-materials/`、`notes/`、`exam/`、`experiment/`；檔案 20 md + 9 pptx + 5 pdf（以 markdown 為主，原檔保留）|
| **work repo**（作業/專題）| 實際產出，引用語料庫與上游 | `...-hw1-G36maid` 以 submodule 拉 Cornell `bril`；`cs-computer-graphics` 以 submodule 拉 4 個作業 repo |
| **AGENTS.md** | agent 操作手冊，每個 repo 都有 | 全 `~/School` **15+ 處** AGENTS.md |

#### 意義
- 講者自況：**「手搓出類似 NotebookLM 或 RAG 的能力」**，但版本控管、可組合（submodule）、可攜（純 markdown）、完全自控——比 NotebookLM 更強。
- 把「問 AI」升級成「**建一個讓 agent 住進去的知識庫**」。
- 其中 AGENTS.md 不只是講者個人習慣，是**業界事實標準**（30+ agents 採用、Linux Foundation 治理）——見 `insight.md` INSIGHT-8 與 `references.md` §6。講者自 Zed 支援後幾乎每 repo 都先建。
- 理論見 `insight.md` INSIGHT-7；**至今最適合直接轉移給學生的 workflow**（不需進階環境、不需付費 API、立即改善課業）。

### 5.12 資訊來源 / 資訊飲食（為何有 insight）

講者的 insight 不憑空而來，來自**直接消費英文初級來源**：

| 來源 | 實際內容（已查證 2026-07-01）| 對應講者哪塊 |
|---|---|---|
| **ThePrimeagen**（主頻道）+ **The PrimeTime**（Twitch 剪輯/反應）+ TheVimeagen | ex-Netflix；Neovim/Lua 狂熱（"I am done with vim" → Neovim forever）；i3/tmux/vim 工作流實戰。**註**：原描述提「AI 趨勢」實為次要，主軸是開發生產力與 Vim 文化 | Vim/CLI/tmux 工作流 |
| **Low Level**（UC6biysICWOJ-C3P4Tyeggzg）| **已確認 = 專做 exploit / vulnerability 的資安頻道**（非 "Low Level Learning"）。實例：copy.fail Linux 全 distro LPE、AppArmor LPE、ISP 0-day（1.2M views）、UEFI Ring -2、M1 cache 漏洞 | Linux kernel CVE / CTF — 完全對齊 |
| **Tsoding** | 硬派 C/C++ 從零實作（如 "Insane Shadow Data Trick in C"：stb_ds.h、dynamic array、macro、realloc，21 分鐘深論）| 底層實作細節 |
| **Fireship** | "X in 100 Seconds" 系列 + 快節奏生態評論（如 "Big projects are ditching TypeScript"，3:38 / 1.6M views）。涵蓋語言、框架、AI 工具 | 快速吸收技術新知與生態動態 |
| **Linus Tech Tips / LTTClips** | PC 硬體評測、科技產品（LTTClips 為剪輯頻道）| homelab（Proxmox/TrueNAS）、Framework Laptop 調校 |
| **Theo - t3․gg** | **TypeScript / web / JS 框架生態**為主（t3 stack 創造者），如 "The Future of TypeScript"（30 分鐘論 TypeScript Go port）。**註**：原描述「軟體架構」略過廣，主軸是 web 生態與業界轉變 | 系統層以外的 web/JS 工程視野 |
| X / Twitter 開發者討論 | 即時業界辯論、踩坑 | 第一手趨勢 |
| GitHub issues / discussions | 真實工程討論、維護者設計取捨 | 工具實際設計取捨（AGENTS.md gotcha 多從此而來）|

> **查證備註**：上表為實際內容查證，非僅 Gemini 從觀看歷史撈的描述。兩處原描述略過廣已修正（ThePrimeagen 的「AI 趨勢」實為次要；Theo 的「軟體架構」實為 TypeScript/web 生態）。「Low Level」並已與同名易混淆的 "Low Level Learning" 區分開。

**關鍵觀察（講者陳述）**：繁中 AI 社群大量內容**只是搬運，或只講工具用法，根本沒有 insight**。講者的優勢正是跨過語言牆直接吸收初級來源。這同時是 workshop 的定位錨點（見 §8）與 `insight.md` INSIGHT-9 的來源。

### 5.13 ACP / agent 協定生態的追蹤

講者 starred `agentclientprotocol/agent-client-protocol`（3.5K stars）與 `openab/openab`（Discord ↔ ACP coding CLI 的 harness）。ACP = **Zed 創造的「editor ↔ agent」開放協定**（2025-08-27，Gemini CLI 為首個整合；2025-10 JetBrains 加入），與 MCP（agent ↔ tools）**互補不競爭**。完整誕生脈絡、與 Zed 關係、LSP/ACP/MCP/A2A 生態全景見 `references.md` §8。

**意義**：ACP 是「editor 側的開放標準」，與 opencode（no vendor lock-in）、AGENTS.md（INSIGHT-8）同屬「**agent 生態在每個邊界走向 open protocol**」這股力量。講者追蹤此生態 = 持續把脈 agent 工具鏈的開放化走向。生態亮點：**已有 GLM 驅動的 ACP agent**（Zhipu AI glm-5.1）——呼應本 session 跑在 GLM 上。

---

## 6. AI 工具演化的第一手見證（脈絡）

> 講者作為 Zed 重度使用者 + Guild Contributor，是「看著 coding agent 從無到有」的一線見證者。
> 這段親身經歷本身就是 workshop 最佳的「概念發展史」教材——因為現在的學生一進場就是 agent 時代，不懂之前為什麼這樣設計。

### 6.1 時間軸（已查證）

| 時間 | 事件 | 對講者的意義 |
|---|---|---|
| 2023-06-28 | Zed 0.92「Introducing the assistant panel」——最早的 conversation editor，OpenAI API key，**text thread 概念誕生** | 講者接觸 AI coding 的起點形式 |
| 2024-03-04 | Claude 3 Opus / Sonnet / Haiku 發布 | 「最好的模型」開始洗牌 |
| 2024-06-20 | **Claude 3.5 Sonnet** 發布——coding 能力跨代提升，業界公認的分水嶺 | 真正「能寫程式」的 LLM 出現 |
| 2024-08-20 | Zed「Introducing Zed AI」——hosted service、綁 Claude 3.5 Sonnet、assistant panel + inline transformation + `/workflow`、Prompt Caching | Zed 正式 all-in AI；講者貢獻與使用重疊期 |
| 2024-10-22 | Claude 3.5 Sonnet v2 + Computer Use（公開 beta）| agent 能「看螢幕」的開端 |
| 2025-02 上旬 | Andrej Karpathy 提出 **"vibe coding"** 一詞 | 講者「嗤之以鼻」的對象正式被命名 |
| 2025-02-24 | **Claude 3.7 Sonnet**（首個 hybrid reasoning）+ **Claude Code CLI** 發布 | agentic coding 正式成為正規軍 |
| 2025-03-25 / 06-17 | Gemini 2.5 Pro（experimental → stable GA）| 多模型競爭格局成形 |
| 2025-05 | Zed 引入 **Agent Panel**（agentic workflows），text thread 退居 legacy 模式 | 講者見證典範轉移：stateless 共編 → stateful agent |
| 2025-05-22 | Claude Sonnet 4 + Opus 4 發布 | 講者隨發布升級的主力模型 |
| 2025-06-25 | Google **gemini-cli** 開源（Apache 2.0）— Zed agent 的同期同儕 | agent 工具生態多元化；講者記憶中「同期只有 gemini-cli 跟各種 fork」即指此 |
| 2025-08-19 | **AGENTS.md** spec repo 建立（Sourcegraph Amp 發起，OpenAI/Google/Cursor/Factory 聯合）| agent instruction 開放標準起點；講者後續幾乎每 repo 都建的依據 |
| 2025-09-25 | 講者的 `mcp-server-markitdown` 上架 Zed 擴充商店（A 典範 MCP 實作）| 講者首個被大量採用的 MCP 作品（截至 2026-07 達 29,963 下載）|
| 2025-12 | AGENTS.md **捐贈 Linux Foundation（AAIF）** | 業界事實標準化；不綁任一廠商 |
| 2026-04 (v0.231.1) | Zed **移除 legacy text thread** | 一個時代結束 |

> 講者記憶壓縮的時間窗：**約 2023 中 → 2025 中**。這段是「web chatbot 剪貼 → text thread 共編 → agent 自主」的三段演化。當時主流還是 Cursor + web chatbot 剪下貼上，VSCode side chat 等級。

### 6.2 Text Thread 經驗（講者第一個「真正懂 context」的契機）

- **形式本質**：跟 AI 共同編輯一個檔案。可注入 selected file / codeblock / selected text / 自己打的字；LLM 結果接在下面。
- **因為同時是貢獻者 + 使用者**，提早理解了「上下文（context）」這個概念——而這是「剪下貼上 web chatbot」派永遠學不到的。
- **關鍵 trick**：直接編輯 thread 的歷史訊息（包含 AI 的舊回覆）來修正錯誤 / 幻覺 / 方向偏差，而不必開新對話或花 token 修正。把整個對話當成 **mutable document**。

### 6.3 對 workshop 的啟示（第一個浮現的教材級 insight）

講者親身走過 **stateless text-thread（你看見並控制整個 request）→ stateful agent（細節被隱藏）** 的演化。
而**現在的學生一入場就是 agent 時代**，從沒看見「context 長什麼樣」。

→ 這代表 **text-thread 模式可能是理解 agent 最有效的教學起點**：先讓學生看到「一次 LLM 呼叫 = 一段文字 = 你能編輯的歷史」，再過渡到「agent 把這件事自動化並加上 tool call」。**講者內化的心智模型，正好是學生缺的那塊。**

---

## 7. 待補充區塊（已 close，2026-07-01）

> 講者表示對 AI agent 的 insight 已全部說完。原本三項質性欄位的實際內容如下：

- [~] **日常實際用 AI 做哪些事** — partially：已知實習 coding、**課程學習/複習（§5.11，大宗）**、學習文件處理、CTF、研究（§5.10）；講者不再補精確比例。
- [x] **最有感的幾個自創 workflow** ✅ 已記多個（見 §5.7、§5.8、§5.11、§6.2）。
- [x] **絕不交給 AI 的部分** → **reframed**：講者沒給「禁止交給 AI 的清單」，而是給了四個**工程紀律判斷**（TDD 適合 agent / human-in-loop 看場合 / LSP 有時是噪音 / git 是聖旨不信 tool revert）——這四個其實是「**AI 不位移工程責任，只改變施力點**」的切面，已收成 `insight.md` **INSIGHT-10**。
- [x] **教授 demo 的「哇」瞬間** → **不是功能 demo，是對比本身**：教授看到其他學生還在用 web chatbot 剪下貼上，對比講者的實際場景，那個 gap 就是 wow。**沒有單一炫技瞬間要保留**——workshop 的核心不是重現某個 demo，而是**把那個 gap 關起來**（web chatbot → 真正 agent workflow）。這跟 INSIGHT-9 / §8 的價值主張完全一致。
- [x] **失敗經驗 / 踩過的坑** → 講者沒特別強調。**proxy**：被 Google Antigravity ban（§5.1）+ Summer Yue 類型事件（`references.md` §13.4）+ opencode 與 Anthropic/Google 鬧翻（§10）已覆蓋大部分「坑」的教材價值。

---

## 8. 給 workshop 設計的初步觀察（先記下，之後再論證）

- **可教的概念（工具鏈中立的）**：decomposition、skill 模組化、MCP 給 agent 工具、verification 心態、context 管理、平行 delegation
- **難轉移的工具鏈（要找替代或降門檻）**：Arch + tmux + terminal、自架 homelab、付費 API quota、opencode/omo 本身（安裝有門檻）
- **核心張力**：講者 setup 高度個人化且進階；受眾大概率落差很大。workshop 成敗取決於「概念 vs 工具」的切線畫在哪。
- **workshop 的核心價值主張 = 提供繁中社群缺的 insight 層**：不是教工具用法（那是搬運層在做），而是教「為什麼這樣用」的心智模型（INSIGHT-1~8）。源自講者的英文初級來源資訊飲食（見 §5.12、`insight.md` INSIGHT-9）——這是講者相對於繁中 AI 內容圈的獨特資產。
- **workshop 本質 = 關閉「教授看到的 gap」**：那個讓教授「哇」的對比（學生還在 web chatbot vs 講者的真實 agent workflow）就是 workshop 要消除的距離。所以 workshop 的北極星不是「教幾個工具」，而是**讓學生從 web-chatbot 心智模型遷移到 agent 心智模型**——INSIGHT-1~3（祛魅層）正是這個遷移的起點。
- **講者的開放 vs 封閉倫理立場（workshop 定位考量）**：講者因親身被 Google ban（§5.1）+ 見證 Anthropic 跨標準封閉實踐（見 `references.md` §11），對「封閉 vendor」有明確倫理反感，與大量推特開發者共鳴。這讓 workshop 帶有價值選擇色彩——**好處**是真誠、有立場；**風險**是可能變成反 Anthropic 宣傳。設計時需平衡：誠實承認 Claude 模型最強、MCP 是真貢獻，同時指出封閉實踐風險。講者「no vendor lock-in」（INSIGHT-4）因此有道德維度，不只是技術偏好。
