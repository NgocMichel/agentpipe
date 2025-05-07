# AgentPipe 🚀

![AgentPipe Logo](screenshots/agentpipe-logo.png)

[![CI](https://github.com/kevinelliott/agentpipe/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/kevinelliott/agentpipe/actions/workflows/test.yml)
[![Go Version](https://img.shields.io/badge/Go-1.24+-00ADD8?style=flat&logo=go)](https://go.dev/)
[![Release](https://img.shields.io/github/v/release/kevinelliott/agentpipe?color=success)](https://github.com/kevinelliott/agentpipe/releases)
[![License](https://img.shields.io/github/license/kevinelliott/agentpipe?color=blue)](https://github.com/kevinelliott/agentpipe/blob/main/LICENSE)
[![Go Report Card](https://goreportcard.com/badge/github.com/kevinelliott/agentpipe)](https://goreportcard.com/report/github.com/kevinelliott/agentpipe)
[![Downloads](https://img.shields.io/github/downloads/kevinelliott/agentpipe/total?color=brightgreen)](https://github.com/kevinelliott/agentpipe/releases)
[![GitHub Stars](https://img.shields.io/github/stars/kevinelliott/agentpipe?color=yellow&logo=github)](https://github.com/kevinelliott/agentpipe)

AgentPipe is a powerful CLI and TUI application that orchestrates conversations between multiple AI agents. It allows different AI CLI tools (like Claude, Cursor, Gemini, Qwen, Ollama) to communicate with each other in a shared "room", creating dynamic multi-agent conversations with real-time metrics, cost tracking, and interactive user participation.

## Screenshots

### Enhanced TUI Interface
![AgentPipe TUI](screenshots/tui/tui1.png)
*Enhanced TUI with multi-panel layout: agent list with status indicators, conversation view with metrics, statistics panel showing turns and total cost, configuration panel, and user input area*

### Console/CLI Interface
![AgentPipe Console](screenshots/console/console1.png)
*CLI output showing color-coded agent messages with agent type indicators (e.g., "Alice (qoder)"), HOST vs SYSTEM distinction, and inline metrics display*

## Supported AI Agents

All agents now use a **standardized interaction pattern** with structured three-part prompts, message filtering, and comprehensive logging for reliable multi-agent conversations.

- ✅ **Amp** (Sourcegraph) - Advanced coding agent with autonomous reasoning ⚡ **Thread-optimized**
- ✅ **Claude** (Anthropic) - Advanced reasoning and coding
- ✅ **Codex** (OpenAI) - Code generation specialist (non-interactive exec mode)
- ✅ **Copilot** (GitHub) - Terminal-based coding agent with multiple model support
- ✅ **Continue** - AI coding assistant with TUI and headless modes for development workflows
- ✅ **Crush** (Charm/Charmbracelet) - Terminal-first AI coding assistant with multi-provider support
- ✅ **Cursor** (Cursor AI) - IDE-integrated AI assistance
- ✅ **Factory** (Factory.ai) - Agent-native software development with Droid (non-interactive exec mode)
- ✅ **Gemini** (Google) - Multimodal understanding
- ✅ **Groq** - Fast AI code assistant powered by Groq LPUs (Lightning Processing Units)
- ✅ **Kimi** (Moonshot AI) - Interactive AI agent with advanced reasoning (interactive-first CLI)
- ✅ **OpenCode** (SST) - AI coding agent built for the terminal (non-interactive run mode)
- ✅ **OpenRouter** - Unified API access to 400+ models from multiple providers (API-based, no CLI required) 🌐 **API-based**
- ✅ **Qoder** - Agentic coding platform with enhanced context engineering
- ✅ **Qwen** (Alibaba) - Multilingual capabilities
- ✅ **Ollama** - Local LLM support (planned)

## Features

### Core Capabilities
- **Multi-Agent Conversations**: Connect multiple AI agents in a single conversation
- **Multiple Conversation Modes**:
  - `round-robin`: Agents take turns in a fixed order
  - `reactive`: Agents respond based on conversation dynamics
  - `free-form`: Agents participate freely as they see fit
- **Flexible Configuration**: Use command-line flags or YAML configuration files

### Enhanced TUI Interface
- Multi-panel layout with dedicated sections for agents, chat, stats, and config
- Color-coded agent messages with unique colors per agent
- **Agent type indicators** showing agent type in parentheses (e.g., "Alice (qoder)")
- **Branded sunset logo** with gradient colors
- Real-time agent activity indicators (🟢 active/responding, ⚫ idle)
- Inline metrics display (response time in seconds, token count, cost)
- **Conversation search** (Ctrl+F) with n/N navigation through results
- **Agent filtering** via slash commands (/filter, /clear)
- **Help modal** (?) showing all keyboard shortcuts
- Topic panel showing initial conversation prompt
- Statistics panel with turn counters and total conversation cost
- Configuration panel displaying all active settings and config file path
- Interactive user input panel for joining conversations
- Smart message consolidation (headers only on speaker change)
- Proper multi-paragraph message formatting

### Production Features
- **Prometheus Metrics**: Comprehensive observability with 10+ metrics types
  - Request rates, durations, errors
  - Token usage and cost tracking
  - Active conversations, retry attempts, rate limit hits
  - HTTP server with `/metrics`, `/health`, and web UI endpoints
  - Ready for Grafana dashboards and alerting
- **Conversation Management**:
  - Save/resume conversations from state files
  - Export to JSON, Markdown, or HTML formats
  - Automatic chat logging to `~/.agentpipe/chats/`
- **Reliability & Performance**:
  - Rate limiting per agent with token bucket algorithm
  - Retry logic with exponential backoff (configurable)
  - Structured error handling with error types
  - Config hot-reload for development workflows
- **Middleware Pipeline**: Extensible message processing
  - Built-in: logging, metrics, validation, sanitization, filtering
  - Custom middleware support for transforms and filters
  - Error recovery and panic handling
- **Docker Support**: Multi-stage builds, docker-compose, production-ready
- **Health Checks**: Automatic agent health verification before conversations
- **Agent Detection**: Built-in doctor command to check installed AI CLIs
- **Customizable Agents**: Configure prompts, models, and behaviors for each agent

## What's New

See [CHANGELOG.md](CHANGELOG.md) for detailed version history and release notes.

**Latest Release**: v0.6.0 - OpenRouter API Support

**What's New in v0.6.0**:

🌐 **OpenRouter API Support - First API-Based Agent**:
- **New Agent Type**: Direct API integration without CLI dependencies
  - Access 400+ models from multiple providers through a unified API
  - No CLI installation required - just set `OPENROUTER_API_KEY`
  - Support for models from Anthropic, OpenAI, Google, DeepSeek, and more
  - Real-time token usage and accurate cost tracking from API responses
  - Streaming and non-streaming message support
  - Smart model matching with provider registry integration
- **Example Configurations**:
  - `examples/openrouter-conversation.yaml` - Multi-provider conversation
  - `examples/openrouter-solo.yaml` - Single agent testing
- **Foundation for Future API Agents**: Paves the way for direct Anthropic API, Google AI API, etc.

**Previous Release - v0.4.9** (2025-10-25): Crush CLI support
- Full support for Charm's Crush CLI with multi-provider capabilities

**Previous Release - v0.4.8** (2025-10-25): Fixed GitHub API rate limiting
- PyPI integration for Kimi, npm registry for Qwen
- No more 403 rate limit errors

**Previous Release - v0.4.7** (2025-10-25): Improved Kimi version detection
**Previous Release - v0.4.6** (2025-10-25): Groq Code CLI support
- Dedicated security workflows (Trivy and CodeQL)
- Enhanced README badges with downloads and stars metrics
- Fixed Windows test failures for platform-specific installations

**Previous Release - v0.4.3** (2025-10-25): Kimi CLI agent support
- Full support for Kimi CLI from Moonshot AI
- Installation via `uv tool install kimi-cli` (requires Python 3.13+)

**Previous Release - v0.4.2** (2025-10-24): Qoder installation improvements
- Added `--force` flag to Qoder install and upgrade commands

**Previous Release - v0.4.1** (2025-10-22): Conversation summarization & unique agent IDs
- AI-generated summaries at conversation completion
- Unique agent IDs for multiple agents of same type
- Local event storage to `~/.agentpipe/events/`

**Previous Release - v0.4.0**: Bridge connection events and cancellation detection
**Previous Release - v0.3.0**: Real-time conversation streaming to AgentPipe Web
**Previous Release - v0.2.2**: JSON output support for agents list command
**Previous Release - v0.2.1**: OpenCode agent and improved package management
**Previous Release - v0.2.0**: Agent upgrade command and automated version detection

## Installation

### Using Homebrew (macOS/Linux)

```bash
brew tap kevinelliott/tap
brew install agentpipe
```

### Using the install script

```bash
curl -sSL https://raw.githubusercontent.com/kevinelliott/agentpipe/main/install.sh | bash
```

### Using Go

```bash
go install github.com/kevinelliott/agentpipe@latest
```

### Build from source

```bash
git clone https://github.com/kevinelliott/agentpipe.git
cd agentpipe

# Build only
go build -o agentpipe .

# Or build and install to /usr/local/bin (requires sudo on macOS/Linux)
sudo make install

# Or install to custom location (e.g., ~/.local/bin, no sudo needed)
make install PREFIX=$HOME/.local
```

## Prerequisites

AgentPipe requires at least one AI CLI tool to be installed:

- [Amp CLI](https://ampcode.com) - `amp` ⚡ **Optimized**
  - Install: `npm install -g @sourcegraph/amp` or see [installation guide](https://ampcode.com/install)
  - Authenticate: Follow Amp documentation
  - Features: Autonomous coding, IDE integration, complex task execution
  - **Thread Management**: AgentPipe uses Amp's native threading to maintain server-side conversation state
  - **Smart Filtering**: Only sends new messages from other agents, reducing API costs by 50-90%
  - **Structured Context**: Initial prompts are delivered in a clear, three-part structure
- [Claude CLI](https://github.com/anthropics/claude-code) - `claude`
  - Install: See [installation guide](https://docs.claude.com/en/docs/claude-code/installation)
  - Authenticate: Run `claude` and follow authentication prompts
  - Features: Advanced reasoning, coding, complex task execution
- [GitHub Copilot CLI](https://github.com/github/copilot-cli) - `copilot`
  - Install: `npm install -g @github/copilot`
  - Authenticate: Launch `copilot` and use `/login` command
  - Requires: Node.js v22+, npm v10+, and active GitHub Copilot subscription
- [Cursor CLI](https://cursor.com/cli) - `cursor-agent`
  - Install: `curl https://cursor.com/install -fsS | bash`
  - Authenticate: `cursor-agent login`
- [Factory CLI](https://factory.ai/product/cli) - `droid`
  - Install: `curl -fsSL https://app.factory.ai/cli | sh`
  - Authenticate: Sign in via browser when prompted
  - Features: Agent-native development, Code Droid and Knowledge Droid, CI/CD integration
- [Gemini CLI](https://github.com/google/generative-ai-cli) - `gemini`
- [Kimi CLI](https://github.com/MoonshotAI/kimi-cli) - `kimi`
  - Install: `uv tool install --python 3.13 kimi-cli`
  - Upgrade: `uv tool upgrade kimi-cli --python 3.13 --no-cache`
  - Authenticate: Run `kimi` and use `.set_api_key` command with Moonshot AI API key
  - Get API Key: [platform.moonshot.cn](https://platform.moonshot.cn/console/api-keys)
  - Features: Advanced reasoning, multi-turn conversations, MCP/ACP protocol support, interactive-first design
  - ⚠️ Note: Kimi is designed as an interactive CLI tool - best experience running interactively
- [OpenCode CLI](https://opencode.ai) - `opencode`
  - Install: `npm install -g opencode-ai@latest`
  - Authenticate: Run `opencode auth login` and configure API keys
  - Features: Terminal-native AI coding agent, non-interactive run mode, multi-provider support
- [Qoder CLI](https://qoder.com/cli) - `qodercli`
  - Install: See [installation guide](https://qoder.com/cli)
  - Authenticate: Run `qodercli` and use `/login` command
  - Features: Enhanced context engineering, intelligent agents, MCP integration, built-in tools
- [Qwen CLI](https://github.com/QwenLM/qwen-code) - `qwen`
- [Codex CLI](https://github.com/openai/codex-cli) - `codex`
  - Install: `npm install -g @openai/codex` or `brew install --cask codex`
  - Uses `codex exec` subcommand for non-interactive mode
  - Automatically bypasses approval prompts for multi-agent conversations
  - ⚠️ For development/testing only - not recommended for production use
- [Ollama](https://github.com/ollama/ollama) - `ollama` (planned)

Check which agents are available on your system:

```bash
agentpipe doctor
```

## Support AgentPipe Development

Help support the ongoing development and testing of AgentPipe by using these referral links when signing up for AI agent services. Using these links provides the author with service credits to continue improving agent implementations and adding new features.

### Referral Links

- **Qoder CLI** - Enhanced context engineering and intelligent agents
  - **Referral Link**: [Sign up with referral code](https://qoder.com/referral?referral_code=1oOG0VHes5uNvrKJr8gwc7Fjm7AWxx52)
  - Regular link: [qoder.com/cli](https://qoder.com/cli)
  - Benefits: Using the referral link provides credits for continued Qoder integration development

> **Note**: Using referral links costs you nothing extra and helps fund the development of better multi-agent orchestration features. Thank you for your support!

## Quick Start

### Simple conversation with command-line flags

```bash
# Start a conversation between Claude and Gemini
agentpipe run -a claude:Alice -a gemini:Bob -p "Let's discuss AI ethics"

# Use TUI mode with metrics for a rich experience
agentpipe run -a claude:Poet -a gemini:Scientist --tui --metrics

# Configure conversation parameters
agentpipe run -a claude:Agent1 -a gemini:Agent2 \
  --mode reactive \
  --max-turns 10 \
  --timeout 45 \
  --prompt "What is consciousness?"

# Specify models for agents that support it
agentpipe run -a claude:claude-sonnet-4-5:Alice -a gemini:gemini-2.5-pro:Bob

# Use OpenRouter with specific models
agentpipe run -a openrouter:anthropic/claude-sonnet-4-5:Assistant \
  -a openrouter:google/gemini-2.5-pro:Reviewer \
  --prompt "Design a microservices architecture"
```

### Agent specification formats

AgentPipe supports three formats for specifying agents via the `--agents` / `-a` flag:

1. **`type`** - Use agent type with auto-generated name
   ```bash
   agentpipe run -a claude -a gemini
   # Creates: claude-agent-1, gemini-agent-2
   ```

2. **`type:name`** - Use agent type with custom name (uses default model)
   ```bash
   agentpipe run -a claude:Alice -a gemini:Bob
   # Creates: Alice (Claude), Bob (Gemini)
   ```

3. **`type:model:name`** - Use agent type with specific model and custom name
   ```bash
   agentpipe run -a claude:claude-sonnet-4-5:Architect \
     -a gemini:gemini-2.5-pro:Reviewer
   # Creates: Architect (Claude Sonnet 4.5), Reviewer (Gemini 2.5 Pro)
   ```

**Model Support by Agent Type:**

| Agent Type | Model Support | Required | Example Models |
|------------|--------------|----------|----------------|
| `claude` | ✅ Optional | No | `claude-sonnet-4-5`, `claude-opus-4` |
| `gemini` | ✅ Optional | No | `gemini-2.5-pro`, `gemini-2.5-flash` |
| `copilot` | ✅ Optional | No | `gpt-4o`, `gpt-4-turbo` |
| `qwen` | ✅ Optional | No | `qwen-plus`, `qwen-turbo` |
| `factory` | ✅ Optional | No | `claude-sonnet-4-5`, `gpt-4o` |
| `qoder` | ✅ Optional | No | `claude-sonnet-4-5`, `gpt-4o` |
| `codex` | ✅ Optional | No | `gpt-4o`, `gpt-4-turbo` |
| `groq` | ✅ Optional | No | `llama3-70b`, `mixtral-8x7b` |
| `crush` | ✅ Optional | No | `deepseek-r1`, `qwen-2.5` |
| `openrouter` | ✅ **Required** | Yes | `anthropic/claude-sonnet-4-5`, `google/gemini-2.5-pro` |
| `kimi` | ❌ Not supported | No | N/A |
| `cursor` | ❌ Not supported | No | N/A |
| `amp` | ❌ Not supported | No | N/A |

**Examples:**

```bash
# Use default models
agentpipe run -a claude:Alice -a gemini:Bob

# Specify models explicitly
agentpipe run -a claude:claude-sonnet-4-5:Alice \
  -a gemini:gemini-2.5-pro:Bob

# Mix default and explicit models
agentpipe run -a claude:Architect \
  -a gemini:gemini-2.5-flash:Reviewer

# OpenRouter requires model specification
agentpipe run -a openrouter:anthropic/claude-sonnet-4-5:Claude \
  -a openrouter:google/gemini-2.5-pro:Gemini

# Error: OpenRouter without model
agentpipe run -a openrouter:Assistant  # ❌ Will fail

# Error: Agents that don't support models
agentpipe run -a kimi:some-model:Assistant  # ❌ Will fail
```

### Using configuration files

```bash
# Run with a configuration file
agentpipe run -c examples/simple-conversation.yaml

# Run a debate between three agents
agentpipe run -c examples/debate.yaml --tui

# Brainstorming session with multiple agents
agentpipe run -c examples/brainstorm.yaml
```

## Configuration

### YAML Configuration Format

```yaml
version: "1.0"

agents:
  - id: agent-1
    type: claude  # Agent type (claude, gemini, qwen, etc.)
    name: "Friendly Assistant"
    prompt: "You are a helpful and friendly assistant."
    announcement: "Hello everyone! I'm here to help!"
    model: claude-3-sonnet  # Optional: specific model
    temperature: 0.7        # Optional: response randomness
    max_tokens: 1000        # Optional: response length limit

  - id: agent-2
    type: gemini
    name: "Technical Expert"
    prompt: "You are a technical expert who loves explaining complex topics."
    announcement: "Technical Expert has joined the chat!"
    temperature: 0.5

orchestrator:
  mode: round-robin       # Conversation mode
  max_turns: 10          # Maximum conversation turns
  turn_timeout: 30s      # Timeout per agent response
  response_delay: 2s     # Delay between responses
  initial_prompt: "Let's start our discussion!"

logging:
  enabled: true                    # Enable chat logging
  chat_log_dir: ~/.agentpipe/chats # Custom log path (optional)
  show_metrics: true               # Display response metrics in TUI (time, tokens, cost)
  log_format: text                 # Log format (text or json)
```

### Conversation Modes

- **round-robin**: Agents speak in a fixed rotation
- **reactive**: Agents respond based on who spoke last
- **free-form**: Agents decide when to participate

## Commands

### `agentpipe run`

Start a conversation between agents.

**Flags:**
- `-c, --config`: Path to YAML configuration file
- `-a, --agents`: List of agents (formats: `type`, `type:name`, or `type:model:name`)
- `-m, --mode`: Conversation mode (default: round-robin)
- `--max-turns`: Maximum conversation turns (default: 10)
- `--timeout`: Response timeout in seconds (default: 30)
- `--delay`: Delay between responses in seconds (default: 1)
- `-p, --prompt`: Initial conversation prompt
- `-t, --tui`: Use enhanced TUI interface with panels and user input
- `--log-dir`: Custom path for chat logs (default: ~/.agentpipe/chats)
- `--no-log`: Disable chat logging
- `--metrics`: Display response metrics (duration, tokens, cost) in TUI
- `--skip-health-check`: Skip agent health checks (not recommended)
- `--health-check-timeout`: Health check timeout in seconds (default: 5)
- `--save-state`: Save conversation state to file on completion
- `--state-file`: Custom state file path (default: auto-generated)
- `--watch-config`: Watch config file for changes and reload (development mode)

### `agentpipe doctor`

Comprehensive system health check to verify AgentPipe is properly configured and ready to use.

```bash
agentpipe doctor

# Output in JSON format for programmatic consumption
agentpipe doctor --json
```

The doctor command performs a complete diagnostic check of your system and provides detailed information about:

**System Environment:**
- Go runtime version and architecture
- PATH environment validation
- Home directory detection
- AgentPipe directories (`~/.agentpipe/chats`, `~/.agentpipe/states`)

**AI Agent CLIs:**
- Detection of al