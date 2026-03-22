# Installing PipeLLM WebSearch for Codex

## Prerequisites

- Git

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/PipeLlm-AI/pipellm-websearch-skill.git ~/.codex/pipellm-websearch
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/pipellm-websearch/skills ~/.agents/skills/pipellm-websearch
   ```

3. **Restart Codex** to discover the skills.

## Verify

```bash
ls -la ~/.agents/skills/pipellm-websearch
```

## Updating

```bash
cd ~/.codex/pipellm-websearch && git pull
```

## Uninstalling

```bash
rm ~/.agents/skills/pipellm-websearch
rm -rf ~/.codex/pipellm-websearch
```
