<div align="center">

# CodeBridge

[English](README.md) · [中文](README_CN.md)

</div>

> 本地代理，将 Claude Code、Codex、OpenCode、Cline、Aider 等编码代理连接到 OpenAI 兼容的 AI 提供商。与 Anthropic 无关。

## 功能

- 支持 50+ 提供商（NVIDIA NIM、Groq、DeepSeek、Gemini、OpenRouter 等）
- 自动故障转移：某个提供商挂了，自动切换下一个，无需重启
- 支持 Claude Code、Codex、Pi、OpenCode、Cline、Hermes、DeepSeek Harness、Grok Build、Muse Code、Aider
- Web 管理界面配置，无需手动改配置文件

## 环境要求

- Python 3.14+
- [uv](https://github.com/astral-sh/uv) 包管理器

## 安装

### 方式一：自动安装（推荐）

```powershell
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1")))
```

### 方式二：手动安装

```powershell
# 1. 安装 uv（已装可跳过）
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# 2. 进入项目目录
cd CodeBridge-main

# 3. 安装依赖
uv sync

# 4. 全局安装（可选，装完后任意目录都能用 fcc 命令）
uv tool install -e .
```

## 快速开始

```bash
# 1. 启动服务
fcc-server          # 或: uv run fcc-server

# 2. 浏览器自动打开管理界面
#    地址: http://127.0.0.1:8082/admin

# 3. 在管理界面配置提供商
#    - 粘贴 API Key（如 NVIDIA_NIM_API_KEY）
#    - 选择模型
#    - 点击 Apply

# 4. 启动编码代理
fcc-claude          # Claude Code
fcc-codex           # Codex
fcc-opencode        # OpenCode
fcc-cline           # Cline
fcc-aider           # Aider
```

## 支持的提供商

| 提供商     | 设置项                | 示例模型                                       |
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

完整列表见管理界面中的提供商目录。

## IDE 集成

### VS Code 中使用 Claude Code

安装 Claude Code 扩展，在 VS Code 设置（JSON）中添加：

```json
"claudeCode.disableLoginPrompt": true,
"claudeCode.environmentVariables": [
  { "name": "ANTHROPIC_BASE_URL", "value": "http://localhost:8082" },
  { "name": "ANTHROPIC_AUTH_TOKEN", "value": "freecc" }
]
```

### Codex App

编辑 `%USERPROFILE%\.codex\config.toml`（Windows）或 `~/.codex/config.toml`（macOS）：

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

编辑 Claude ACP 配置：

- Windows: `C:\Users\%USERNAME%\AppData\Roaming\JetBrains\acp-agents\installed.json`
- macOS/Linux: `~/.jetbrains/acp.json`

添加：

```json
"env": {
  "ANTHROPIC_BASE_URL": "http://localhost:8082",
  "ANTHROPIC_AUTH_TOKEN": "freecc"
}
```

### Claude Code 一直要求登录

打开 `~/.claude.json`（Windows 为 `%USERPROFILE%\.claude.json`），添加：

```json
"hasCompletedOnboarding": true
```

## 可选集成

在 **管理界面 → Messaging** 中配置：

### Discord 机器人

1. 在 [Discord Developer Portal](https://discord.com/developers/applications) 创建机器人
2. 开启 Message Content Intent，邀请时给予 read/send/Manage Messages 权限
3. 管理界面中：Messaging Platform 选 `discord`，填入 Bot Token、允许的频道、允许的目录

### Telegram 机器人

1. 通过 [@BotFather](https://t.me/BotFather) 创建机器人
2. 从 [@userinfobot](https://t.me/userinfobot) 获取你的用户 ID
3. 管理界面中：Messaging Platform 选 `telegram`，填入 Bot Token、用户 ID、允许的目录

### 语音输入

重新运行安装脚本，加上语音参数：

```powershell
# NVIDIA NIM 语音转文字
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1"))) -VoiceNim

# 本地 Whisper
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1"))) -VoiceLocal
```

## 命令一览

| 命令                   | 说明             |
|------------------------|------------------|
| `fcc-server`           | 启动代理服务     |
| `fcc-server --version` | 查看版本         |
| `fcc-claude`           | 启动 Claude Code |
| `fcc-codex`            | 启动 Codex       |
| `fcc-opencode`         | 启动 OpenCode    |
| `fcc-cline`            | 启动 Cline       |
| `fcc-aider`            | 启动 Aider       |

## 更新

重新运行安装命令。手动安装用户：

```powershell
uv tool install --force -e .
```

## 卸载

```powershell
# 自动卸载
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/uninstall.ps1")))

# 手动卸载
uv tool uninstall free-claude-code
```

## 许可证

MIT License。详见 [LICENSE](LICENSE)。
