# Cybr Agent

Cybr Agent is CybrFlux's AI agent: it works in your terminal, in a desktop app and over messaging,
runs tasks with real tools, and keeps skills and memory between sessions.

## Install (macOS, Apple Silicon)

```bash
HERMES_REPO_URL=https://github.com/CybrFlux/cybr-agent-cli.git \
  bash <(curl -fsSL https://raw.githubusercontent.com/CybrFlux/cybr-agent-cli/main/scripts/install.sh) --channel main
```

Open a new Terminal window, then:

```bash
cybr setup      # pick a model and add its API key
cybr            # start chatting
```

## Everyday commands

| Command | What it does |
|---|---|
| `cybr` | Start an interactive chat |
| `cybr setup` | First-time setup wizard |
| `cybr model` | Change the model or provider |
| `cybr update` | Update to the latest Cybr Agent |
| `cybr doctor` | Check that everything is healthy |
| `cybr desktop` | Open the desktop app |
| `cybr gateway` | Run the messaging gateway (Telegram, Slack, and more) |

## Updates

`cybr update` pulls the latest release. Updates keep the Cybr Agent name, icons and wording.

---
CybrFlux · MIT licensed — see `LICENSE`.
