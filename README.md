# PipeLLM WebSearch

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

> Give your coding agent the ability to search the web, read pages, and stay up to date — powered by [PipeLLM](https://pipellm.com).

A skill extension for coding agents (Claude Code, Cursor, Gemini CLI, Codex, OpenCode) that teaches your agent **when** and **how** to use web search effectively during development tasks.

## ✨ What It Does

This skill teaches your coding agent to:

- 🔍 **Search the web** — find documentation, solutions, and references
- ⚡ **Quick search** — fast lookups when speed matters
- 📄 **Read web pages** — extract clean content from any URL
- 📰 **Search news** — find current events and recent developments

Your agent learns to **choose the right search type** based on the situation — fast snippets for quick lookups, deep RAG search for thorough research, or news search for current events.

## 🚀 Installation

### Claude Code

```
/plugin install pipellm-websearch@pipellm-websearch
```

Or register the marketplace first:

```
/plugin marketplace add PipeLlm-AI/pipellm-websearch-skill
/plugin install pipellm-websearch@pipellm-websearch
```

### Cursor

```
/add-plugin pipellm-websearch
```

### Gemini CLI

```
gemini extensions install https://github.com/PipeLlm-AI/pipellm-websearch-skill
```

### Codex

```
Fetch and follow instructions from https://raw.githubusercontent.com/PipeLlm-AI/pipellm-websearch-skill/refs/heads/main/.codex/INSTALL.md
```

### OpenCode

```
Fetch and follow instructions from https://raw.githubusercontent.com/PipeLlm-AI/pipellm-websearch-skill/refs/heads/main/.opencode/INSTALL.md
```

## 🔑 Setup

1. Visit [console.pipellm.com](https://console.pipellm.com)
2. Sign up or log in — new accounts get **$5 free credit**
3. Go to **API Keys** → **Create Key** (starts with `pipe-`)
4. Set your key: `export PIPELLM_API_KEY=pipe-your-key-here`

## 🛠️ Available Search Types

| Type | Speed | Use Case |
|------|-------|----------|
| **RAG Search** | ~5-15s | Deep research, fact-checking, technical lookups |
| **Simple Search** | ~1s ⚡ | Quick facts, getting URLs, version checks |
| **Web Reader** | ~3-10s | Reading documentation, articles, blog posts |
| **News Search** | ~5-15s | Current events, breaking news, announcements |

Each request costs **$0.05** from your PipeLLM balance.

## 📖 How It Works

This is a **pure skill** (no runtime code). It provides your coding agent with:

1. **Decision logic** — when to search vs. when to rely on existing knowledge
2. **Scenario-based selection** — which search type to use for different tasks
3. **API knowledge** — how to call PipeLLM's WebSearch API with `curl`/`fetch`
4. **Error handling** — how to deal with failures and guide users through setup

The agent uses its native HTTP tools to make API calls directly.

## 🔄 Updating

### Gemini CLI
```bash
gemini extensions update pipellm-websearch
```

### Codex / OpenCode
```bash
cd ~/.codex/pipellm-websearch && git pull
# or
cd ~/.config/opencode/pipellm-websearch && git pull
```

## 📄 License

MIT
