# AI Workshop 籌備筆記

> 目標：教實驗室大學生 / 碩士生「如何最大化使用 AI agent 輔助開發與研究」
> 講者：G36maid（NTNU CS / ME）
> 形式：整天 workshop，早上 9 點到下午，估 3~6 小時

---

## 設計立場

**演講者驅動，不最佳化受眾。** 講者立場明確：「我想講我想講的」。不為聽眾落差（中學生 ~ Claude Max token-maxxing 朋友，5x 落差）做分層服務，也不糾結 hands-on vs concept 的 fork。

- 北極星：帶聽眾從 web-chatbot 心智模型遷移到 agent 心智模型（見 `insight.md`）
- 骨架：10 條 INSIGHT（祛魅 → 構造 input → 組合 → meta 資訊飲食 → 工程紀律）
- 6 小時場唯一真正的死法是講者自己倦怠 → **讓講者最有火的 insight 拿最多時間**
- 聽眾各自吸收到他能吸收的層，那是他們的事

---

## 1. Token 來源

### opencode Go（主推）

**為什麼適合 workshop**：低門檻、14 個強開源模型一把抓、額度對一整天的 workshop 綽綽有餘、零資料留存、不鎖 opencode TUI（可接任何 agent）。

**費用**（截至 2026-06-30，source: opencode.ai/docs/go/、opencode.ai/go）：

| 項目 | 內容 |
|---|---|
| 月費 | **$5 首月**，之後 **$10/月** |
| 等同用量價值 | **$60/月**（6x leverage）|
| 5 小時上限 | $12 等同用量 |
| 週上限 | $30 等同用量 |
| 月上限 | $60 等同用量 |
| 伺服器節點 | US / EU / Singapore |
| 資料政策 | **zero data retention** |
| 取消政策 | 隨時取消；額度不夠可加值 |

**收錄模型（14 個）**：

| 模型 | 定位 | 備註 |
|---|---|---|
| **GLM-5.2** | 講者日常 driver | 講者用這個跑此 session |
| GLM-5.1 | Opus-level 開源 | Hades 專題用 |
| Kimi K2.7 Code | 程式特化 | |
| Kimi K2.6 | Moonshot 旗艦 | |
| MiMo-V2.5 / V2.5-Pro | 小米 | V2.5 最便宜 |
| MiniMax M3 / M2.7 | agentic 工作馬 | |
| Qwen3.7 Max / Plus | Alibaba 高階 | |
| Qwen3.6 Plus | 上一代 | |
| DeepSeek V4 Pro | 長 context 強 | |
| DeepSeek V4 Flash | 快又便宜 | 高 throughput |

**對 workshop 的實際意義**：
- 學生花 **$5**（首月）就有一整天的 agent 體驗額度，5 小時 $12 window 對單一 session block 綽綽有餘（DeepSeek V4 Flash 可撐 31,650 requests/5h）
- 不強制 opencode TUI：學生若已在用 Cursor / Claude Code / 任何相容 agent，都可接 Go 的 API endpoint
- 開源模型為主 → 跟講者 INSIGHT-4（no vendor lock-in）哲學一致
- **caveat**：「Only one member per workspace can subscribe」——如果實驗室共用 workspace 要注意，但每人各自註冊帳號就沒問題

### BYOK（Bring Your Own Key）

學生若已有 API key（Claude / Gemini / OpenAI / 自架 OpenRouter 等），可選擇用自己的。但講者**主推 Go**，理由：
- 統一管道降低現場排除難度的負擔（一人一種 provider 的 debug 會吃掉 workshop 時間）
- 開源模型陣容正好對齊講者價值主張
- 對完全沒接觸過 API key 的學生，Go 的訂閱流程比各家 console 直覺

---

## 2. 場次結構

### 上半場（早上）：pure opencode

整個早上 session **在 opencode TUI 裡面跑**。講者日常 driver 場景，即興 demo，不切換到其他工具。

**這個選擇隱含的覆蓋範圍**（推論，待講者確認）：
- **祛魅層**（INSIGHT-1~3）：agent = loop 直接 live 演出，不用投影片解釋
- **構造 input 層**（INSIGHT-5/7/8）：MCP、AGENTS.md、自建 context 語料庫——全部是 opencode 原生概念，邊做邊講
- **鎮館之寶登場**：講者的 live config（4 provider 混合 + fallback 鏈）在這裡 show 出來

#### 早上課程骨架（講者初步想法，順序如列）

| # | 段落 | 推測內容 | 待澄清 |
|---|---|---|---|
| 1 | **自我介紹** | 講者是誰、為什麼有資格講、peer 定位（不是權威是同儕走更遠）| — |
| 2 | **知識環節** | ??? 可能是祛魅層（INSIGHT-1~3：LLM/agent 到底是什麼）| 與 #3「關鍵說明」、#5「insight 分享」的邊界? |
| 3 | **關鍵說明** | ??? 可能是北極星 framing / 心智模型遷移 / 今天要帶走什麼 | 具體是什麼的「關鍵」? |
| 4 | **環境配置** | opencode 安裝 + Go 訂閱 + pure Go config 套用 | 學生實機操作 or 講者 demo only? 時間風險? |
| 5 | **講古與趣事 / insight 分享** | INSIGHT-1~10 用故事、親身經歷、歷史脈絡講 | 與 #2「知識環節」內容重疊風險? |

### 下半場（下午）：omo（條件性）

**候選內容**：介紹 omo（oh-my-openagent，講者日常 orchestrator 哲學的實作）。

**調度規則**：如果上半場 opencode 講不完，omo 順延到下午。上半場優先級高於 omo。

---

## 3. 學生用 config（pure Go）

### 為什麼需要

講者日常 config 是 **4 provider 混合**（zai-coding-plan / opencode-go / openai / google），會路由到**昂貴 frontier 模型**（GPT / Gemini 等級，output 可達 $15~$30/1M tokens）。學生如果在 workshop 現場燒這種等級的 token，是「token burner 有機會燒乾」——金額不可控。

**Pure Go config 的作用 = cost safety boundary**：
- 只路由到 opencode-go provider（14 個開源模型）
- 無論學生怎麼 hammer，最大燒掉就是 Go 額度（$12/5h、$30/週、$60/月）
- 對應 $5 首月訂閱，整個 workshop 下來成本可預測、可負擔

### Status：待產出

**To-do**：以講者主 config（`~/Code/Github/dotfiles/opencode/.config/opencode/oh-my-openagent.json`）為 template，產出一份**只保留 opencode-go provider** 的精簡版，供學生 workShop 現場使用。

設計決策待講者拍板（建議方向）：
- 預設 driver model（候選：GLM-5.2 / DeepSeek V4 Pro / MiniMax M2.7）
- 是否做 planner-executor split（如 GLM-5.2 plan + MiniMax M2.7 execute，兩個都是 Go 模型）
- 帶哪些 MCP server（只保留 demo 必要的）
- AGENTS.md 要帶還是讓學生自己寫

---

## （後續章節待補）
