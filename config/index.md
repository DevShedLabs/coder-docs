# Configuration

Settings are stored at `~/.coder/config.json`. Created with defaults on first launch; editable directly to add providers or models without opening the settings UI.

```json
{
  "api_keys": {
    "fireworks": "fw-...",
    "xai": ""
  },
  "providers": {
    "fireworks": {
      "default": "accounts/fireworks/models/deepseek-v4-flash",
      "models": [
        { "id": "accounts/fireworks/models/deepseek-v4-flash", "label": "DeepSeek-V4-Flash ($0.45)", "contextWindow": 164000 }
      ]
    }
  }
}
```

## Where things live under `~/.coder/`

| Path | Purpose |
|---|---|
| `config.json` | API keys, model lists, editor preferences, keybindings |
| `harness.md` | Guardrails always appended to the system prompt, see [AI Agent](../ai/index.md) |
| `prompts/*.md` | Custom prompts, see [AI Agent](../ai/index.md) |
| `skills/<name>/SKILL.md` | Progressive-disclosure skills, see [Skills](../skills/index.md) |
| `connections/databases.json` | Global database connections, see [Databases](../databases/index.md) |
| `connections/sftp.json` | Global SFTP connections, see [SFTP](../sftp/index.md) |
| `themes/<id>/ui.css`, `editor.json` | Custom themes, see [Themes](../themes/index.md) |
| `recorder.db` | Full request/response recordings, see [Reports](../reports/index.md) |
| `global-board.json` | Master Board cards not tied to any project, see [Master Board](../masterboard/index.md) |
| `projects/{id}/token-log/{date}.jsonl` | Per-round token logs, see [Token Usage Dashboard](../tokens/index.md) |
| `projects/{id}/debugger/{timestamp}.jsonl` | Recorded debug sessions, see [Debugger](../debugger/index.md) |
| `docs/` | This documentation, mirrored from the public coder-docs repo |

## Per-project files

| Path | Purpose |
|---|---|
| `{project-root}/board.json` | Kanban board, see [Kanban Board](../kanban/index.md) |
| `{project-root}/connections/databases.json` | Project-scoped database connections |
| `{project-root}/connections/sftp.json` | Project-scoped SFTP connections |
| `{project-root}/.coder/memory/*.md` | AI project memory, see [AI Agent](../ai/index.md) |
| `{project-root}/.coder/orchestration/runs/<runId>/` | Orchestrator run data, see [Orchestrator](../orchestrator/index.md) |

## Tech Stack

- Electron 42
- React 18 + TypeScript
- Vite 8 (Rolldown bundler)
- Monaco Editor (fully bundled, no CDN dependency)
- Zustand 5
- AI SDK v6 (`ai` + `@ai-sdk/fireworks`), 8 providers: Fireworks, xAI (Grok), Anthropic, Cerebras, Baseten, Together AI, OpenAI, OpenRouter
- `react-markdown` + `remark-gfm` + `remark-math`/`rehype-katex` (math rendering)
- `node-pty` + `xterm.js` (terminal)
- `ripgrep` (project search)
- `ws` + `micromatch` (Live Reload)
- `better-sqlite3` + `mysql2` + `pg` + `mongodb` + `ioredis` (Databases panel, five engine drivers, all running in the main process)
- `ssh2` (SFTP panel, SSH/SFTP client, runs in the main process)
- Go LSP sidecar (language intelligence, see [Language Intelligence](../lsp/index.md))

[← Back to Docs](/docs/index.md)
