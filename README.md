# Agent Instructions Pack

This pack contains:

- `AGENTS.md` — canonical, cross-agent instructions (Claude, Codex, Cursor, etc.)
- `CLAUDE.md` — thin shim pointing at `AGENTS.md`
- `.cursor.rules.*.mdc` — refactored Cursor rules that:
  - defer to `AGENTS.md` for global standards
  - stay scoped and minimal for token efficiency

How to apply in your repo:
1) Copy `AGENTS.md` to the repo root.
2) Copy `CLAUDE.md` to the repo root (optional but recommended).
3) For Cursor:
   - Replace contents of `.cursor/rules/*.mdc` with the corresponding `.cursor.rules.*.mdc` files (rename to match your existing filenames).
