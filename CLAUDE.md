# CLAUDE.md — Academic Project Development with Claude Code

<!-- HOW TO USE: Replace [BRACKETED PLACEHOLDERS] with your project info.
     Customize Beamer environments and CSS classes for your theme.
     Keep this file under ~200 lines — Claude loads it every session.
     See the guide at docs/workflow-guide.html for full documentation.
     The "Maintainer view" section at the bottom is for Sebastian's slim-fork
     work; delete it when adapting this file for your own project. -->

**Project:** [YOUR PROJECT NAME]
**Institution:** [YOUR INSTITUTION]
**Branch:** main

---

## Scope Discipline

**Do exactly what was asked — nothing adjacent.** Do not add README files, build scripts,
`.gitignore` edits, helper utilities, or extra tooling that was not requested. If an addition
looks valuable, **list it as a suggestion at the end** and let the user decide.

A request for a codebook is a request for a codebook. Delivering a codebook plus a README plus
build scripts plus gitignore edits means the user now has to review four things to accept one,
and the usual outcome is that all four get thrown away.

**Before adding anything not named in the request, ask.** One line is cheaper than a revert.

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- Beamer `.tex` is authoritative; Quarto `.qmd` derives from it
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to [MEMORY.md](MEMORY.md)

Cross-session context lives in [MEMORY.md](MEMORY.md); past plans, specs, and session logs are in [quality_reports/](quality_reports/).

**How we verify** — the references and rules that carry the verification discipline:

- [`verification-ladder.md`](.claude/references/verification-ladder.md) — the seven rungs, from *qualify the checker* to the external oracle, and how the review loop converges.
- [`external-oracle-process.md`](.claude/references/external-oracle-process.md) — running an independent frontier-model referee (Claude Code → GPT-5.6 Sol Pro) and adjudicating what it returns.
- [`provenance-and-ground-truth.md`](.claude/references/provenance-and-ground-truth.md) — naming and pinning your oracles, classifying divergence, and the clean-room boundary.
- [`review-fencing.md`](.claude/rules/review-fencing.md) — reviewer independence is a property of the environment, not an instruction: a neutral copy outside the checkout, prior verdicts withheld, and the answer keys the repo already commits fenced off.
- [`release-engineering.md`](.claude/references/release-engineering.md) — shipping research software: message and silent-resolution censuses, frozen feature matrices for ports, hash-claimed inherited tests, and downstream consumers pinned by commit SHA.

**How we write** — [`writing-with-ai.md`](.claude/rules/writing-with-ai.md): internal vs external-facing documents, why a model cannot make its own output stop reading as model output, and the human-readable standard for anything with your name on it.

**Theory work** — [`theory-proving.md`](.claude/references/theory-proving.md): proof contracts, portfolio search with isolated explorers, counterexample-hunting your own lemmas, adversarial audits, and the rule that an AI-generated proof is a claim, not a theorem.

**The laws** — [`research-agent-laws.md`](.claude/references/research-agent-laws.md): 21 laws for running agents on research infrastructure, each paid for by a real incident.

**How we remember** — the record lives in the repo, not the transcript:

- [`progress-reports.md`](.claude/rules/progress-reports.md) — GitHub issues as defect memory, `quality_reports/` as work memory, `MEMORY.md` as lesson memory.
- [`issue-ledger.md`](.claude/rules/issue-ledger.md) — the evidence standard an issue must meet, and the seven-section closure comment.
- [`repo-hygiene.md`](.claude/rules/repo-hygiene.md) — **scratch must not become main.** Enforced by `check-repo-hygiene.py` on every commit.

Nothing clears work until it has a row in [`quality_reports/qualification/LEDGER.md`](quality_reports/qualification/LEDGER.md) — run [`/vaccinate`](.claude/skills/vaccinate/SKILL.md) to put one there.

---

## Folder Structure

```
[YOUR-PROJECT]/
├── CLAUDE.MD                    # This file
├── .claude/                     # Project-scope rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers
├── Slides/                      # Beamer .tex files
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts + R code
├── quality_reports/             # Plans, session logs, merge reports, decision records
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report, decision-record, preregistration templates
└── master_supporting_docs/      # Papers and existing slides
```

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh LectureN

# Quality score
python scripts/quality_score.py Quarto/file.qmd

# Palette sync (LaTeX ↔ SCSS)
./scripts/check-palette-sync.sh

# Backtest: is the repo internally consistent and currently true?
# (surface-sync + skill-integrity + model-versions + links + spec-conformance + staleness + repo-hygiene + derived-counts + ledger-coverage + hook-battery)
# Run this after ANY change. Also runs in pre-commit and CI.
./scripts/backtest.sh
```

**Palette contract:** color names in `Preambles/header.tex` must match SCSS variables in `Quarto/theme-template.scss`. See [`Preambles/README.md`](Preambles/README.md).

---

## Quality Thresholds (advisory)

Generic concepts at [`~/.claude/rules/quality-gates.md`](file:///C:/Users/P314966/.claude/rules/quality-gates.md). Project-specific deduction tables and numeric thresholds go in the cloned project's own `.claude/rules/quality-gates.md` (path-scoped).

| Score | Checkpoint | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

Enforced by `/commit` (halts + asks for override) **and** — once you run `./scripts/install-hooks.sh` — by a real git pre-commit hook (`.githooks/pre-commit`) that runs the full backtest gate suite plus the quality (≥80) gate on every commit. Bypass sparingly with `SKIP_QUALITY_GATE=1` or `--no-verify`.

---

## Skills Quick Reference

The full table of all skills lives in [README.md](README.md#skills-claudeskills). Most-used, by workflow:

- **Slides / teaching:** `/create-lecture` `/compile-latex` `/deploy` `/qa-quarto` `/slide-excellence` `/syllabus` `/teach-from-paper` `/scaffold-exercises`
- **Papers / review:** `/review-paper` (`--peer`) `/seven-pass-review` `/respond-to-referees` `/verify-claims` `/proofread` `/humanize` `/submission-disclosures`
- **Data / reproducibility:** `/data-analysis` `/simulation-study` `/audit-reproducibility` `/diagnose` `/replication-package` `/capture-environment` `/power-analysis` `/disclosure-check`
- **Research / writing:** `/interview-me` `/lit-review` `/research-ideation` `/preregister` `/grant-proposal` `/data-management-plan`
- **Verification / rigor:** `/vaccinate` `/challenge` `/oracle-review` `/adjudicate-review` `/differential-audit` `/blast-radius` `/verify-artifact` `/credible-claims` `/deep-audit`
- **Meta / workflow:** `/commit` `/learn` `/new-skill` `/checkpoint` `/context-status` `/deep-audit` `/coauthor-brief` `/triage-inbox`

Stata (`/stata-replication`), R packages (`/r-package-check`), TikZ (`/extract-tikz`, `/new-diagram`), and more — see the README for the complete index.

---

<!-- CUSTOMIZE: Replace placeholder rows ([your-env], [.your-class]) with your own.
     Delete the rows marked "(example — delete)" once you've added yours. -->

## Beamer Custom Environments

| Environment | Effect | Use Case |
| --- | --- | --- |
| `[your-env]` | [Description] | [When to use] |
| `keybox` | Gold background box | Key points *(example — delete)* |
| `definitionbox[Title]` | Blue-bordered titled box | Formal definitions *(example — delete)* |

## Quarto CSS Classes

| Class | Effect | Use Case |
| --- | --- | --- |
| `[.your-class]` | [Description] | [When to use] |
| `.smaller` | 85% font | Dense content *(example — delete)* |
| `.positive` | Green bold | Good annotations *(example — delete)* |

---

## Current Project State

| Lecture | Beamer | Quarto | Key Content |
| --- | --- | --- | --- |
| HelloWorld *(sample — delete when ready)* | `HelloWorld.tex` | `HelloWorld.qmd` | Minimal deck to verify setup |
| 1: [Topic] | `Lecture01_Topic.tex` | `Lecture1_Topic.qmd` | [Brief description] |

---

> ## Maintainer view (workflow-meta project)
>
> **The section below applies when Sebastian opens this folder in Claude Code to iterate on the slim fork.** New users cloning this fork for a downstream project should delete everything from this divider to end-of-file (and replace the template placeholders above with their own project content).

### What this repo is (for maintainer work)

Sebastian's slim fork of [`pedrohcgs/claude-code-my-workflow`](https://github.com/pedrohcgs/claude-code-my-workflow). Slimmed 2026-05-18; re-slimmed same day after Pedro v1.2.0 → v1.8.0 pull (103 upstream commits, 111 files changed, 10K+ insertions). See [`quality_reports/session_logs/`](quality_reports/session_logs/) for build logs and [`quality_reports/plans/`](quality_reports/plans/) for plans.

Framework backbone (CLAUDE.md core principles, MEMORY.md universal patterns, 12 generic rules) lives at user scope `~/.claude/`, not here. This repo ships project scaffolding only.

### Maintenance loop (when Pedro pushes upstream)

```powershell
cd C:\Users\P314966\workflow-template-slim
git fetch upstream                                            # pedrohcgs/claude-code-my-workflow
git diff main upstream/main                                   # review what Pedro changed
git checkout -b reslim-YYYY-MM-DD                             # always branch for non-trivial pulls
git merge upstream/main                                       # accept the merge
# Re-delete the 12 framework rules (paths in MAINTAINER-HANDBOOK.md Workflow 2).
# Resolve CLAUDE.md / MEMORY.md conflicts: keep dual-role structure (our version),
# selectively merge Pedro's improvements (new skill rows in the table, etc.).
# Pedro's newly added files: keep if project-scaffolding or lecture-specific;
# promote to ~/.claude/ if generic backbone (use the biology-PhD rubric).
git add -A
git commit -m "Pull Pedro's <version> updates; re-slim"
git checkout main && git merge reslim-YYYY-MM-DD && git push origin main
```

Manual re-slim is the deliberate baseline. If Pedro's cadence picks up and re-slim becomes tedious, escalate to `.gitattributes` with `merge=ours` on the slimmed paths.

Full step-by-step in [`MAINTAINER-HANDBOOK.md`](MAINTAINER-HANDBOOK.md).

### Outstanding workflow-meta tasks

- **Companion paste:** drop the block in [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork field (1633 chars; trim per in-file guide if needed).
- **Skills/agents incremental promotion:** Pedro now ships ~30 skills + 14 agents in this fork after v1.8.0; only `review-matlab` + `matlab-reviewer` are at user scope so far. Promote per project need.
- **Reconcile user-scope rules with Pedro's v1.8.0 updates:** the user-scope versions of `orchestrator-protocol`, `quality-gates`, `r-code-conventions` are at Pedro's v1.2.0-era content; Pedro updated them since (Pre-Flight Reports, Post-Flight Verification, Surface-Sync gate). Diff and selectively pull updates.
- **Next re-slim:** on the next Pedro push (no schedule).

### Project-specific files in this repo

- [`quality_reports/plans/`](quality_reports/plans/) — slim-fork plans
- [`quality_reports/session_logs/`](quality_reports/session_logs/) — slim-fork session logs (2026-05-18 initial + re-slim addendum)
- [`MEMORY.md`](MEMORY.md) — slim-fork meta-history
- [`README.md`](README.md) — fork architecture, maintenance workflow, original Pedro README
- [`MAINTAINER-HANDBOOK.md`](MAINTAINER-HANDBOOK.md) — pinnable operating manual
