<div align="center">

# CodeBridge

[English](README.md) · [中文](README_CN.md)

</div>

> Local proxy connecting coding agents (Claude Code, Codex, OpenCode, Cline, Aider, etc.) to OpenAI-compatible AI providers. Not affiliated with Anthropic.

## What It Does

- Routes requests to 50+ providers (NVIDIA NIM, Groq, DeepSeek, Gemini, OpenRouter, etc.)
- Auto-fallback: if one provider fails, tries the next without restarting
- Works with Claude Code, Codex, Pi, OpenCode, Cline, Hermes, DeepSeek Harness, Grok Build, Muse Code, Aider
- Web Admin UI for configuration, no need to edit config files

## Prerequisites

- Python 3.14+
- [uv](https://github.com/astral-sh/uv) package manager

## Install

### Option A: Automatic installer (Recommended)

macOS/Linux:

```bash
curl -fsSL "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.sh" | sh
```

Windows PowerShell:

```powershell
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1")))
```

### Option B: Manual install

```bash
# 1. Install uv (skip if already installed)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# 2. Enter project directory
cd CodeBridge-main

# 3. Install dependencies
uv sync

# 4. Install globally (optional, makes fcc commands available everywhere)
uv tool install -e .
```

## Quick Start

```bash
# 1. Start server
fcc-server          # or: uv run fcc-server

# 2. Open Admin UI in browser (auto-opens)
#    URL: http://127.0.0.1:8082/admin

# 3. Configure provider in Admin UI
#    - Paste your API key (e.g. NVIDIA_NIM_API_KEY)
#    - Select a model
#    - Click Apply

# 4. Run a coding agent
fcc-claude          # Claude Code
fcc-codex           # Codex
fcc-opencode        # OpenCode
fcc-cline           # Cline
fcc-aider           # Aider
```

## Supported Providers

| Provider   | Setting               | Example Model                                  |
|------------|-----------------------|------------------------------------------------|
| NVIDIA NIM | `NVIDIA_NIM_API_KEY`  | `nvidia_nim/nvidia/nemotron-3-super-120b-a12b` |
| OpenRouter | `OPENROUTER_API_KEY`  | `open_router/openrouter/free`                  |
| Groq       | `GROQ_API_KEY`        | `groq/llama-3.3-70b-versatile`                 |
| DeepSeek   | `DEEPSEEK_API_KEY`    | `deepseek/deepseek-chat`                       |
| Gemini     | `GEMINI_API_KEY`      | `gemini/models/gemini-2.0-flash`               |
| DeepInfra  | `DEEPINFRA_API_KEY`   | `deepinfra/deepseek-ai/DeepSeek-V4-Flash`      |
| OpenAI     | `Connect in Admin UI` | `openai/<model-id>`                            |
| xAI        | `XAI_API_KEY`         | `xai/grok-4.5`                                 |
| Mistral    | `MISTRAL_API_KEY`     | `mistral/devstral-small-latest`                |
| Kimi       | `KIMI_API_KEY`        | `kimi/kimi-k2.5`                               |
| Ollama     | `OLLAMA_BASE_URL`     | `ollama/<model-tag>`                           |
| LM Studio  | `LM_STUDIO_BASE_URL`  | `lmstudio/<model-id>`                          |

Full list: see the provider catalog in Admin UI.

## IDE Integration

### Claude Code in VS Code

Install the Claude Code extension, then add to VS Code settings (JSON):

```json
"claudeCode.disableLoginPrompt": true,
"claudeCode.environmentVariables": [
  { "name": "ANTHROPIC_BASE_URL", "value": "http://localhost:8082" },
  { "name": "ANTHROPIC_AUTH_TOKEN", "value": "freecc" }
]
```

### Codex App

Edit `%USERPROFILE%\.codex\config.toml` (Windows) or `~/.codex/config.toml` (macOS):

```toml
model_provider = "fcc"
model = "nvidia_nim/nvidia/nemotron-3-super-120b-a12b"

[model_providers.fcc]
name = "Free Claude Code"
base_url = "http://127.0.0.1:8082/v1"
wire_api = "responses"

[model_providers.fcc.auth]
command = "fcc-codex"
args = ["--print-proxy-auth-token"]
```

### JetBrains

Edit the Claude ACP config:

- Windows: `C:\Users\%USERNAME%\AppData\Roaming\JetBrains\acp-agents\installed.json`
- macOS/Linux: `~/.jetbrains/acp.json`

Add:

```json
"env": {
  "ANTHROPIC_BASE_URL": "http://localhost:8082",
  "ANTHROPIC_AUTH_TOKEN": "freecc"
}
```

### Claude Code keeps asking to log in

Open `~/.claude.json` (or `%USERPROFILE%\.claude.json` on Windows) and add:

```json
"hasCompletedOnboarding": true
```

## Optional Integrations

Configure in **Admin UI → Messaging**:

### Discord Bot

1. Create a bot at [Discord Developer Portal](https://discord.com/developers/applications)
2. Enable Message Content Intent, invite with read/send/Manage Messages permissions
3. In Admin UI: set Messaging Platform to `discord`, enter Bot Token, Allowed Channels, Allowed Directory

### Telegram Bot

1. Create a bot via [@BotFather](https://t.me/BotFather)
2. Get your user ID from [@userinfobot](https://t.me/userinfobot)
3. In Admin UI: set Messaging Platform to `telegram`, enter Bot Token, User ID, Allowed Directory

### Voice Notes

Re-run the installer with the voice flag:

```bash
# NVIDIA NIM transcription
curl -fsSL "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.sh" | sh -s -- --voice-nim

# Local Whisper
curl -fsSL "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.sh" | sh -s -- --voice-local
```

## Commands

| Command                | Description            |
|------------------------|------------------------|
| `fcc-server`           | Start the proxy server |
| `fcc-server --version` | Check version          |
| `fcc-claude`           | Launch Claude Code     |
| `fcc-codex`            | Launch Codex           |
| `fcc-opencode`         | Launch OpenCode        |
| `fcc-cline`            | Launch Cline           |
| `fcc-aider`            | Launch Aider           |

## Update

Re-run the install command. For manual install:

```bash
uv tool install --force -e .
```

## Uninstall

```bash
# Automatic
curl -fsSL "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/uninstall.sh" | sh

# Manual
uv tool uninstall free-claude-code
```

## License

MIT License. See [LICENSE](LICENSE).
