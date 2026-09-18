# claude-agents

Single source for the Claude Code agent roles shared across every repository on this
machine. `~/.claude/agents` is a symlink to `agents/` here, so each role loads in every
session; a repository's own `.claude/agents/<name>.md` overrides the shared one by name,
and that is reserved for genuine specializations.

The eight SDLC names here — `analyst`, `architect`, `implementer`, `reviewer`,
`verifier`, `historian`, `integrator`, `ops` — are Nathan's personal roles, for
repositories that are not gateline hosts. In a gateline host repo, the rendered files in
that repo's `.claude/agents/` (whose source is `roles/` in the gateline repo, rendered by
`gateline render`) override these by name, and that is intended.

Roles reference a repository's conventions by pointing at its `AGENTS.md` / `CLAUDE.md`
rather than naming its files, so one file serves every repo.
