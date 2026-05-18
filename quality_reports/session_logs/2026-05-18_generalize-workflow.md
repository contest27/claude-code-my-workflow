# Session log — Generalise workflow to user scope

**Date:** 2026-05-18
**Goal:** Extract the generic backbone of Sebastian's Bank Capital `.claude/` setup to user-scope `~/.claude/` so the framework auto-loads in every Claude Code project on this machine, without each project re-duplicating the boilerplate.
**Plan:** [`2026-05-18_generalize-workflow-HANDOFF.md`](../plans/2026-05-18_generalize-workflow-HANDOFF.md) (Sebastian-authored handoff brief, in-session execution rather than fresh-session)
**Status:** COMPLETED 2026-05-18 (all phases done; relocated to slim fork as workflow-meta history)

---

## Decisions logged (Phase 1)

| Decision | Value | Source |
|---|---|---|
| Upstream URL | `https://github.com/pedrohcgs/claude-code-my-workflow` | GitHub REST API on the fork (`gh` not installed; used `Invoke-RestMethod`) |
| Clone location | `C:\Users\P314966\workflow-template-upstream` | User Q1 answer |
| Calibration scope | Researcher + lecturer + supervisor (broadest) | User Q2 answer |
| Quality-gates handling | Concepts only at global; numbers per project | User Q3 answer |
| Global `MEMORY.md` | Yes — cross-project facts | User Q4 answer |

---

## Findings (Phase 1 — discovery)

Pedro's upstream is **substantially richer** than the Bank Capital `.claude/` tree. The handoff brief assumed Bank Capital was Pedro + Sebastian additions; in fact Bank Capital is Pedro minus lecture content plus paper-revision additions.

| Component | Pedro | Bank Capital | Pedro-only | Sebastian-only | Shared |
|---|---|---|---|---|---|
| Rules (.md) | 24 | 16 | 8 (Beamer/Quarto/TikZ/post-flight-verification/summary-parity) | 1 (revision-protocol) | 15 |
| Skills | 28 | 18 | 17 (lecture + advanced research) | 5 (paper-revision-specific) | 13 |
| Agents | 14 | 5 | 11 (lecture + peer-review pool) | 2 (theory-paper-reviewer + numerical-reviewer) | 3 |

Shared rules — mostly tiny diffs (header / path tweaks). Big diffs: `quality-gates.md` (125 lines — Sebastian's is Bank-Capital R3 specific; Pedro's is generic Quarto/R/Beamer advisory), `single-source-of-truth.md` (100), `knowledge-base-template.md` (134), `orchestrator-protocol.md` (44).

---

## Phase 3 deliverables (this session, so far)

- `C:\Users\P314966\.claude\CLAUDE.md` — 130 lines, three identities, generic principles, environment paths, pointers to `~/.claude/rules/`.
- `C:\Users\P314966\.claude\MEMORY.md` — cross-project facts (Sebastian's identity, RUG CT clock, workflow preferences, environment, Overleaf-Dropbox sync, framework lineage).

Rule promotions (copy verbatim from Pedro's, where appropriate) deferred to subsequent turns. MVP-first.

---

## Phase progression

- [x] Phase 1 — discovery (Pedro clone, diff, classification baseline)
- [x] Phase 2 — classification (incremental; happens as files are touched)
- [/] Phase 3 — author user-scope (CLAUDE.md + MEMORY.md done; rules pending)
- [ ] Phase 4 — slim Bank Capital `CLAUDE.md` (backup first; project-specific delta only)
- [ ] Phase 4.5 — slim `contest27/claude-code-my-workflow` GitHub fork (pending push permission)
- [ ] Phase 5 — `companion-instructions-claude-ai.md` for manual paste
- [ ] Phase 6 — verify global framework auto-loads in non-Bank-Capital project; Bank Capital still works

---

## Open questions

- Confirm `~/.claude/CLAUDE.md` actually auto-loads in every project on Windows Claude Code (Phase 6 verification).
- Skills / agents promotion: incremental as needed, per Sebastian's "broadest" scope choice — but how aggressively this session?
- Phase 4.5 (push slimmed fork to GitHub) — explicit Sebastian go/no-go before any push.

---

## Notes on the file-level diff

Sebastian's `revision-protocol.md` is the only rule he added that Pedro doesn't have. It's heavily Bank-Capital-R3-coupled (R3.N anchors, JMCB references) — STAYS project scope. The matching paper-revision skills (`referee-response`, `revision-decision`, `skeptical-referee`) are also project-scope today; they are reusable across any paper project but their promotion to user scope is deferred until Sebastian has a second paper actively in revision.

Sebastian's theory-paper-reviewer and numerical-reviewer agents are similarly cross-paper-reusable; promotion deferred for the same reason. Today the precedent is the matlab-reviewer pair (promoted 2026-05-18 earlier in the day) which is fully generic.

---

## End-of-session wrap-up (2026-05-18 evening)

All planned phases completed:

- [x] **Phase 1** — Pedro's upstream cloned (`https://github.com/pedrohcgs/claude-code-my-workflow`) + inventory + diff against Bank Capital `.claude/`.
- [x] **Phase 2** — Classification of rules/skills/agents (most of Pedro's content is generic baseline; Sebastian's Bank-Capital-specific items stay project-scope).
- [x] **Phase 3** — User-scope authoring: `~/.claude/CLAUDE.md` (119 lines, three identities), `~/.claude/MEMORY.md` (98 lines, cross-project facts), 12 generic rules promoted to `~/.claude/rules/`.
- [x] **Phase 4** — Bank Capital `CLAUDE.md` slimmed to project-specific delta (168 lines vs 172 original; generic content removed, current-state detail added). Backups at `CLAUDE.md.pre-generalize.bak` + `MEMORY.md.pre-generalize.bak`. Migration `[LEARN:meta]` entry appended to Bank Capital `MEMORY.md`.
- [x] **Phase 4.5** — `contest27/claude-code-my-workflow` GitHub fork slimmed: 12 rule deletions, `CLAUDE.md` Core-Principles section stripped, `MEMORY.md` stubbed, `README.md` slim-fork notice prepended, `pedrohcgs/claude-code-my-workflow` wired as `upstream` remote. Commit [`457402d`](https://github.com/contest27/claude-code-my-workflow/commit/457402d) pushed to `main`: 15 files changed, 51 insertions, 920 deletions.
- [x] **Phase 5** — `~/.claude/companion-instructions-claude-ai.md` authored (1633-char paste block for claude.ai Custom Instructions + Cowork).
- [x] **Phase 6 (Sebastian-verified)** — Fresh Claude Code session opened in Practice Theory Gap project folder. Confirmed user-scope `~/.claude/CLAUDE.md` auto-loads ("Sebastian Pfeil — research economist", three-contexts framing, plan-first / contractor-mode-after-approval); project-scope coexists correctly (picked up "Ella as coauthor").

---

## Post-completion: relocate to workflow-meta project (2026-05-18)

The session was executed in the Bank Capital project folder — but the work was about workflow generalisation, not Bank Capital. Sebastian asked to move the misfiled artifacts to the slim-fork repo where they belong as meta-history. Done:

- This session log moved from `Bank Capital/Latest Version/my-project/quality_reports/session_logs/` to `workflow-template-slim/quality_reports/session_logs/`.
- The plan (handoff brief) moved from `Bank Capital/.../plans/` to `workflow-template-slim/quality_reports/plans/`.
- Forwarding stubs left at the old Bank Capital paths.
- The slim fork's `CLAUDE.md` polished with a maintainer-view section at the bottom (dual-role: scaffolding above for new clones, maintainer view below for Sebastian iterating).
- `MEMORY.md` rewritten with workflow-meta history (slim commit hash, rules promoted vs retained, maintenance decisions, open items).
- Pending: commit + push these polish edits to `contest27/claude-code-my-workflow:main`.

---

## Outstanding (post-session)

- **Companion claude.ai paste:** Sebastian to drop the in-file block from `~/.claude/companion-instructions-claude-ai.md` into claude.ai Custom Instructions + Cowork's equivalent field. Trim if the field rejects 1633 chars; in-file guide lists trim priorities.
- **Skills/agents promotion:** incremental, per-need. Don't bulk-promote.
- **Re-slim on next Pedro upstream push:** manual workflow documented in slim fork's `README.md` and `CLAUDE.md` maintainer view.

---

## What worked

- Pedro's `meta-governance.md` rubric ("Would a biology PhD student forking the workflow for lab protocols benefit from this knowledge?") cleanly resolved the generic-vs-specific question for every file.
- The matlab-reviewer/review-matlab pair promoted earlier in the day was the worked precedent that proved user-scope auto-load works on this Windows host.
- Manual diff against Pedro's freshly-cloned upstream (rather than relying on git history) gave a clean baseline for classification — Pedro's content IS the generic baseline; Sebastian's fork is Pedro minus lecture content plus paper-revision additions.

## What was less obvious upfront

- Sebastian's GitHub fork (`contest27/claude-code-my-workflow`) was at PR #35 — about 7 PRs behind Pedro's `main`. Re-syncing was out of scope for the slim work; the fork was slimmed AS-IS at its current commit, not after a Pedro-pull.
- The session being executed inside the Bank Capital folder meant the plan and session log got misfiled there. Sebastian caught this and asked to relocate (this section captures that work).
- The `CLAUDE.md` and `MEMORY.md` in the slim fork are dual-role: scaffolding for new clones + maintainer view for Sebastian iterating on the slim. The dual-role pattern is explicit in both files (maintainer section clearly delimited; instructions for new clones to delete it).
