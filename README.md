桌面端运行界面
<img width="2459" height="1612" alt="f1ca881015cc72892fdb3964cd4bc675" src="https://github.com/user-attachments/assets/f8284233-85ce-423e-a7ee-ef5e45b9a4de" />
<img width="2433" height="1585" alt="image" src="https://github.com/user-attachments/assets/16d99e4b-1bf4-40f8-bf82-e20e31cee1ce" />


# Hermes Agent — Desktop Development Environment

> **Course Project** — Full-stack development environment for the Hermes Agent desktop application, including the Electron shell, Python AI agent backend, TUI, and messaging gateway.

[![Electron](https://img.shields.io/badge/Electron-39.8.10-47848F?logo=electron)](https://electronjs.org)
[![Python](https://img.shields.io/badge/Python-3.11.9-3776AB?logo=python)](https://python.org)
[![Node.js](https://img.shields.io/badge/Node.js-24.16.0-339933?logo=node.js)](https://nodejs.org)
[![React](https://img.shields.io/badge/React-19.2.5-61DAFB?logo=react)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.0.3-3178C6?logo=typescript)](https://typescriptlang.org)
[![Vite](https://img.shields.io/badge/Vite-8.1.0-646CFF?logo=vite)](https://vitejs.dev)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the App](#running-the-app)
- [Building the Desktop App](#building-the-desktop-app)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Development Notes](#development-notes)
- [License](#license)

---

## Overview

This repository contains a complete **Hermes Agent Desktop** development environment. Hermes Agent is an open-source, self-improving AI agent built by [Nous Research](https://nousresearch.com). It features a built-in learning loop, cross-platform desktop application, terminal UI, and messaging gateway supporting 20+ platforms.

### What's Inside

| Component | Description |
|-----------|-------------|
| **Electron Desktop App** | Native Windows/macOS/Linux GUI with React 19 renderer |
| **Python AI Backend** | Agent core with conversation loop, tool orchestration, memory |
| **TUI (Terminal UI)** | Ink/React-based terminal interface via `hermes --tui` |
| **Messaging Gateway** | Multi-platform support (Telegram, Discord, Slack, etc.) |
| **Plugin System** | Extensible memory providers, model providers, tools |

---

## Features

- **Electron Desktop GUI** — Streaming chat, file browser, side-by-side previews, voice I/O
- **AI Agent Core** — Tool-calling loop, subagent delegation, skill creation/improvement
- **80+ Built-in Tools** — Terminal, file operations, web search, browser automation, MCP
- **Multi-Provider Support** — OpenAI, Anthropic, OpenRouter, SiliconFlow, custom endpoints
- **Persistent Memory** — Cross-session learning with pluggable memory backends
- **Cron Scheduler** — Natural-language scheduled tasks with multi-platform delivery
- **Plugin Architecture** — Custom tools, model providers, memory backends via plugins
- **Portable Runtime** — Self-contained `workspace/` with `run.ps1` / `run.sh` launchers

---

## Tech Stack

### Frontend (Desktop App)
| Technology | Version | Purpose |
|------------|---------|---------|
| Electron | 39.8.10 | Desktop shell |
| React | 19.2.5 | UI framework |
| TypeScript | 6.0.3 | Type-safe development |
| Vite | 8.1.0 | Build tooling |
| Tailwind CSS | 4.2.4 | Styling |
| nanostores | 1.3.0 | State management |
| xterm.js | 6.0.0 | Embedded terminal |
| node-pty | 1.1.0 | PTY backend |

### Backend (Python Agent)
| Technology | Version | Purpose |
|------------|---------|---------|
| Python | 3.11.9 | Runtime |
| OpenAI SDK | 2.24.0 | LLM API client |
| HTTPX | 0.28.1 | HTTP client |
| Pydantic | 2.13.4 | Data validation |
| FastAPI + Uvicorn | 0.133.1 | API server |
| Rich | 14.3.3 | Terminal UI |
| SQLite (FTS5) | — | Session storage |

### DevOps & Tooling
| Technology | Purpose |
|------------|---------|
| uv | Python package manager |
| npm workspaces | Monorepo package management |
| esbuild | Electron main/preload bundling |
| electron-builder | App packaging & distribution |
| Git | Version control |

---

## Project Structure

```
hermes-agent/
├── apps/                        # Frontend applications (npm workspaces)
│   ├── desktop/                 # Electron desktop app
│   │   ├── src/                 # React renderer source
│   │   ├── electron/            # Electron main process + preload
│   │   ├── scripts/             # Build tooling (.mjs)
│   │   ├── assets/              # App icons
│   │   └── public/              # Static assets
│   └── shared/                  # Framework-agnostic JSON-RPC client
│
├── agent/                       # AI agent core subsystems
│   ├── conversation_loop.py     # Core conversation loop
│   ├── prompt_builder.py        # System prompt construction
│   ├── memory_manager.py        # Memory management
│   └── ...                      # ~90 modules
│
├── tools/                       # Tool implementations (80+ files)
│   ├── registry.py              # Auto-discovery tool registry
│   └── environments/            # Terminal backends
│
├── gateway/                     # Messaging gateway
│   ├── run.py                   # Gateway main loop
│   └── platforms/               # 20+ platform adapters
│
├── skills/                      # Built-in skills (20 categories)
├── plugins/                     # Plugin system (memory, providers, tools)
├── cron/                        # Scheduled job system
├── hermes_cli/                  # CLI subsystem
├── ui-tui/ + tui_gateway/       # Terminal UI (Ink + Python)
│
├── workspace/                   # Portable HERMES_HOME runtime directory
│   ├── config.yaml              # Runtime configuration
│   ├── .env.example             # Environment template (no real keys)
│   ├── SOUL.md                  # Agent persona
│   ├── memories/                # Long-term memory
│   └── skills/                  # User-created skills
│
├── run.ps1 / run.sh             # Portable launchers
├── hermes                       # Python entry point
├── run_agent.py                 # AIAgent class (~277KB)
├── pyproject.toml               # Python project metadata
└── package.json                 # npm workspace root
```

---

## Prerequisites

### Required
| Tool | Minimum Version | Check |
|------|----------------|-------|
| **Node.js** | ≥ 22.12.0 | `node --version` |
| **npm** | ≥ 10.x | `npm --version` |
| **Python** | ≥ 3.11, < 3.14 | `python --version` |
| **uv** | latest | `uv --version` |
| **Git** | any | `git --version` |
| **PowerShell** | 5.1+ (Windows) | `$PSVersionTable.PSVersion` |

### Optional
| Tool | Purpose |
|------|---------|
| ripgrep (rg) | Fast file search |
| ffmpeg | Voice/audio features |
| Docker | Container terminal backend |

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/hermes-agent-desktop.git
cd hermes-agent-desktop
```

### 2. Install Python Dependencies

```bash
# Create virtual environment
uv venv .venv --python 3.11

# Activate (Windows PowerShell)
.\.venv\Scripts\Activate.ps1

# Install all Python dependencies
uv pip install -e ".[all]"
```

### 3. Install Node.js Dependencies

```bash
# From repository root (installs all workspaces)
npm ci
```

### 4. Configure API Keys

```bash
# Copy environment template
cp workspace\.env.example workspace\.env

# Edit workspace\.env with your API keys
# Example for SiliconFlow:
#   OPENAI_API_KEY=sk-your-key-here
#   OPENAI_BASE_URL=https://api.siliconflow.cn/v1

# Edit workspace\config.yaml to set your model provider
```

---

## Running the App

### Desktop GUI (Electron)

```bash
cd apps/desktop
HERMES_DESKTOP_HERMES_ROOT="D:\path\to\project" npx electron .
```

Or using the build:

```bash
cd apps/desktop
npm run build
npm start
```

### TUI (Terminal UI)

```bash
# Windows PowerShell
.\run.ps1 --tui

# Linux/macOS/WSL
./run.sh --tui
```

### Interactive CLI

```bash
.\run.ps1              # Windows
./run.sh               # Linux/macOS/WSL
```

### Messaging Gateway

```bash
.\run.ps1 gateway start
```

---

## Building the Desktop App

### Development Build

```bash
cd apps/desktop
npm run build
```

Output goes to `apps/desktop/dist/`:
- `electron-main.cjs` — Main process bundle (CJS)
- `electron-preload.js` — Preload script (CJS)
- `index.html` + `assets/` — Renderer bundle (Vite)

### Production Packaging

```bash
cd apps/desktop
npm run pack          # Unpacked directory build
npm run dist:win      # Windows NSIS + MSI installer
npm run dist:mac      # macOS DMG + zip
npm run dist:linux    # Linux AppImage + deb + rpm
```

> **Windows Note:** The desktop app uses CJS format for the Electron main process to ensure `require('electron')` resolves correctly. See `apps/desktop/scripts/bundle-electron-main.mjs`.

---

## Configuration

### config.yaml (workspace/config.yaml)

```yaml
model:
  provider: custom              # or openrouter, openai, anthropic, etc.
  default: Qwen/Qwen3-32B       # Model identifier
  base_url: https://api.siliconflow.cn/v1
  api_mode: chat_completions    # OpenAI-compatible protocol
_config_version: 33
```

### .env (workspace/.env — NEVER COMMIT)

```ini
OPENAI_API_KEY=sk-xxx           # Your API key
OPENAI_BASE_URL=https://api.siliconflow.cn/v1
```

### Supported Providers

- **OpenRouter** — Multi-model router
- **OpenAI** — Direct OpenAI API
- **Anthropic** — Native Anthropic API
- **SiliconFlow** (硅基流动) — Chinese AI inference cloud
- **MiniMax** — Chinese LLM provider
- **Custom** — Any OpenAI-compatible endpoint

---

## Usage Guide

### Slash Commands

| Command | Action |
|---------|--------|
| `/help` | Show all available commands |
| `/model` | Switch AI model/provider |
| `/new` | Start a fresh conversation |
| `/skills` | Browse available skills |
| `/compress` | Compress conversation context |
| `/usage` | Check token usage |
| `/retry` | Retry the last turn |
| `/undo` | Undo the last turn |

### Tools Available

Core tools include: `terminal`, `read_file`, `write_file`, `web_search`, `browser_navigate`, `delegate_task`, `memory`, `skills`, `todo`, `vision_analyze`, `tts`, `code_execution`, and many more.

---

## Development Notes

### Desktop App Architecture

```
Electron Main Process (main.ts)
  └─ spawn("hermes", ["serve", "--host", "127.0.0.1", "--port", "0"])
       └─ Python tui_gateway (JSON-RPC over WebSocket)
            └─ AIAgent + tools + sessions
```

- **React Renderer** → `@hermes/shared` → WebSocket JSON-RPC → Python Backend
- **Slash Commands** → Client-side curation → Backend `slash.exec` → `_SlashWorker`
- **Preload** → `contextBridge.exposeInMainWorld('hermesDesktop', {...})`

### Key Build Scripts

| Script | File | Purpose |
|--------|------|---------|
| `bundle-electron-main.mjs` | `scripts/` | esbuild: main.ts → electron-main.cjs |
| `stage-native-deps.mjs` | `scripts/` | Copy node-pty native binaries |
| `write-build-stamp.mjs` | `scripts/` | Git commit stamp for bootstrap |
| `assert-dist-built.mjs` | `scripts/` | Verify dist/ completeness |

---

## License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

Built by [Nous Research](https://nousresearch.com).

---

<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

# Hermes Agent ☤
<p align="center">
  <a href="https://hermes-agent.nousresearch.com/">Hermes Agent</a> | <a href="https://hermes-agent.nousresearch.com/">Hermes Desktop</a>
</p>
<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/Docs-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="Documentation"></a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/Built%20by-Nous%20Research-blueviolet?style=for-the-badge" alt="Built by Nous Research"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/Lang-中文-red?style=for-the-badge" alt="中文"></a>
  <a href="README.ur-pk.md"><img src="https://img.shields.io/badge/Lang-اردو-green?style=for-the-badge" alt="اردو"></a>
  <a href="README.es.md"><img src="https://img.shields.io/badge/Lang-Español-orange?style=for-the-badge" alt="Español"></a>
</p>

**The self-improving AI agent built by [Nous Research](https://nousresearch.com).** It's the only agent with a built-in learning loop — it creates skills from experience, improves them during use, nudges itself to persist knowledge, searches its own past conversations, and builds a deepening model of who you are across sessions. Run it on a $5 VPS, a GPU cluster, or serverless infrastructure that costs nearly nothing when idle. It's not tied to your laptop — talk to it from Telegram while it works on a cloud VM.

Use any model you want — [Nous Portal](https://portal.nousresearch.com), OpenRouter, OpenAI, your own endpoint, and [many others](https://hermes-agent.nousresearch.com/docs/integrations/providers). Switch with `hermes model` — no code changes, no lock-in.

<table>
<tr><td><b>A real terminal interface</b></td><td>Full TUI with multiline editing, slash-command autocomplete, conversation history, interrupt-and-redirect, and streaming tool output.</td></tr>
<tr><td><b>Lives where you do</b></td><td>Telegram, Discord, Slack, WhatsApp, Signal, and CLI — all from a single gateway process. Voice memo transcription, cross-platform conversation continuity.</td></tr>
<tr><td><b>A closed learning loop</b></td><td>Agent-curated memory with periodic nudges. Autonomous skill creation after complex tasks. Skills self-improve during use. FTS5 session search with LLM summarization for cross-session recall. <a href="https://github.com/plastic-labs/honcho">Honcho</a> dialectic user modeling. Compatible with the <a href="https://agentskills.io">agentskills.io</a> open standard.</td></tr>
<tr><td><b>Scheduled automations</b></td><td>Built-in cron scheduler with delivery to any platform. Daily reports, nightly backups, weekly audits — all in natural language, running unattended.</td></tr>
<tr><td><b>Delegates and parallelizes</b></td><td>Spawn isolated subagents for parallel workstreams. Write Python scripts that call tools via RPC, collapsing multi-step pipelines into zero-context-cost turns.</td></tr>
<tr><td><b>Runs anywhere, not just your laptop</b></td><td>Six terminal backends — local, Docker, SSH, Singularity, Modal, and Daytona. Daytona and Modal offer serverless persistence — your agent's environment hibernates when idle and wakes on demand, costing nearly nothing between sessions. Run it on a $5 VPS or a GPU cluster.</td></tr>
<tr><td><b>Research-ready</b></td><td>Batch trajectory generation, trajectory compression for training the next generation of tool-calling models.</td></tr>
</table>

---

## Quick Install

### Linux, macOS, WSL2, Termux

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

### Windows (native, PowerShell)

> **Heads up:** Native Windows runs Hermes without WSL — CLI, gateway, TUI, and tools all work natively. If you'd rather use WSL2, the Linux/macOS one-liner above works there too. Found a bug? Please [file issues](https://github.com/NousResearch/hermes-agent/issues).

Run this in PowerShell:

```powershell
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```

The installer handles everything: uv, Python 3.11, Node.js, ripgrep, ffmpeg, **and a portable Git Bash** (MinGit, unpacked to `%LOCALAPPDATA%\hermes\git` — no admin required, completely isolated from any system Git install). Hermes uses this bundled Git Bash to run shell commands.

If you already have Git installed, the installer detects it and uses that instead. Otherwise a ~45MB MinGit download is all you need — it won't touch or interfere with any system Git.

> **Android / Termux:** The tested manual path is documented in the [Termux guide](https://hermes-agent.nousresearch.com/docs/getting-started/termux). On Termux, Hermes installs a curated `.[termux]` extra because the full `.[all]` extra currently pulls Android-incompatible voice dependencies.
>
> **Windows:** Native Windows is fully supported — the PowerShell one-liner above installs everything. If you'd rather use WSL2, the Linux command works there too. Native Windows install lives under `%LOCALAPPDATA%\hermes`; WSL2 installs under `~/.hermes` as on Linux.

After installation:

```bash
source ~/.bashrc    # reload shell (or: source ~/.zshrc)
hermes              # start chatting!
```

### Troubleshooting

#### Windows Defender or antivirus flags `uv.exe` as malware

If your antivirus (Bitdefender, Windows Defender, etc.) quarantines `uv.exe` from the Hermes `bin` folder (`%LOCALAPPDATA%\hermes\bin\uv.exe`), this is a **false positive**. The file is Astral's `uv` — the Rust Python package manager Hermes bundles to manage its Python environment. ML-based antivirus engines commonly flag unsigned Rust binaries that download and install packages.

**To verify your copy is authentic:**

```powershell
# Install GitHub CLI if needed
winget install --id GitHub.cli

# Login to GitHub
gh auth login

# Run verification
$uv = "$env:LOCALAPPDATA\hermes\bin\uv.exe"
$ver = (& $uv --version).Split(' ')[1]
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$zip = "$env:TEMP\uv.zip"
Invoke-WebRequest "https://github.com/astral-sh/uv/releases/download/$ver/uv-x86_64-pc-windows-msvc.zip" -OutFile $zip -UseBasicParsing
gh attestation verify $zip --repo astral-sh/uv
Expand-Archive $zip "$env:TEMP\uv_x" -Force
(Get-FileHash "$env:TEMP\uv_x\uv.exe").Hash -eq (Get-FileHash $uv).Hash
```

If attestation says "Verification succeeded" and the last line prints `True`, you're good.

**To whitelist Hermes:**
- **Windows Defender:** Run PowerShell as Admin → `Add-MpPreference -ExclusionPath "$env:LOCALAPPDATA\hermes\bin"`
- **Bitdefender:** Add an exception in the Bitdefender console (Protection > Antivirus > Settings > Manage Exceptions)
- Whitelist the **folder**, not the file hash — Hermes updates `uv` and the hash changes every version

For more context, see the upstream Astral reports: [astral-sh/uv#13553](https://github.com/astral-sh/uv/issues/13553), [astral-sh/uv#15011](https://github.com/astral-sh/uv/issues/15011), [astral-sh/uv#10079](https://github.com/astral-sh/uv/issues/10079).

---

## Getting Started

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

📖 **[Full documentation →](https://hermes-agent.nousresearch.com/docs/)**

---

## Skip the API-key collection — Nous Portal

Hermes works with whatever provider you want — that's not changing. But if you'd rather not collect five separate API keys for the model, web search, image generation, TTS, and a cloud browser, **[Nous Portal](https://portal.nousresearch.com)** covers all of them under one subscription:

- **300+ models** — pick any of them with `/model <name>`
- **Tool Gateway** — web search (Firecrawl), image generation (FAL), text-to-speech (OpenAI), cloud browser (Browser Use), all routed through your sub. No extra accounts.

One command from a fresh install:

```bash
hermes setup --portal
```

That logs you in via OAuth, sets Nous as your provider, and turns on the Tool Gateway. Check what's wired up any time with `hermes portal info`. Full details on the [Tool Gateway docs page](https://hermes-agent.nousresearch.com/docs/user-guide/features/tool-gateway).

You can still bring your own keys per-tool whenever you want — the gateway is per-backend, not all-or-nothing.

---

## CLI vs Messaging Quick Reference

Hermes has two entry points: start the terminal UI with `hermes`, or run the gateway and talk to it from Telegram, Discord, Slack, WhatsApp, Signal, or Email. Once you're in a conversation, many slash commands are shared across both interfaces.

| Action                         | CLI                                           | Messaging platforms                                                              |
| ------------------------------ | --------------------------------------------- | -------------------------------------------------------------------------------- |
| Start chatting                 | `hermes`                                      | Run `hermes gateway setup` + `hermes gateway start`, then send the bot a message |
| Start fresh conversation       | `/new` or `/reset`                            | `/new` or `/reset`                                                               |
| Change model                   | `/model [provider:model]`                     | `/model [provider:model]`                                                        |
| Set a personality              | `/personality [name]`                         | `/personality [name]`                                                            |
| Retry or undo the last turn    | `/retry`, `/undo`                             | `/retry`, `/undo`                                                                |
| Compress context / check usage | `/compress`, `/usage`, `/insights [--days N]` | `/compress`, `/usage`, `/insights [days]`                                        |
| Browse skills                  | `/skills` or `/<skill-name>`                  | `/<skill-name>`                                                                  |
| Interrupt current work         | `Ctrl+C` or send a new message                | `/stop` or send a new message                                                    |
| Platform-specific status       | `/platforms`                                  | `/status`, `/sethome`                                                            |

For the full command lists, see the [CLI guide](https://hermes-agent.nousresearch.com/docs/user-guide/cli) and the [Messaging Gateway guide](https://hermes-agent.nousresearch.com/docs/user-guide/messaging).

---

## Documentation

All documentation lives at **[hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)**:

| Section                                                                                             | What's Covered                                             |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [Quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)                 | Install → setup → first conversation in 2 minutes          |
| [CLI Usage](https://hermes-agent.nousresearch.com/docs/user-guide/cli)                              | Commands, keybindings, personalities, sessions             |
| [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration)                | Config file, providers, models, all options                |
| [Messaging Gateway](https://hermes-agent.nousresearch.com/docs/user-guide/messaging)                | Telegram, Discord, Slack, WhatsApp, Signal, Home Assistant |
| [Security](https://hermes-agent.nousresearch.com/docs/user-guide/security)                          | Command approval, DM pairing, container isolation          |
| [Tools & Toolsets](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools)            | 40+ tools, toolset system, terminal backends               |
| [Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills)              | Procedural memory, Skills Hub, creating skills             |
| [Memory](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory)                     | Persistent memory, user profiles, best practices           |
| [MCP Integration](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp)               | Connect any MCP server for extended capabilities           |
| [Cron Scheduling](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron)              | Scheduled tasks with platform delivery                     |
| [Context Files](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files)       | Project context that shapes every conversation             |
| [Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture)             | Project structure, agent loop, key classes                 |
| [Contributing](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing)             | Development setup, PR process, code style                  |
| [CLI Reference](https://hermes-agent.nousresearch.com/docs/reference/cli-commands)                  | All commands and flags                                     |
| [Environment Variables](https://hermes-agent.nousresearch.com/docs/reference/environment-variables) | Complete env var reference                                 |

---

## Migrating from OpenClaw

If you're coming from OpenClaw, Hermes can automatically import your settings, memories, skills, and API keys.

**During first-time setup:** The setup wizard (`hermes setup`) automatically detects `~/.openclaw` and offers to migrate before configuration begins.

**Anytime after install:**

```bash
hermes claw migrate              # Interactive migration (full preset)
hermes claw migrate --dry-run    # Preview what would be migrated
hermes claw migrate --preset user-data   # Migrate without secrets
hermes claw migrate --overwrite  # Overwrite existing conflicts
```

What gets imported:

- **SOUL.md** — persona file
- **Memories** — MEMORY.md and USER.md entries
- **Skills** — user-created skills → `~/.hermes/skills/openclaw-imports/`
- **Command allowlist** — approval patterns
- **Messaging settings** — platform configs, allowed users, working directory
- **API keys** — allowlisted secrets (Telegram, OpenRouter, OpenAI, Anthropic, ElevenLabs)
- **TTS assets** — workspace audio files
- **Workspace instructions** — AGENTS.md (with `--workspace-target`)

See `hermes claw migrate --help` for all options, or use the `openclaw-migration` skill for an interactive agent-guided migration with dry-run previews.

---

## Contributing

We welcome contributions! See the [Contributing Guide](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) for development setup, code style, and PR process.

Quick start for contributors — use the standard installer, then work from the
full git checkout it creates at `$HERMES_HOME/hermes-agent` (usually
`~/.hermes/hermes-agent`). This matches the layout used by `hermes update`, the
managed venv, lazy dependencies, gateway, and docs tooling.

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
cd "${HERMES_HOME:-$HOME/.hermes}/hermes-agent"
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

Manual clone fallback (for throwaway clones/CI where you intentionally do not
want the managed install layout):

Create the venv outside the cloned source tree — a venv inside the directory
the agent operates from can be wiped by a relative-path command the agent runs
against its own checkout, destroying the running runtime mid-session.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uv venv ~/.hermes/venvs/hermes-dev --python 3.11
source ~/.hermes/venvs/hermes-dev/bin/activate
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

---

## Community

- 💬 [Discord](https://discord.gg/NousResearch)
- 📚 [Skills Hub](https://agentskills.io)
- 🐛 [Issues](https://github.com/NousResearch/hermes-agent/issues)
- 🔌 [computer-use-linux](https://github.com/avifenesh/computer-use-linux) — Linux desktop-control MCP server for Hermes and other MCP hosts, with AT-SPI accessibility trees, Wayland/X11 input, screenshots, and compositor window targeting.
- 🔌 [HermesClaw](https://github.com/AaronWong1999/hermesclaw) — Community WeChat bridge: Run Hermes Agent and OpenClaw on the same WeChat account.

---

## License

MIT — see [LICENSE](LICENSE).

Built by [Nous Research](https://nousresearch.com).
