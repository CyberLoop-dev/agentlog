<p align="center">
  <img src="assets/banner.svg" alt="agentlog banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HTML-single%20file-f472b6?style=for-the-badge" alt="single file">
  <img src="https://img.shields.io/badge/dependencies-zero-8b5cf6?style=for-the-badge" alt="zero deps">
  <img src="https://img.shields.io/badge/100%25-local-22c55e?style=for-the-badge" alt="local">
  <img src="https://img.shields.io/badge/license-MIT-3b82f6?style=for-the-badge" alt="MIT">
</p>

**agentlog** turns a raw JSONL agent trace into a clean, searchable timeline. See every user message, assistant reply, tool call and tool result at a glance, instead of scrolling through walls of JSON.

## Use it

1. Open `index.html` in your browser (no server, no build).
2. Paste your trace, or drag a `.jsonl` file onto the box.
3. Filter by type, search, and click a card to collapse it.

Nothing is uploaded. Your traces never leave your machine.

## Input format

One JSON object per line. agentlog is forgiving and detects the type automatically:

```jsonl
{"role": "user", "content": "What is the tallest mountain in Europe?"}
{"type": "tool_call", "name": "web_search", "input": {"query": "tallest mountain Europe"}}
{"type": "tool_result", "name": "web_search", "output": "Mount Elbrus (5,642 m)..."}
{"role": "assistant", "content": "Mount Elbrus."}
```

| Detected as | When |
|-------------|------|
| `user`, `assistant`, `system` | `role` is set to that value |
| `tool_call` | `type` is `tool_call` / `tool_use`, or `tool_calls` exists |
| `tool_result` | `type` is `tool_result`, or `role` is `tool` |
| `event` | anything else |

The body is taken from the first of `content`, `text`, `message`, `input`, `arguments`, `output`, `result`. A plain JSON array of records works too.

## Features

- Color-coded timeline with per-type filter chips and counts
- Full-text search with highlighted matches
- Collapse or expand any card, or all at once
- Drag and drop files
- Invalid lines are reported, not fatal

## License

MIT
