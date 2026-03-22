# Installing PipeLLM WebSearch for OpenCode

## Prerequisites

- Git

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/PipeLlm-AI/pipellm-websearch-skill.git ~/.config/opencode/pipellm-websearch
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.config/opencode/pipellm-websearch/skills ~/.agents/skills/pipellm-websearch
   ```

3. **Restart OpenCode** to discover the skills.

## Verify

```bash
ls -la ~/.agents/skills/pipellm-websearch
```

## Updating

```bash
cd ~/.config/opencode/pipellm-websearch && git pull
```

## Uninstalling

```bash
rm ~/.agents/skills/pipellm-websearch
rm -rf ~/.config/opencode/pipellm-websearch
```
