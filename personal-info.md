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
- **OpenRouter 作為模型發現 + 實測渠道**：OpenRouter 常最早架上各家最新模型，部分 lab 模型上架時有限時免費。講者會利用這些限免窗口，把新模型丟到**真實工作**上測實力（不是跑 benchmark，是看實戰表現）——這是 INSIGHT-2（把 LLM 當系統實測）與 INSIGHT-4（模型選擇）的日常實踐。

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

## 7. 待補充區塊

> 講者表示會持續補充與 AI 相關的內容。以下欄位等講者補完再填：

- [ ] **日常實際用 AI 做哪些事**（coding / 讀 paper / 寫作 / debug / 實驗設計 / 文獻整理 的比例）— partially：已知實習 coding、**課程學習/複習（§5.11，大宗）**、學習文件處理、CTF、研究（§5.10）；仍缺精確比例
- [x] **最有感的幾個自創 workflow** ✅ 已記多個：text-thread 編輯歷史（§6.2）／ re-roll·改 input·fork A/B·偷看 thinking（§5.7）／ curl + doc→markdown·多模型三招（§5.8）
- [ ] **絕不交給 AI 的部分**（與其原因）
- [ ] **跟教授 demo 時，讓教授「哇」的那個瞬間**（workshop 最該保留的核心場景）
- [ ] **失敗經驗 / 踩過的坑**（避免學生重蹈）

---

## 8. 給 workshop 設計的初步觀察（先記下，之後再論證）

- **可教的概念（工具鏈中立的）**：decomposition、skill 模組化、MCP 給 agent 工具、verification 心態、context 管理、平行 delegation
- **難轉移的工具鏈（要找替代或降門檻）**：Arch + tmux + terminal、自架 homelab、付費 API quota、opencode/omo 本身（安裝有門檻）
- **核心張力**：講者 setup 高度個人化且進階；受眾大概率落差很大。workshop 成敗取決於「概念 vs 工具」的切線畫在哪。
