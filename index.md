# DevShed Coder Docs

A fast, lightweight desktop code editor with an integrated AI agent, Git UI, GitHub issues/PRs, terminal, a database viewer/editor, an SFTP client, and project tools. Think VS Code without the bloat.

### [AI Agent](ai/index.md)
Streaming chat, multiple providers, tool use, extended thinking, voice dictation, and live editor streaming.

### [Skills](skills/index.md)
Progressive-disclosure instructions the agent loads on demand, shared by chat and the Orchestrator.

### [Orchestrator](orchestrator/index.md)
Multi-agent pipeline that plans, builds, and reviews a goal with a team of agents.

### [Token Usage Dashboard](tokens/index.md)
Per-round token logging, daily/session/7-day breakdowns, and a rebuild-from-history tool.

### [Reports (Request/Response Recorder)](reports/index.md)
Every AI round recorded verbatim to SQLite — full prompts, responses, and tool calls, exportable to Markdown/HTML.

### [Language Intelligence (LSP)](lsp/index.md)
Hover docs, go-to-definition, autocomplete, and diagnostics via real language servers.

### [Debugger](debugger/index.md)
Multi-language step-debugging (Node, Go, Rust, Python, PHP) over the Debug Adapter Protocol.

### [Terminal](terminal/index.md)
Integrated PTY terminal with multiple renameable tabs.

### [Smart Search](search/index.md)
Ripgrep-powered project-wide search and replace.

### [Git](git/index.md)
Status, stage/unstage, commit, push/pull/fetch, branch management, and discard changes.

### [Tickets](tickets/index.md)
GitHub issues and pull requests, connected to your project's own git remote.

### [Databases](databases/index.md)
SQLite, MySQL, PostgreSQL, MongoDB, and Redis behind one connection tree and query console.

### [SFTP](sftp/index.md)
Edit remote files over SFTP as real Monaco tabs.

### [Live Reload](livereload/index.md)
Watch files and refresh a browser tab or in-app preview automatically on save.

### [In-App Browser](browser/index.md)
A real editor tab that's a sandboxed embedded browser, split it alongside your code.

### [Kanban Board](kanban/index.md)
Per-project task board stored as plain JSON so the AI can read and write it directly.

### [Master Board](masterboard/index.md)
Cross-project task index that aggregates every project's Kanban board into one view.

### [Mindmaps](mindmaps/index.md)
Plain-text `.mindmap.md` files with an interactive canvas view.

### [Math Formulas](math/index.md)
LaTeX math via KaTeX, anywhere Coder renders markdown.

### [Themes](themes/index.md)
Independent UI and editor color themes, plus custom themes loaded from disk.

### [Configuration](config/index.md)
Where settings, prompts, and connections live on disk.

### [Shortcuts & Workflows](shortcuts/index.md)
The full keyboard shortcut reference.
