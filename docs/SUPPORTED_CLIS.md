# Supported CLIs

Career-ops is AI-agnostic and runs on several command-line agent tools. The core logic is shared via `AGENTS.md`, while CLI-specific nuances are handled through entry wrappers in the repository root.

| CLI | Entry File | How to Invoke |
| --- | --- | --- |
| Claude Code | `CLAUDE.md` | Interactive: `claude` (then `/career-ops`). Headless/Batch: `claude -p "prompt"` |
| Cursor | `AGENTS.md` | Interactive: open the project in Cursor and ask for `career-ops` (skill entrypoint at `.cursor/skills/career-ops/SKILL.md`) |
| Codex | `CODEX.md` (see [`docs/CODEX.md`](CODEX.md)) | Interactive: `codex` (then use plain text). Headless/Batch: `codex exec "prompt"` |
| OpenCode | `OPENCODE.md` | Interactive: `opencode` (then `/career-ops`). Headless/Batch: `opencode run "prompt"` |
| Antigravity CLI | `AGENTS.md` | Interactive: `agy` (then `/career-ops`). Headless/Batch: `agy -p "prompt"` |
| Grok Build CLI | `AGENTS.md` | Interactive: `grok` (then `/career-ops`). Headless/Batch: `grok -p "prompt"` |
| Qwen | `AGENTS.md` | Interactive: `qwen`. Headless/Batch: `qwen -p "prompt"` |
| Kimi | `KIMI.md` | Interactive: `kimi` |
| GitHub Copilot CLI | `AGENTS.md` | Headless/Batch: `copilot -p "prompt"` |
| Gemini | `GEMINI.md` | Legacy wrapper redirecting to `AGENTS.md` (transitioned to Antigravity CLI). |
| Hermes Agent | `AGENTS.md` | Interactive: open the checkout in a Hermes session (see [below](#hermes-agent)) |

## Hermes Agent

Run Hermes with the checkout as the session's working directory. Two Hermes-specific details:

- **Load the router skill.** Project skills load only once the checkout is trusted: run `hermes skills trust` inside the repo. The router at `.agents/skills/career-ops/SKILL.md` then loads for sessions in that directory, and the modes work as they do under any other CLI.
- **`AGENTS.md` and scanner-based hosts.** Hermes scans project-context files for prompt injection before they reach the model, and drops the whole file on a match. The scan anchors on attack strings, so a rule that quotes one literally, even inside a sentence forbidding it, blocks the file for those users. Describe such phrasing rather than quoting it, and treat the skill route above as the reliable entry point.

Hermes is interactive-only here: nothing in this repository drives a `hermes` binary headlessly, so the batch runner stays Claude Code-specific.
