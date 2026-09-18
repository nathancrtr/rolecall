# claude-agents

Single source for the Claude Code agent roles shared across every repository on this
machine. `~/.claude/agents` is a symlink to `agents/` here, so each role loads in every
session; a repository's own `.claude/agents/<name>.md` overrides the shared one by name,
and that is reserved for genuine specializations.

The gateline SDLC roles are **not** here: their source is `roles/` in the gateline repo,
rendered into each host by `gateline render`.

Roles reference a repository's conventions by pointing at its `AGENTS.md` / `CLAUDE.md`
rather than naming its files, so one file serves every repo.
