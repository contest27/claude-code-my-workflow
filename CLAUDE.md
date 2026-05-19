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

> **Slim-fork note (updated 2026-05-18, post Pedro v1.8.0 pull):** Framework principles (plan first, verify after, single source of truth, two-tier memory, [LEARN] tags, contractor mode after approval) live at `~/.claude/CLAUDE.md` in user scope and auto-load in every Claude Code session. This file is the **project-specific delta** only. See [`README.md`](README.md) for the slim-fork architecture and [`MAINTAINER-HANDBOOK.md`](MAINTAINER-HANDBOOK.md) for the re-slim workflow.

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

# Surface-count sync (README ↔ CLAUDE.md ↔ guide ↔ landing page)
./scripts/check-surface-sync.sh
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

Enforced by `/commit` (halts + asks for override); not enforced by a git pre-commit hook.

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [LectureN]` | Render Quarto + sync to docs/ |
| `/extract-tikz [LectureN]` | TikZ → PDF → SVG |
| `/new-diagram [snippet] [output.tex]` | Scaffold a TikZ diagram from the gallery with prevention + review |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/review-r [file]` | R code quality review |
| `/qa-quarto [LectureN]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer → Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/create-lecture` | Full lecture creation |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/review-paper [file]` | Manuscript review (single-pass / `--adversarial` / `--peer <journal>` simulated pipeline) |
| `/respond-to-referees [report] [manuscript]` | R&R cross-reference + response draft |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/audit-reproducibility [paper]` | Enforce replication tolerance thresholds on paper ↔ code |
| `/learn [skill-name]` | Extract discovery into persistent skill |
| `/context-status` | Show session health + context usage |
| `/deep-audit` | Repository-wide consistency audit |
| `/permission-check` | Diagnose permission layers when prompts fire unexpectedly |
| `/seven-pass-review` | Seven-pass adversarial manuscript review (parallel forked subagents) |
| `/verify-claims [file]` | Chain-of-Verification fact-check (forked verifier, fresh context) |
| `/checkpoint [topic]` | Save a structured state snapshot before stopping or handing off |
| `/preregister [--style osf\|aspredicted\|aea-rct]` | Draft a preregistration document (OSF / AsPredicted / AEA RCT Registry) |

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
