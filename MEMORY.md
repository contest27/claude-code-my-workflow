# Project Memory — Slim Fork (workflow-meta project)

Meta-history of Sebastian Pfeil's slim fork of `pedrohcgs/claude-code-my-workflow`. Project-specific `[LEARN]` entries about the fork's evolution accumulate here. Generic cross-project workflow lessons live at `~/.claude/MEMORY.md` (user scope).

> **For new project clones:** Wipe everything below and start fresh. The maintainer-history entries don't apply to your downstream project.

---

## Project Context

[LEARN:project] **Purpose.** This repo is Sebastian's slim fork of Pedro Santanna's `claude-code-my-workflow` template. Slimmed on 2026-05-18 to ship project scaffolding only; the framework backbone (CLAUDE.md core principles, MEMORY.md universal patterns, 12 generic rules) was hoisted to user scope `~/.claude/`. New projects clone from this fork as their bootstrap; the framework auto-loads from user scope when Claude Code runs on Sebastian's machine.

[LEARN:project] **Upstream:** [`pedrohcgs/claude-code-my-workflow`](https://github.com/pedrohcgs/claude-code-my-workflow) (Pedro Santanna). Wired as `git remote add upstream` on 2026-05-18 for future pulls. Fork was last synced at PR #35 (`3840e81 Merge pull request #35 from pedrohcgs/chore/template-cleanup`); Pedro has since added content the fork has not yet pulled (e.g., post-flight-verification rule, summary-parity rule, TikZ-prevention/measurement, content-invariants, cross-artifact-review).

[LEARN:project] **Slim commit:** [`457402d Slim template: framework now at user scope (~/.claude/)`](https://github.com/contest27/claude-code-my-workflow/commit/457402d) — 15 files changed, 51 insertions, 920 deletions. Pushed to `contest27/claude-code-my-workflow:main` on 2026-05-18.

[LEARN:project] **Fork origin:** This is Sebastian's fork, not Pedro's. Sebastian's GitHub handle is `contest27`. Pedro Santanna's is `pedrohcgs`.

---

## Rules Promoted to User Scope (2026-05-18)

[LEARN:project] **Twelve generic rules** moved from this fork's `.claude/rules/` to `~/.claude/rules/`:

| Rule | Why generic |
|---|---|
| `meta-governance.md` | The generic-vs-specific rubric — the framework's self-description |
| `plan-first-workflow.md` | Universal pattern |
| `orchestrator-protocol.md` | Contractor-mode loop |
| `orchestrator-research.md` | Research-mode variant |
| `session-logging.md` | Three-trigger pattern |
| `verification-protocol.md` | Compile/render/test |
| `single-source-of-truth.md` | Universal principle (path-scoped to Slides/Quarto for the lecture case) |
| `quality-gates.md` | Concept-only (advisory thresholds); project-specific deduction tables stay in projects |
| `exploration-fast-track.md` | Sandbox workflow |
| `exploration-folder-protocol.md` | Sandbox structure |
| `pdf-processing.md` | Safe PDF chunking |
| `r-code-conventions.md` | R coding standards |

## Rules Retained at Fork Scope

[LEARN:project] **Six rules kept** (lecture-specific or paper-revision-specific, not promoted to user scope yet):

| Rule | Reason |
|---|---|
| `beamer-quarto-sync.md` | Lecture-specific (Beamer ↔ Quarto parity) |
| `no-pause-beamer.md` | Lecture-specific (Beamer overlay hygiene) |
| `tikz-visual-quality.md` | Lecture-specific (TikZ diagram standards) |
| `proofreading-protocol.md` | Could go user-scope but not yet promoted — Sebastian's Bank-Capital project has a customised version |
| `replication-protocol.md` | Could go user-scope but not yet promoted — domain-specific replication patterns |
| `knowledge-base-template.md` | Could go user-scope but not yet promoted — heavy diff between Pedro's and Sebastian's variants |

## Skills and Agents

[LEARN:project] **Not yet promoted to user scope.** Pedro ships 22 skills + 10 agents in this fork. Only `review-matlab` (skill) and `matlab-reviewer` (agent) are at user scope so far, promoted 2026-05-18 morning as the worked precedent. Bulk promotion was deferred during the 2026-05-18 generalisation work to keep within the 3-hour time-box. Promote individual skills/agents to user scope when they're needed across projects.

---

## Maintenance Decisions

[LEARN:meta] **Manual re-slim chosen over `.gitattributes merge=ours`.** Pedro's update cadence is low; manual review when pulling upstream gives the maintainer visibility into what changed. Escalate to `merge=ours` only if Pedro's pace picks up. Decision recorded by Sebastian via the original handoff brief, Phase 4.5.

[LEARN:meta] **Skills and agents stay at fork-scope for now** (rather than bulk-promote). Pedro has 28 skills + 14 agents on his upstream; the fork-as-cloned has 22 skills + 10 agents (older). Bulk promotion would have required reading + classifying + adapting frontmatter for ~30 files in one session — outside the time-box. Incremental promotion as needed in future sessions.

[LEARN:meta] **Dual-role CLAUDE.md.** This repo's `CLAUDE.md` serves two audiences: (1) downstream users who clone the fork as their project bootstrap (scaffolding at top with `[YOUR PROJECT NAME]` placeholders), (2) Sebastian iterating on the slim fork itself (maintainer view at the bottom under a clear divider, instructing downstream users to delete it). Same pattern in `MEMORY.md`: meta-history at top, blank stub guidance for new clones at the top of the file.

[LEARN:meta] **Workflow-meta project location.** The slim fork's local clone at `C:\Users\P314966\workflow-template-slim\` IS the workflow-meta project — when Sebastian opens Claude Code here, the maintainer view applies. The 2026-05-18 generalisation work itself was misfiled in Bank Capital's `my-project/quality_reports/` because Claude Code was launched there; the plan and session log have been moved to `quality_reports/plans/` and `quality_reports/session_logs/` respectively. Forwarding stubs at the old Bank Capital paths point here.

---

## Open Items

[LEARN:open] **Skills/agents promotion to user scope:** incremental, as they're needed in non-Bank-Capital projects. Don't bulk-promote.

[LEARN:open] **Re-slim on next Pedro push:** unscheduled. When Pedro publishes new content, follow the manual re-slim workflow in `README.md` and `CLAUDE.md` (maintainer view).

[LEARN:open] **Companion claude.ai paste:** Sebastian to paste the contents of [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork field. 1633 chars; trim per the in-file guide if the field rejects.

[LEARN:open] **Sebastian's fresh-session verification:** done 2026-05-18 in Practice Theory Gap project folder. The new-session response confirmed user-scope `~/.claude/CLAUDE.md` auto-loaded ("Sebastian Pfeil — research economist", three-contexts framing, plan-first / contractor-mode-after-approval, project-scope picking up "Ella as coauthor"). Architecture works.
