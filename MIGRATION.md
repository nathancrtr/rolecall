# Migration status

What each repository's `.claude/agents/` still needs to carry now that the shared
roles exist in `agents/`. A repo file shadows the shared one by name, so "safe to
delete" means the shared file covers it; "keep an override" means the file should be
trimmed to only the repo-specific part.

## job-radar

**Safe to delete** — byte-identical to the shared file, or fully folded into it:

`art-director.md`, `business-analyst.md`, `copywriter.md`, `market-researcher.md`,
`name-reviewer.md`, `integrator.md`.

`name-reviewer.md` was seeded into the shared repo verbatim and turned out to carry no
job-radar nouns at all; the shared file is that role plus a generic pointer at a
repository's own naming brief and claims rules.

**Keep a thin override** — these roles were generalized, and the rules below were
dropped because they only mean something in job-radar.

- **designer** (2) — the `WEBAPP-*.md` document set as the design standard; the
  recorded card-surface decision (`DD-n`) that a critique may not silently reopen.
  Also the pointer to `roles/art-director.md` as the repo's own production contract,
  and the S1 digest cap of 10 as the floor a design operates under.
- **ux-researcher** (2) — D3 (no method may automate against a logged-in endpoint)
  and D1 (real career data must not reach a public artifact); the
  `WEBAPP-UX-RESEARCH.md` §6/§7 starting point and the two personas in
  `WEBAPP-REQUIREMENTS.md` §2.
- **analyst** (3) — the `F/S/C/O/P/D` and `WEB-nn` ID families and the documents that
  own them; the named non-negotiables (D2, D3, S1, C3) a spec may not require; the
  `ARCHITECTURE.md` / `PRODUCT-ARCHITECTURE.md` grounding.
- **architect** (4) — `roles/` as domain role contracts naming a tier, never a model
  ID (P1/C3), executed through `pipeline/roles/runner.py`; the `TenantContext`
  three-backend storage topology and `data/postings` versus `data/annotations`;
  `cli.py` as the known collision point; the `http.politeness` fairness class with
  `pipeline/ratelimit.py` and `pipeline/http.py`.
- **implementer** (8) — `uv` / `pyproject.toml` / `.venv` setup and the
  `Bash(uv *)` allowlist; `python -m tools.run_tests` by name; the `tenant` /
  `other_tenant` / `configured_tenant` fixtures; `JOB_RADAR_TEST_DATABASE_URL` versus
  `DATABASE_URL` and the scratch-Postgres runner; `docker-compose.dev.yml`, MinIO and
  the `JOB_RADAR_S3_*` variables; `--no-postgres`; the issue label vocabulary, the
  `gh` sub-issue invocation and the retired priority labels; the `PROPOSAL.md` §7 /
  `WEBAPP-REQUIREMENTS.md` §5 ID sources.
- **reviewer** (5) — the D2/D3/D4/S1/S2/C3/O2 violation table, including the two
  named excluded employers; `tools/check_citations.py` as the S2 gate that is not in
  CI; `http.politeness` and `pipeline/http.py`; `data/postings/` versus
  `data/annotations/`; the `git log` "led / owned / drove" rule.
- **verifier** (6) — `job_radar_test` versus `job_radar` and the
  `job_radar_scratch_database` marker; `JOB_RADAR_TEST_DATABASE_URL`; the
  `docker-compose.dev.yml` / MinIO / `R2Storage.from_env()` setup;
  `tools.check_citations --tenant ID`; `pipeline coverage --tiers` and
  `tools.discover_ats` with the `vendor: unknown` fallback;
  `tests/shared_config_test.py` as the "config, not code" signal.
- **historian** (5) — the named root documentation surface (`PROPOSAL.md`,
  `PRODUCT-ARCHITECTURE.md`, the `WEBAPP-*.md` set, `docs/PROVISIONING.md`,
  `roles/README.md`, `.env.example`, `docker-compose.dev.yml` headers); `docs/history/`,
  `research/` and `docs/audits/` as the record directories; the three tests that
  already assert the checkable claims (tables, backticked paths, documented
  commands); `tools/unclosed_claims.py` and its blind spot; the specific
  cheap-to-falsify commands.
- **ops** (6) — Fly.io with `fly.toml` / `fly.production.toml` and the deploy
  workflows; `/healthz`; Neon, R2, Clerk and Resend as the managed dependencies; the
  crons in `pipeline/worker.py` and the deleted scheduled workflows; the
  `docs/ENVIRONMENTS.md` §6 promotion contract; `.env.example` as the variable
  contract.
- **product-manager** (8) — the `ROADMAP.md` surface map (§1–§4 editable, §5
  append-only) and the `briefs/README.md` never-edit rule; Project 4's `Horizon` field
  and **Needs placing** column, the `priority:unranked` and `priority:P0-now` labels,
  and the 2026-08-09 retirement of the per-issue priority labels; the `gh issue
  create` plus `sub_issues` invocation and the type/area label vocabulary; the
  milestone layer retired 2026-08-21 (#583, `docs/history/epic-milestones.md`);
  `PRODUCT-ARCHITECTURE.md` as the design authority and its §7 exit clauses for the
  phase epics B–F; `tools.pr_flags` (including `--from-json`) and `pipeline coverage
  --tiers` as the sweep commands, with the two 2026-08-07 environment failures; `data/`,
  `artifacts/` and `watchlist/proposals/` as the O3 record directories; "tenant 0 is
  not a user".

## curricle

**Keep a thin override**: `art-director.md` (the Python renderer table, `theme.py` as
the design system, `DIRECTION.md`, the `build/` render loop, the private sibling
courses, the derived-data / no-LLM-on-request-path / `profile.FIELDS` constraints) and
`copywriter.md` (the approachable-commercial voice target, copy living in the named
renderers, the evidence-tier rule). Both bodies above the `## In this repo` line are
now the shared files.

## agent-pipeline

**Safe to delete**: `designer.md`, `ux-researcher.md`, `copywriter.md`,
`business-analyst.md`, `market-researcher.md` — the older copies, whose distinct
content (deliverable lists, discipline rules, escalation rules) is folded into the
shared files. Their `fact-verification` and `adversarial-discipline` skill references
are carried as inline instructions.

**Keep**: `architect.md`, `implementer.md`, `reviewer.md` are a different role family
from the shared ones of the same name (read-only architect, general-purpose
implementer, any-target adversarial reviewer) and must stay to shadow them.
`conductor.md`, `qa-tester.md` and `visual-engineer.md` have no shared equivalent.

## household, travel

**Safe to delete**: `fact-checker.md`, `trip-scout.md` in both repos — identical to
the shared files.

## textual-flow

**Safe to delete**: `prose-editor.md` — identical to the shared file.

## company-ops

**Safe to delete**: `community-steward.md`, `content-author.md`, `market-intel.md`,
`metrics-analyst.md` — all identical to the shared files.
