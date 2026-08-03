# Kanban Board

- **Board view** full-screen kanban overlay with five columns: Backlog, To Do, In Progress, Review, Done
- **Sidebar strip** compact column preview always accessible from the activity bar
- **Cards** rich markdown card bodies with preview/edit toggle, status dropdown, and delete confirm
- **Drag-and-drop** move cards between columns with HTML5 drag
- **Search** filter cards across all columns from the board header; non-matching cards dim in place
- **AI-writable** board stored as `board.json` in the project root so the AI can read and update tasks directly; FS watcher syncs the UI instantly on external writes
- **Import from Tickets** one click turns a GitHub issue or PR into a card (see [Tickets](../tickets/index.md)); re-importing updates the same card instead of duplicating it, and never overwrites the column you've moved it to
- **Open-count badge** cards not in the last column are shown on the Kanban activity-bar icon, always live even while the panel is closed

Each project stores its board at `{project-root}/board.json`. The format is human-readable JSON that AI tools can write directly, useful for having the AI manage your task list. Add `board.json` to `.gitignore` if you don't want it committed.

See also [Master Board](../masterboard/index.md) for a cross-project view.

[← Back to Docs](/docs/index.md)
