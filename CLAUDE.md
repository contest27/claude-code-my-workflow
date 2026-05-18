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

> **Slim-fork note (2026-05-18):** Framework principles (plan first, verify after, single source of truth, two-tier memory, [LEARN] tags, contractor mode after approval) live at `~/.claude/CLAUDE.md` in user scope and auto-load in every Claude Code session. This file is the **project-specific delta** only. See [`README.md`](README.md) for the slim-fork architecture and the maintenance workflow when Pedro pushes upstream updates.

---

## Folder Structure

```
[YOUR-PROJECT]/
├── CLAUDE.MD                    # This file
├── .claude/                     # Project-scope rules, skills, agents, hooks (most generics now at ~/.claude/)
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers
├── Slides/                      # Beamer .tex files
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts + R code
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report templates
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
```

---

## Quality Thresholds

Generic concepts at [`~/.claude/rules/quality-gates.md`](file:///C:/Users/P314966/.claude/rules/quality-gates.md). Project-specific deduction tables and numeric thresholds go in the cloned project's own `.claude/rules/quality-gates.md` (path-scoped).

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [LectureN]` | Render Quarto + sync to docs/ |
| `/extract-tikz [LectureN]` | TikZ → PDF → SVG |
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
| `/review-paper [file]` | Manuscript review |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/learn [skill-name]` | Extract discovery into persistent skill |
| `/context-status` | Show session health + context usage |
| `/deep-audit` | Repository-wide consistency audit |

---

<!-- CUSTOMIZE: Replace the example entries below with your own
     Beamer environments and Quarto CSS classes. -->

## Beamer Custom Environments

| Environment       | Effect        | Use Case       |
|-------------------|---------------|----------------|
| `[your-env]`      | [Description] | [When to use]  |

## Quarto CSS Classes

| Class              | Effect        | Use Case       |
|--------------------|---------------|----------------|
| `[.your-class]`    | [Description] | [When to use]  |

---

## Current Project State

| Lecture | Beamer | Quarto | Key Content |
|---------|--------|--------|-------------|
| 1: [Topic] | `Lecture01_Topic.tex` | `Lecture1_Topic.qmd` | [Brief description] |
| 2: [Topic] | `Lecture02_Topic.tex` | -- | [Brief description] |

---

> ## Maintainer view (workflow-meta project)
>
> **The section below applies when Sebastian opens this folder in Claude Code to iterate on the slim fork.** New users cloning this fork for a downstream project should delete everything from this divider to end-of-file (and replace the template placeholders above with their own project content).

### What this repo is (for maintainer work)

Sebastian's slim fork of [`pedrohcgs/claude-code-my-workflow`](https://github.com/pedrohcgs/claude-code-my-workflow). Slimmed 2026-05-18 — see [`quality_reports/session_logs/2026-05-18_generalize-workflow.md`](quality_reports/session_logs/2026-05-18_generalize-workflow.md) for the build log and [`quality_reports/plans/2026-05-18_generalize-workflow-HANDOFF.md`](quality_reports/plans/2026-05-18_generalize-workflow-HANDOFF.md) for the original plan.

Framework backbone (CLAUDE.md core principles, MEMORY.md universal patterns, 12 generic rules) lives at user scope `~/.claude/`, not here. This repo ships project scaffolding only.

### Maintenance loop (when Pedro pushes upstream)

```powershell
cd C:\Users\P314966\workflow-template-slim
git fetch upstream                                            # pedrohcgs/claude-code-my-workflow
git diff main upstream/main                                   # review what Pedro changed
git merge upstream/main                                       # accept the merge
# Manually delete framework files re-introduced by the merge — paths slimmed 2026-05-18:
#   .claude/rules/{meta-governance,plan-first-workflow,orchestrator-protocol,
#                  orchestrator-research,session-logging,verification-protocol,
#                  single-source-of-truth,quality-gates,exploration-fast-track,
#                  exploration-folder-protocol,pdf-processing,r-code-conventions}.md
# Pedro's newly added files: keep if project-scaffolding, delete if its content belongs in ~/.claude/.
git add -A
git commit -m "Pull Pedro's <date> updates; re-slim"
git push origin main
```

Manual re-slim is the deliberate baseline. If Pedro's cadence picks up and re-slim becomes tedious, escalate to `.gitattributes` with `merge=ours` on the slimmed paths.

### Outstanding workflow-meta tasks

- Companion paste: drop the block in [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork (1633 chars; self-trim per the in-file guide if needed).
- Skills/agents incremental promotion: Pedro ships 28 skills + 14 agents in this fork; only `review-matlab` + `matlab-reviewer` are at user scope so far. Promote as projects need them.
- Re-slim on next Pedro push (no schedule).

### Project-specific files in this repo

- [`quality_reports/plans/`](quality_reports/plans/) — slim-fork plans (the 2026-05-18 generalisation handoff)
- [`quality_reports/session_logs/`](quality_reports/session_logs/) — slim-fork session logs
- [`MEMORY.md`](MEMORY.md) — slim-fork meta-history (the slim commit, rules promoted, decisions)
- [`README.md`](README.md) — fork architecture, maintenance workflow, original Pedro README
