# Cybr Agent CLI Reference

Live sources when anything looks stale: `cybr --help`, `cybr <command> --help`,
https://hermes-agent.nousresearch.com/docs/reference/cli-commands

### Global Flags

```
hermes [flags] [command]        (no subcommand = interactive chat)

  --version, -V             Show version
  -z, --oneshot PROMPT      One-shot: print ONLY the final response (for scripts/pipes)
  -m MODEL  --provider P    Model/provider override for this invocation
  -t, --toolsets LIST       Comma-separated toolsets for this invocation
  --resume, -r SESSION      Resume session by ID or title
  --continue, -c [NAME]     Resume by name, or most recent session
  --worktree, -w            Isolated git worktree mode (parallel agents)
  --skills, -s SKILL        Preload skills (comma-separate or repeat)
  --profile, -p NAME        Use a named profile
  --yolo                    Skip dangerous command approval
  --tui / --cli             Force the Ink TUI / classic REPL
  --ignore-rules            Skip AGENTS.md/SOUL.md/memory/skill injection
  --safe-mode               Disable ALL customizations (troubleshooting)
  --pass-session-id         Include session ID in system prompt
```

### Chat

```
cybr chat [flags]
  -q, --query TEXT          Single query, non-interactive
  --image PATH              Attach a local image to a single query
  -Q, --quiet               Suppress banner, spinner, tool previews
  --checkpoints             Enable filesystem checkpoints (/rollback)
  --max-turns N             Cap tool-calling iterations
  --source TAG              Session source tag (default: cli)
```
(plus the global flags above)

### Configuration

```
cybr setup [section]      Wizard (model|tts|terminal|gateway|tools|agent)
cybr model                Interactive model/provider picker
cybr fallback [add|remove|list]  Fallback provider chain
cybr config [show|edit|get|set|unset|path|env-path|check|migrate]
cybr login / logout       OAuth sign-in / clear stored auth
cybr doctor [--fix]       Check dependencies and config
cybr status [--full]      Component summary (--full: every section)
```

### Tools & Skills

```
cybr tools [list|enable NAME|disable NAME]   Per-platform toolsets (curses UI with no args)

cybr skills list|browse|search QUERY|inspect ID
cybr skills install ID    Hub identifier OR a direct https://…/SKILL.md URL
cybr skills config        Enable/disable skills per platform
cybr skills check|update|uninstall|publish PATH
cybr skills tap add REPO  Add a GitHub repo as a skill source
hermes bundles              Skill bundles (one /<name> alias loads several skills)
```

### MCP Servers

```
cybr mcp add NAME (--url or --command) | remove | list | test NAME
cybr mcp catalog | install NAME     Curated catalog install
cybr mcp configure NAME             Toggle tool selection
cybr mcp serve                      Run Cybr Agent as an MCP server
```
Details (transport, tool discovery, catalog): `references/native-mcp.md`.

### Gateway (Messaging Platforms)

```
cybr gateway run|install|start|stop|restart|status|setup
```

20+ platforms: Telegram, Discord, Slack, WhatsApp (Baileys + Business Cloud API), iMessage (Photon — `cybr photon setup`), Signal, Email, SMS, Matrix, Mattermost, Teams, LINE, SimpleX, ntfy, Google Chat, Home Assistant, DingTalk, Feishu, WeCom, Weixin, API Server, Webhooks. Open WebUI connects via the API Server adapter. Most adapters ship under `plugins/platforms/`.
Docs: https://hermes-agent.nousresearch.com/docs/user-guide/messaging/

### Sessions

```
cybr sessions list|browse|rename ID TITLE|delete ID|export OUT|prune|stats
```

### Cron / Webhooks

```
cybr cron list|create SCHED|edit ID|pause|resume|run ID|remove|status
    Schedules: '30m', 'every 2h', '0 9 * * *', ISO timestamp
cybr webhook subscribe NAME|list|remove NAME|test NAME
```
Webhook payloads/routes: `references/webhooks.md`.

### Profiles

```
cybr profile list|create NAME (--clone|--clone-all|--clone-from)|use|show|delete
hermes profile rename A B | alias NAME | export NAME | import FILE
cybr profile migrate-identity A B   Retry a completed rename's session/routing identity migration
```

### Credentials & Pools

```
cybr auth                 Interactive credential manager
cybr auth add [PROVIDER]  Add OAuth or API-key credential (nous, openai-codex, qwen-oauth, …)
cybr auth list|remove P IDX|reset PROVIDER|status
```
Multiple credentials per provider form a pool that rotates automatically and skips exhausted keys.

### Other

```
cybr desktop / gui        Native desktop app
cybr dashboard            Web admin panel + embedded chat (--stop / --status)
cybr proxy                OpenAI-compatible local proxy backed by an OAuth provider
cybr portal               Quick setup / sign in via Nous Portal
cybr kanban <verb>        Multi-agent work-queue board
cybr project              Named multi-folder workspaces
cybr skin list|use|set    Switch/tweak skins (see references/themes.md)
cybr pets <verb>          Pet mascots (see references/petdex.md)
cybr memory setup|status|off|reset   Memory provider
cybr secrets bitwarden|onepassword   External secret stores
cybr moa                  Mixture-of-Agents slots
cybr hooks / security / backup / import / checkpoints / console
cybr logs [-f] [errors]   View agent/error logs
cybr send                 One-off message through a gateway platform
cybr pairing / plugins / insights / journey / computer-use
cybr acp                  ACP server (IDE integration)
cybr completion bash|zsh|fish
cybr update / uninstall / claw migrate
```

Plugin- and provider-supplied subcommands (e.g. `cybr photon setup`) only appear once their plugin is installed/active.

### Where to Find Things

| Looking for... | Location |
|---|---|
| Config options | `cybr config edit` · [Configuration docs](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) |
| Tools / toolsets | `cybr tools list` · [Tools reference](https://hermes-agent.nousresearch.com/docs/reference/tools-reference) |
| Skills catalog | `cybr skills browse` · [Skills catalog](https://hermes-agent.nousresearch.com/docs/reference/skills-catalog) |
| Provider setup | `cybr model` · [Providers guide](https://hermes-agent.nousresearch.com/docs/integrations/providers) |
| Env variables | `cybr config env-path` · [Env vars reference](https://hermes-agent.nousresearch.com/docs/reference/environment-variables) |
| Gateway logs | `~/.hermes/logs/gateway.log` (or `cybr logs`) |
| Sessions | `cybr sessions browse` (reads state.db) |
