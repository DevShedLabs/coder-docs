# Token Usage Dashboard

- **Per-round logging** every AI response round (including intermediate tool-call loops) is logged to `~/.coder/projects/{id}/token-log/{date}.jsonl`; captures the true cumulative cost, not just the final round
- **Today tab** total chat input/output and inline completion tokens for the current day, with a per-model breakdown table
- **Session tab** token totals and round count for the current chat session only
- **7-Day History tab** daily table of chat vs inline token consumption for the past week
- **Rebuild from History** scans all saved chat sessions and back-fills the token log; recovers data from sessions that predate live logging and lets you compare against provider billing
- **Title bar icon** always accessible from the coin icon in the top title bar

See also [Reports](../reports/index.md) for a full verbatim recorder of every request/response, not just token counts.

[← Back to Docs](/docs/index.md)
