# rolecall

A cast of generic Claude Code agent roles. Each file in `agents/` is one subagent —
an analyst, a reviewer, an art director — written to be good at its craft and to
know nothing about your repository. What it *does* know is where to look: every
role opens by deferring to an `## Agent roles` section in your `AGENTS.md` or
`CLAUDE.md`, which names your commands, your paths and your conventions for that
role. The role brings the discipline; the repository brings the facts.

## The cast

**SDLC** — the eight phases of a change, each a separate agent so that the one who
builds is not the one who judges.

- **analyst** — turns an informal ask into a numbered, testable spec
- **architect** — turns a spec into a plan and a conflict-free work breakdown
- **implementer** — builds exactly one scoped work item and stops
- **reviewer** — reads one diff adversarially against the requirements it claims
- **verifier** — runs the changed system and proves the criteria with pasted output
- **historian** — reconciles docs, changelog and tracker with what the code did
- **integrator** — probes an unfamiliar repo and writes down how it actually works
- **ops** — carries a finished change toward release, rollback plan included

**Product and design**

- **product-manager** — sweeps the backlog against the north star and proposes one bet
- **business-analyst** — turns a fuzzy business ask into structured requirements
- **designer** — critiques or specifies a screen, flow or component
- **ux-researcher** — represents the user who is not in the room
- **art-director** — makes the thing look like someone cared, with the reasons said out loud

**Research and naming**

- **market-researcher** — sizes markets and maps competitors with sourced evidence
- **name-reviewer** — kills weak names adversarially and never proposes replacements

**Publishing and ops**

- **copywriter** — writes the words a user encounters, with rationale and alternatives
- **content-author** — drafts one public piece, every claim registered to its evidence
- **prose-editor** — copy pass that removes the tics of machine-written prose
- **community-steward** — triages a public tracker; drafts replies, never posts them
- **market-intel** — standing competitor watch, reported as deltas with sources
- **metrics-analyst** — one-page recurring ops brief: what needs attention, what needs a call

**Trip research** — the same evidence discipline pointed at something that is not code.

- **trip-scout** — researches candidates and returns entries carrying a source and a date
- **fact-checker** — re-verifies prices and hours that have gone stale, and reports the deltas

## Install

As a plugin:

```
/plugin marketplace add nathancrtr/rolecall
/plugin install rolecall@rolecall
```

The agents then appear as `rolecall:<name>` — `rolecall:implementer`, and so on.

Or symlink the directory into your user scope, where they load under bare names in
every session:

```
ln -s /path/to/rolecall/agents ~/.claude/agents
```

## The `## Agent roles` convention

A role stays generic because your repository supplies the specifics. Add a section
to `AGENTS.md` (or `CLAUDE.md`) with one `###` entry per role you use. It is already
in an agent's context, and it wins wherever it conflicts with the role file.

```markdown
## Agent roles

### implementer

* Setup is `uv sync`; never `pip install` into the ambient environment.
* Run the suite as `python -m tools.run_tests`, never a bare `pytest` — the
  wrapper strips deployment variables that a bare run would read.
* Work lands on a branch off `main`; `main` is protected.
* Requirement IDs come from `docs/REQUIREMENTS.md` (`R-nn`); cite the governing
  ID in the comment and in your report.
* `src/cli.py` is the collision point — check with the dispatcher before
  touching it.
* Generated files under `dist/` are never hand-edited; run `make render`.
```

Write the facts an agent would otherwise guess: the exact commands, the paths that
matter, the one rule that is non-negotiable. Where a role has no entry, it works
from your general guidance and says so whenever a repo fact would have changed a
decision.

## Overriding a role

Prefer an `### <name>` entry — it is smaller, and it survives upgrades. Copy a role
into `.claude/agents/<name>.md` only when the **frontmatter** itself must differ for
your repo: a narrower tool list, a pinned model, a changed description. A copy
shadows the plugin role by name, so it is a full copy, and it should carry a line
recording what it forked from:

```
extends: rolecall/implementer@<commit>
```

## A note on the SDLC names

The eight SDLC names deliberately coincide with the roles rendered by
[gateline](https://github.com/nathancrtr/gateline), a framework that runs those
phases as a gated pipeline. In a gateline host repository, the files rendered into
that repo's `.claude/agents/` override these by name, and that is intended: the
rendered role is bound to that pipeline's contracts and gates, while these are the
free-standing versions for every other repository.

## License

Apache-2.0. See [LICENSE](LICENSE).
