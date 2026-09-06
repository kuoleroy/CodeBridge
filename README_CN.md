<div align="center">

<h1>
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="assets/free-claude-code-wordmark-light.svg">
    <img src="assets/free-claude-code-wordmark-dark.svg" alt="Free Claude Code" width="610">
  </picture>
</h1>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Python 3.14](https://img.shields.io/badge/python-3.14-3776ab.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/downloads/)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json&style=for-the-badge)](https://github.com/astral-sh/uv)

[快速开始](#快速开始) · [提供商](#选择提供商) · [客户端](#连接客户端) · [集成](#可选集成) · [管理](#管理安装)

</div>

<p align="center">
  <em>独立开源项目，与 Anthropic 无关。Claude 和 Claude Code 是 Anthropic 的商标。</em>
</p>

## 功能特点

- **50+ 服务提供商，每月 13 亿免费 Token** - 使用免费、付费、订阅和本地模型，无需担心账户风险
- **10 个编码代理，一个模型目录** - 支持 Claude Code、Codex、Pi、OpenCode、Cline、Hermes、DeepSeek Harness、Grok Build、Muse Code、Aider
- **自动故障转移** - 当某个提供商宕机时，自动切换到下一个配置的模型
- **终端、桌面、IDE、手机** - 支持原生启动器、VS Code、JetBrains、Discord、Telegram
- **私有本地聊天** - 在 Admin 中与任何配置的模型进行聊天会话
- **语音输入** - 支持本地 Whisper 或 NVIDIA NIM 语音转文字

## 快速开始

### 1. 安装

Windows PowerShell：

```powershell
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1")))
```

### 2. 启动服务

```powershell
fcc-server
```

服务启动后会自动打开 Admin UI（http://127.0.0.1:8082/admin）

### 3. 配置提供商

1. 获取 API Key（如 NVIDIA NIM、Groq 等）
2. 在 Admin UI 中粘贴 Key
3. 选择模型
4. 点击 **Apply**

### 4. 运行编码代理

```powershell
fcc-claude    # Claude Code
fcc-codex     # Codex
fcc-opencode  # OpenCode
fcc-cline     # Cline
fcc-aider     # Aider
```

## 选择提供商

| 提供商 | Admin UI 设置 | 示例模型 |
|--------|---------------|----------|
| NVIDIA NIM | `NVIDIA_NIM_API_KEY` | `nvidia_nim/nvidia/nemotron-3-super-120b-a12b` |
| OpenRouter | `OPENROUTER_API_KEY` | `open_router/openrouter/free` |
| Groq | `GROQ_API_KEY` | `groq/llama-3.3-70b-versatile` |
| DeepSeek | `DEEPSEEK_API_KEY` | `deepseek/deepseek-chat` |
| Gemini | `GEMINI_API_KEY` | `gemini/models/gemini-2.0-flash` |
| DeepInfra | `DEEPINFRA_API_KEY` | `deepinfra/deepseek-ai/DeepSeek-V4-Flash` |

## 连接客户端

### 终端使用

启动 `fcc-server`，然后运行对应的客户端命令。

### VS Code 集成

安装 Claude Code 扩展，在设置中添加：

```json
"claudeCode.environmentVariables": [
  { "name": "ANTHROPIC_BASE_URL", "value": "http://localhost:8082" },
  { "name": "ANTHROPIC_AUTH_TOKEN", "value": "freecc" }
]
```

## 可选集成

### Discord 机器人

1. 在 Discord Developer Portal 创建机器人
2. 在 Admin UI 配置 Discord Bot Token
3. 设置消息平台为 `discord`

### Telegram 机器人

1. 通过 @BotFather 创建机器人
2. 在 Admin UI 配置 Telegram Bot Token
3. 设置消息平台为 `telegram`

## 管理安装

### 检查版本

```powershell
fcc-server --version
```

### 更新

重新运行安装命令即可。

### 卸载

```powershell
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/uninstall.ps1")))
```

## 项目链接

- [报告 Bug 或请求功能](https://github.com/Alishahryar1/free-claude-code/issues)
- [贡献指南](CONTRIBUTING.md)

## 许可证

MIT License。详见 [LICENSE](LICENSE)。