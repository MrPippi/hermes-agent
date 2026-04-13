<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

# Hermes Agent ☤

<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/Docs-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="文件"></a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="授權條款：MIT"></a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/Built%20by-Nous%20Research-blueviolet?style=for-the-badge" alt="由 Nous Research 開發"></a>
</p>

**由 [Nous Research](https://nousresearch.com) 打造的自我進化 AI 代理。** 這是唯一內建學習迴路的代理——它從經驗中創造技能、在使用過程中持續改進、主動提醒自己保存知識、搜尋自己的歷史對話，並在每次會話中不斷深化對你的了解。可部署於 5 美元的 VPS、GPU 叢集，或幾乎閒置時零成本的無伺服器基礎設施。不受限於你的筆電——在 Telegram 上與它溝通，同時讓它在雲端 VM 上處理任務。

使用任何你想要的模型——[Nous Portal](https://portal.nousresearch.com)、[OpenRouter](https://openrouter.ai)（200+ 個模型）、[z.ai/GLM](https://z.ai)、[Kimi/Moonshot](https://platform.moonshot.ai)、[MiniMax](https://www.minimax.io)、OpenAI，或你自己的端點。透過 `hermes model` 切換——無需修改程式碼，沒有供應商鎖定。

<table>
<tr><td><b>真正的終端介面</b></td><td>完整的 TUI，支援多行編輯、斜線指令自動完成、對話歷史記錄、中斷重導向，以及串流工具輸出。</td></tr>
<tr><td><b>與你同在</b></td><td>Telegram、Discord、Slack、WhatsApp、Signal 與 CLI——全部透過單一閘道程序運作。支援語音備忘錄轉錄與跨平台對話連續性。</td></tr>
<tr><td><b>閉環學習迴路</b></td><td>代理自主管理的記憶，配合定期提示。完成複雜任務後自動創建技能。技能在使用中持續自我改進。FTS5 會話搜尋配合 LLM 摘要，實現跨會話回憶。<a href="https://github.com/plastic-labs/honcho">Honcho</a> 辯證式使用者建模。與 <a href="https://agentskills.io">agentskills.io</a> 開放標準相容。</td></tr>
<tr><td><b>排程自動化</b></td><td>內建 cron 排程器，可傳送至任何平台。每日報告、夜間備份、每週審計——全部以自然語言設定，無需人工看管。</td></tr>
<tr><td><b>委派與並行處理</b></td><td>生成隔離的子代理以進行並行工作流。撰寫透過 RPC 呼叫工具的 Python 腳本，將多步驟流程壓縮為零上下文成本的回合。</td></tr>
<tr><td><b>在任何地方運行，不只是你的筆電</b></td><td>六種終端後端——本地、Docker、SSH、Daytona、Singularity 與 Modal。Daytona 和 Modal 提供無伺服器持久化——代理環境在閒置時進入休眠，按需喚醒，會話之間幾乎零成本。可在 5 美元的 VPS 或 GPU 叢集上運行。</td></tr>
<tr><td><b>研究就緒</b></td><td>批次軌跡生成、Atropos RL 環境、軌跡壓縮，用於訓練下一代工具呼叫模型。</td></tr>
</table>

---

## 快速安裝

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

適用於 Linux、macOS、WSL2，以及透過 Termux 的 Android。安裝程式會自動處理各平台的設定。

> **Android / Termux：** 已測試的手動安裝步驟記錄於 [Termux 指南](https://hermes-agent.nousresearch.com/docs/getting-started/termux)。在 Termux 上，Hermes 會安裝精選的 `.[termux]` 附加套件，因為完整的 `.[all]` 附加套件目前會引入 Android 不相容的語音依賴項。
>
> **Windows：** 不支援原生 Windows。請安裝 [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) 後再執行上述指令。

安裝完成後：

```bash
source ~/.bashrc    # reload shell (or: source ~/.zshrc)
hermes              # start chatting!
```

---

## 開始使用

```bash
hermes              # Interactive CLI — start a conversation
hermes model        # Choose your LLM provider and model
hermes tools        # Configure which tools are enabled
hermes config set   # Set individual config values
hermes gateway      # Start the messaging gateway (Telegram, Discord, etc.)
hermes setup        # Run the full setup wizard (configures everything at once)
hermes claw migrate # Migrate from OpenClaw (if coming from OpenClaw)
hermes update       # Update to the latest version
hermes doctor       # Diagnose any issues
```

📖 **[完整文件 →](https://hermes-agent.nousresearch.com/docs/)**

## CLI 與訊息平台快速參考

Hermes 有兩個入口：使用 `hermes` 啟動終端介面，或執行閘道並透過 Telegram、Discord、Slack、WhatsApp、Signal 或 Email 與其對話。進入對話後，許多斜線指令在兩種介面間通用。

| 操作 | CLI | 訊息平台 |
|---------|-----|---------------------|
| 開始聊天 | `hermes` | 執行 `hermes gateway setup` + `hermes gateway start`，然後向機器人發送訊息 |
| 開始新對話 | `/new` 或 `/reset` | `/new` 或 `/reset` |
| 更換模型 | `/model [provider:model]` | `/model [provider:model]` |
| 設定個性 | `/personality [name]` | `/personality [name]` |
| 重試或撤銷上一回合 | `/retry`、`/undo` | `/retry`、`/undo` |
| 壓縮上下文 / 查看用量 | `/compress`、`/usage`、`/insights [--days N]` | `/compress`、`/usage`、`/insights [days]` |
| 瀏覽技能 | `/skills` 或 `/<skill-name>` | `/skills` 或 `/<skill-name>` |
| 中斷目前工作 | `Ctrl+C` 或發送新訊息 | `/stop` 或發送新訊息 |
| 平台特定狀態 | `/platforms` | `/status`、`/sethome` |

完整指令列表請參閱 [CLI 指南](https://hermes-agent.nousresearch.com/docs/user-guide/cli) 與 [訊息閘道指南](https://hermes-agent.nousresearch.com/docs/user-guide/messaging)。

---

## 文件

所有文件均位於 **[hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)**：

| 章節 | 涵蓋內容 |
|---------|---------------|
| [快速入門](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart) | 安裝 → 設定 → 2 分鐘內完成第一次對話 |
| [CLI 使用](https://hermes-agent.nousresearch.com/docs/user-guide/cli) | 指令、快捷鍵、個性設定、會話管理 |
| [設定](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) | 設定檔、服務提供者、模型、所有選項 |
| [訊息閘道](https://hermes-agent.nousresearch.com/docs/user-guide/messaging) | Telegram、Discord、Slack、WhatsApp、Signal、Home Assistant |
| [安全性](https://hermes-agent.nousresearch.com/docs/user-guide/security) | 指令審批、私訊配對、容器隔離 |
| [工具與工具集](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools) | 40+ 種工具、工具集系統、終端後端 |
| [技能系統](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) | 程序性記憶、技能中心、建立技能 |
| [記憶](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory) | 持久記憶、使用者檔案、最佳實踐 |
| [MCP 整合](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp) | 連接任何 MCP 伺服器以擴充功能 |
| [Cron 排程](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron) | 排程任務並傳送至指定平台 |
| [情境檔案](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files) | 塑造每次對話的專案情境 |
| [架構](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture) | 專案結構、代理迴路、核心類別 |
| [貢獻](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) | 開發環境設定、PR 流程、程式碼風格 |
| [CLI 參考](https://hermes-agent.nousresearch.com/docs/reference/cli-commands) | 所有指令與旗標 |
| [環境變數](https://hermes-agent.nousresearch.com/docs/reference/environment-variables) | 完整環境變數參考 |

---

## 從 OpenClaw 遷移

若您來自 OpenClaw，Hermes 可自動匯入您的設定、記憶、技能與 API 金鑰。

**首次設定時：** 設定精靈（`hermes setup`）會自動偵測 `~/.openclaw`，並在開始設定前提供遷移選項。

**安裝後隨時可執行：**

```bash
hermes claw migrate              # Interactive migration (full preset)
hermes claw migrate --dry-run    # Preview what would be migrated
hermes claw migrate --preset user-data   # Migrate without secrets
hermes claw migrate --overwrite  # Overwrite existing conflicts
```

匯入內容：
- **SOUL.md** — 人格檔案
- **記憶** — MEMORY.md 與 USER.md 項目
- **技能** — 使用者創建的技能 → `~/.hermes/skills/openclaw-imports/`
- **指令允許清單** — 審批規則
- **訊息設定** — 平台設定、允許的使用者、工作目錄
- **API 金鑰** — 允許清單中的密鑰（Telegram、OpenRouter、OpenAI、Anthropic、ElevenLabs）
- **TTS 資源** — 工作區音訊檔案
- **工作區說明** — AGENTS.md（配合 `--workspace-target`）

執行 `hermes claw migrate --help` 查看所有選項，或使用 `openclaw-migration` 技能進行互動式代理引導遷移，並支援預覽模式。

---

## 貢獻

歡迎貢獻！請參閱 [貢獻指南](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) 了解開發環境設定、程式碼風格與 PR 流程。

貢獻者快速入門：

```bash
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent
curl -LsSf https://astral.sh/uv/install.sh | sh
uv venv venv --python 3.11
source venv/bin/activate
uv pip install -e ".[all,dev]"
python -m pytest tests/ -q
```

> **RL 訓練（選用）：** 若要參與 RL/Tinker-Atropos 整合開發：
> ```bash
> git submodule update --init tinker-atropos
> uv pip install -e "./tinker-atropos"
> ```

---

## 社群

- 💬 [Discord](https://discord.gg/NousResearch)
- 📚 [技能中心](https://agentskills.io)
- 🐛 [問題回報](https://github.com/NousResearch/hermes-agent/issues)
- 💡 [討論區](https://github.com/NousResearch/hermes-agent/discussions)
- 🔌 [HermesClaw](https://github.com/AaronWong1999/hermesclaw) — 社群 WeChat 橋接：在同一個 WeChat 帳號上同時運行 Hermes Agent 與 OpenClaw。

---

## 授權條款

MIT — 請參閱 [LICENSE](LICENSE)。

由 [Nous Research](https://nousresearch.com) 開發。
