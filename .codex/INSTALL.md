# Installing PipeLLM WebSearch for Codex

## Prerequisites

- Git

## Installation

1. **Clone the repository (pinned to stable release):**
   ```bash
   git clone --branch v1.0.0 --depth 1 https://github.com/PipeLlm-AI/pipellm-websearch-skill.git ~/.codex/pipellm-websearch
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
cd ~/.codex/pipellm-websearch && git fetch --tags && git checkout v1.0.0
```

Replace `v1.0.0` with the latest release tag from [Releases](https://github.com/PipeLlm-AI/pipellm-websearch-skill/releases).

## Uninstalling

1. Remove the symlink:
   ```bash
   rm ~/.agents/skills/pipellm-websearch
   ```

2. Remove the cloned directory:
   ```bash
   rm -r ~/.codex/pipellm-websearch
   ```
