# Project Memory — Slim Fork (workflow-meta project)

Meta-history of Sebastian Pfeil's slim fork of `pedrohcgs/claude-code-my-workflow`. Project-specific `[LEARN]` entries about the fork's evolution accumulate here. Generic cross-project workflow lessons live at `~/.claude/MEMORY.md` (user scope).

> **For new project clones:** Wipe everything below and start fresh. The maintainer-history entries don't apply to your downstream project.

---

## Project Context

[LEARN:project] **Purpose.** This repo is Sebastian's slim fork of Pedro Santanna's `claude-code-my-workflow` template. Slimmed on 2026-05-18 to ship project scaffolding only; the framework backbone (CLAUDE.md core principles, MEMORY.md universal patterns, 12 generic rules) was hoisted to user scope `~/.claude/`. New projects clone from this fork as their bootstrap; the framework auto-loads from user scope when Claude Code runs on Sebastian's machine.

[LEARN:project] **Upstream:** [`pedrohcgs/claude-code-my-workflow`](https://github.com/pedrohcgs/claude-code-my-workflow) (Pedro Santanna). Wired as `git remote add upstream` on 2026-05-18 for pulls. As of 2026-05-18 evening, fork is synced with Pedro through v1.8.0 (commit `e07d935`, PR #104).

[LEARN:project] **Slim commits:** [`457402d` initial slim](https://github.com/contest27/claude-code-my-workflow/commit/457402d) (2026-05-18; 12 rules + CLAUDE.md core + MEMORY.md template-history removed). Subsequent commits: [`a379acb`](https://github.com/contest27/claude-code-my-workflow/commit/a379acb) (workflow-meta layer with dual-role CLAUDE.md/MEMORY.md), [`0f84967`](https://github.com/contest27/claude-code-my-workflow/commit/0f84967) (MAINTAINER-HANDBOOK.md), v1.8.0 re-slim merge (this commit).

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

[LEARN:project] **Rules kept** (lecture-specific or paper-revision-specific, not promoted to user scope yet):

| Rule | Reason |
|---|---|
| `beamer-quarto-sync.md` | Lecture-specific (Beamer ↔ Quarto parity) |
| `no-pause-beamer.md` | Lecture-specific (Beamer overlay hygiene) |
| `tikz-visual-quality.md` | Lecture-specific (TikZ diagram standards) |
| `tikz-measurement.md` | Lecture-specific (added by Pedro v1.3.0; 2026-05-18 re-slim) |
| `tikz-prevention.md` | Lecture-specific (added by Pedro v1.3.0; 2026-05-18 re-slim) |
| `proofreading-protocol.md` | Could go user-scope but not yet promoted — Bank Capital has a customised version |
| `replication-protocol.md` | Could go user-scope but not yet promoted — domain-specific replication patterns |
| `knowledge-base-template.md` | Could go user-scope but not yet promoted — heavy diff between Pedro's and Sebastian's variants |
| `content-invariants.md` | Added by Pedro v1.6.0 (2026-05-18 re-slim); candidate for user-scope promotion later |
| `cross-artifact-review.md` | Added by Pedro v1.4.0 (2026-05-18 re-slim); candidate for user-scope promotion later |
| `post-flight-verification.md` | Added by Pedro v1.7.0 (2026-05-18 re-slim); candidate for user-scope promotion later |
| `summary-parity.md` | Added by Pedro v1.6.1 (2026-05-18 re-slim); candidate for user-scope promotion later |

## Skills and Agents

[LEARN:project] **Not yet promoted to user scope.** Pedro ships ~30 skills + 14 agents in this fork after v1.8.0. Only `review-matlab` (skill) and `matlab-reviewer` (agent) are at user scope so far, promoted 2026-05-18 morning as the worked precedent. Bulk promotion was deferred to keep within the 3-hour time-box. Promote individual skills/agents to user scope when they're needed across projects.

---

## Maintenance Decisions

[LEARN:meta] **Manual re-slim chosen over `.gitattributes merge=ours`.** Pedro's update cadence is unpredictable; manual review when pulling upstream gives the maintainer visibility into what changed. Escalate to `merge=ours` only if cadence forces it. Decision recorded by Sebastian via the original handoff brief, Phase 4.5.

[LEARN:meta] **Skills and agents stay at fork-scope for now** (rather than bulk-promote). Pedro has ~30 skills + 14 agents on his upstream after v1.8.0; bulk promotion would require reading + classifying + adapting frontmatter for ~40 files in one session — outside the time-box. Incremental promotion as needed in future sessions.

[LEARN:meta] **Dual-role CLAUDE.md.** This repo's `CLAUDE.md` serves two audiences: (1) downstream users who clone the fork as their project bootstrap (scaffolding at top with `[YOUR PROJECT NAME]` placeholders), (2) Sebastian iterating on the slim fork itself (maintainer view at the bottom under a clear divider, instructing downstream users to delete it). Same pattern in `MEMORY.md`: meta-history at top, blank stub guidance for new clones at the top of the file.

[LEARN:meta] **Workflow-meta project location.** The slim fork's local clone at `C:\Users\P314966\workflow-template-slim\` IS the workflow-meta project — when Sebastian opens Claude Code here, the maintainer view applies. The 2026-05-18 generalisation work itself was misfiled in Bank Capital's `my-project/quality_reports/` because Claude Code was launched there; the plan and session log were moved to `quality_reports/plans/` and `quality_reports/session_logs/` respectively. Forwarding stubs at the old Bank Capital paths point here.

[LEARN:meta] **First re-slim: Pedro v1.2.0 → v1.8.0 pull (2026-05-18 evening).** 103 commits behind upstream; 111 files changed, 10K+ insertions. Merged via dedicated branch `reslim-2026-05-18-pedro-v1.8.0`. Conflicts:
- **3 modify/delete** (`orchestrator-protocol`, `quality-gates`, `r-code-conventions` — Pedro modified them in v1.4.x – v1.7.x; we had deleted them in the initial slim). Resolved by re-deleting since the user-scope versions are authoritative. **Side-note:** Pedro's updates to these three are worth reviewing for incorporation into user-scope copies — deferred as a follow-up.
- **2 content conflicts** (`CLAUDE.md`, `MEMORY.md`). Kept the dual-role structure from our HEAD; selectively merged Pedro's improvements into the CLAUDE.md skills table (new entries: `/new-diagram`, `/respond-to-referees`, `/audit-reproducibility`, `/permission-check`, `/seven-pass-review`, `/verify-claims`, `/checkpoint`, `/preregister`), the "advisory" framing on Quality Thresholds, the HelloWorld sample row in Current Project State, and the new `check-palette-sync.sh` / `check-surface-sync.sh` commands.

Pedro's new content (kept at fork-scope for now): 6 new rules (`content-invariants`, `cross-artifact-review`, `post-flight-verification`, `summary-parity`, `tikz-measurement`, `tikz-prevention` — first four are user-scope candidates, deferred), 8 new skills, 4 new agents (`claim-verifier`, `domain-referee`, `editor`, `methods-referee`), `.claude/references/` folder (audit-pet-peeves, discipline-cards, journal-profiles, v1.9-backlog), `scripts/R/` template pipeline, `scripts/check-*.py` validators, HelloWorld sample (`Slides/HelloWorld.tex` + `Quarto/HelloWorld.qmd`), `CHANGELOG.md`, `TROUBLESHOOTING.md`, `.github/` (CONTRIBUTING, ISSUE_TEMPLATE, PR_TEMPLATE) + `.vscode/settings.json`.

[LEARN:meta] **Pedro's user-scope-relevant updates pending.** Pedro's v1.3.0–v1.8.0 changes to `orchestrator-protocol.md`, `quality-gates.md`, `r-code-conventions.md` were not pulled into `~/.claude/rules/` during the 2026-05-18 re-slim. Diff Pedro's vs user-scope copy in a follow-up session and selectively incorporate (e.g., Pre-Flight Reports framing, Post-Flight Verification, Surface-Sync gate insights from MEMORY.md/audit lessons).

---

## Open Items

[LEARN:open] **Skills/agents promotion to user scope:** incremental, as they're needed in non-Bank-Capital projects. Don't bulk-promote.

[LEARN:open] **Promote candidate new rules to user scope:** `content-invariants`, `cross-artifact-review`, `post-flight-verification`, `summary-parity` (Pedro v1.4.0–v1.7.0 additions). Currently at fork-scope; the TikZ ones (`tikz-measurement`, `tikz-prevention`) stay fork-scope.

[LEARN:open] **Reconcile user-scope rule updates from Pedro v1.8.0.** `orchestrator-protocol.md`, `quality-gates.md`, `r-code-conventions.md` at user-scope are at Pedro's pre-PR-#35 content; Pedro's newer versions are in `workflow-template-upstream/.claude/rules/` for diff.

[LEARN:open] **Re-slim on next Pedro push:** unscheduled. When Pedro publishes new content, follow `MAINTAINER-HANDBOOK.md` Workflow 2.

[LEARN:open] **Companion claude.ai paste:** Sebastian to paste the contents of [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork field. 1633 chars; trim per the in-file guide if the field rejects.

[LEARN:open] **Sebastian's fresh-session verification:** done 2026-05-18 in Practice Theory Gap project folder. The new-session response confirmed user-scope `~/.claude/CLAUDE.md` auto-loaded ("Sebastian Pfeil — research economist", three-contexts framing, plan-first / contractor-mode-after-approval, project-scope picking up "Ella as coauthor"). Architecture works.
