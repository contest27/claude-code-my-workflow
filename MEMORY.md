# Project Memory — Slim Fork (workflow-meta project)

Meta-history of Sebastian Pfeil's slim fork of `pedrohcgs/claude-code-my-workflow`. Project-specific `[LEARN]` entries about the fork's evolution accumulate here. Generic cross-project workflow lessons live at `~/.claude/MEMORY.md` (user scope).

> **For new project clones:** Wipe everything below and start fresh. The maintainer-history entries don't apply to your downstream project.

---

## Project Context

[LEARN:project] **Purpose.** This repo is Sebastian's slim fork of Pedro Santanna's `claude-code-my-workflow` template. Slimmed on 2026-05-18 to ship project scaffolding only; the framework backbone lives at user scope `~/.claude/`. New projects clone from this fork as their bootstrap; the framework auto-loads from user scope when Claude Code runs on Sebastian's machine.

[LEARN:project] **Upstream:** [`pedrohcgs/claude-code-my-workflow`](https://github.com/pedrohcgs/claude-code-my-workflow) (Pedro Santanna). Wired as `git remote add upstream` on 2026-05-18 for pulls. As of 2026-05-18 evening, fork is synced with Pedro through v1.8.0 (commit `e07d935`, PR #104).

[LEARN:project] **Slim commits on this fork:**
- [`457402d` initial slim](https://github.com/contest27/claude-code-my-workflow/commit/457402d) — 12 rules + CLAUDE.md core + MEMORY.md template-history removed.
- [`a379acb`](https://github.com/contest27/claude-code-my-workflow/commit/a379acb) — workflow-meta layer (dual-role CLAUDE.md / MEMORY.md, plan + session log relocated from Bank Capital).
- [`0f84967`](https://github.com/contest27/claude-code-my-workflow/commit/0f84967) — MAINTAINER-HANDBOOK.md.
- [`ffcfae6`](https://github.com/contest27/claude-code-my-workflow/commit/ffcfae6) — Pull Pedro v1.2.0 → v1.8.0; re-slim.
- (this commit) — Promote 4 new rules to user scope; handbook polish reflecting v1.8.0 re-slim lessons.

[LEARN:project] **Fork origin:** This is Sebastian's fork. Sebastian's GitHub handle is `contest27`. Pedro Santanna's is `pedrohcgs`.

---

## Rules Promoted to User Scope

[LEARN:project] **Sixteen generic rules at `~/.claude/rules/`:**

Initial 12 (2026-05-18):

| Rule | Why generic |
|---|---|
| `meta-governance.md` | Generic-vs-specific rubric — framework's self-description |
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

Additional 4 (2026-05-18, post-v1.8.0 re-slim):

| Rule | Why generic |
|---|---|
| `content-invariants.md` | Numbered invariants for content quality (path-scoped to lecture artifacts; dormant in non-lecture projects) |
| `cross-artifact-review.md` | Paper ↔ code dependency review pattern (path-scoped to manuscript files) |
| `post-flight-verification.md` | Chain-of-Verification anti-hallucination (path-scoped to skill files that produce factual claims) |
| `summary-parity.md` | Anti-whack-a-mole for summary paragraphs (universal — fires on docs and frontmatter descriptions) |

## Rules Retained at Fork Scope

[LEARN:project] **Eight rules kept at fork scope** (lecture-specific or paper-revision-specific):

| Rule | Reason |
|---|---|
| `beamer-quarto-sync.md` | Lecture-specific (Beamer ↔ Quarto parity protocol) |
| `no-pause-beamer.md` | Lecture-specific (Beamer overlay hygiene) |
| `tikz-visual-quality.md` | Lecture-specific (TikZ diagram standards) |
| `tikz-measurement.md` | Lecture-specific (added by Pedro v1.3.0) |
| `tikz-prevention.md` | Lecture-specific (added by Pedro v1.3.0) |
| `proofreading-protocol.md` | Not promoted — Bank Capital has a customised version |
| `replication-protocol.md` | Not promoted — domain-specific replication patterns |
| `knowledge-base-template.md` | Not promoted — heavy diff between Pedro's and Sebastian's variants |

## Skills and Agents

[LEARN:project] **Not yet promoted to user scope.** Pedro ships ~30 skills + 14 agents in this fork after v1.8.0. Only `review-matlab` (skill) and `matlab-reviewer` (agent) are at user scope so far, promoted 2026-05-18 morning as the worked precedent. Promote individual skills/agents to user scope when they're needed across projects.

---

## Maintenance Decisions

[LEARN:meta] **Manual re-slim chosen over `.gitattributes merge=ours`.** Pedro's update cadence is unpredictable; manual review when pulling upstream gives the maintainer visibility into what changed. Escalate to `merge=ours` only if cadence forces it.

[LEARN:meta] **Skills and agents stay at fork-scope by default** (rather than bulk-promote). Pedro has ~30 skills + 14 agents on his upstream after v1.8.0; bulk promotion is outside reasonable session time-boxes. Incremental promotion per project need.

[LEARN:meta] **Dual-role CLAUDE.md.** This repo's `CLAUDE.md` serves two audiences: (1) downstream users who clone the fork as a project bootstrap (scaffolding at top with `[YOUR PROJECT NAME]` placeholders), (2) Sebastian iterating on the slim fork itself (maintainer view at the bottom under a clear divider, instructing downstream users to delete it). Same pattern in `MEMORY.md`.

[LEARN:meta] **Workflow-meta project location.** The slim fork's local clone at `C:\Users\P314966\workflow-template-slim\` IS the workflow-meta project — when Sebastian opens Claude Code here, the maintainer view applies. The 2026-05-18 generalisation work was misfiled in Bank Capital's `my-project/quality_reports/` and relocated here; forwarding stubs at the old Bank Capital paths point here.

[LEARN:meta] **First re-slim: Pedro v1.2.0 → v1.8.0 pull (2026-05-18 evening).** 103 commits behind upstream; 111 files changed, 10K+ insertions. Merged via dedicated branch `reslim-2026-05-18-pedro-v1.8.0`. Conflicts: 3 modify/delete (re-deleted, user-scope authoritative); 2 content conflicts on CLAUDE.md / MEMORY.md (kept dual-role + selectively merged Pedro's improvements).

[LEARN:meta] **Lessons from the first re-slim** (codified in MAINTAINER-HANDBOOK Workflow 2):
- **Always branch for non-trivial pulls.** 100+ commits behind is non-trivial. Branch makes rollback trivial.
- **Conflict resolution pattern:** modify/delete on user-scope rules → re-delete (user scope wins); content conflicts on CLAUDE.md / MEMORY.md → keep our dual-role version + manually merge Pedro's improvements (new skill table rows, command updates, current-state samples).
- **Pedro's new files:** apply biology-PhD rubric. Promote what's generic; keep what's lecture-specific or has unresolved dependencies on fork-scope skills/agents.
- **Path-scoping enables aggressive promotion.** Rules with `paths:` frontmatter only fire when matching files exist — promoting a lecture-specific rule to user scope is harmless in non-lecture projects.

[LEARN:meta] **4-rule promotion (2026-05-18 evening, immediately after v1.8.0 re-slim).** `content-invariants`, `cross-artifact-review`, `post-flight-verification`, `summary-parity` promoted from fork scope to `~/.claude/rules/`. Rationale per rule: each has `paths:` frontmatter so it only fires when relevant; `summary-parity` is genuinely universal; the others either lecture-target (content-invariants, dormant in non-lecture projects) or skill-target (post-flight-verification fires when editing specific skill files). User-scope CLAUDE.md "Cross-cutting rules" table updated with all four.

[LEARN:meta] **Pedro's user-scope-relevant rule updates pending.** Pedro v1.3.0–v1.8.0 changed `orchestrator-protocol`, `quality-gates`, `r-code-conventions` in ways worth reviewing for incorporation into the user-scope copies (Pre-Flight Reports framing, Post-Flight Verification framing, Surface-Sync gate insights). Deferred — diff Pedro's vs user-scope in a follow-up session.

---

## Open Items

[LEARN:open] **Skills/agents promotion to user scope:** incremental, per project need.

[LEARN:open] **Reconcile user-scope rule updates from Pedro v1.8.0:** `orchestrator-protocol.md`, `quality-gates.md`, `r-code-conventions.md` at user-scope are at Pedro's pre-PR-#35 content; Pedro's newer versions are in `workflow-template-upstream/.claude/rules/` for diff.

[LEARN:open] **Re-slim on next Pedro push:** follow `MAINTAINER-HANDBOOK.md` Workflow 2.

[LEARN:open] **Companion claude.ai paste:** Sebastian to paste the contents of [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork field. 1633 chars; trim per the in-file guide if the field rejects.

[LEARN:open] **Wife's custom instructions:** drafted in the 2026-05-18 session; Sebastian to fill in name + language and paste into her account.

[LEARN:open] **Sebastian's fresh-session verification:** done 2026-05-18 in Practice Theory Gap project folder. The new-session response confirmed user-scope `~/.claude/CLAUDE.md` auto-loaded. Architecture works.
