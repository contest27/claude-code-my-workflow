# MAINTAINER HANDBOOK — Sebastian's slim fork

Reference guide for Sebastian Pfeil maintaining [`contest27/claude-code-my-workflow`](https://github.com/contest27/claude-code-my-workflow) and starting new Claude Code projects from it. **Pin this file in your IDE** for quick access.

**The three-tier setup (post 2026-05-18 generalisation + v1.8.0 re-slim):**
- **User scope:** `~/.claude/CLAUDE.md`, `~/.claude/MEMORY.md`, `~/.claude/rules/` (16 rules), `~/.claude/companion-instructions-claude-ai.md`. Auto-loads in every Claude Code session on this machine.
- **Slim-fork scope:** this repo on disk at `C:\Users\P314966\workflow-template-slim\`, on GitHub at `contest27/claude-code-my-workflow`. Project scaffolding for new clones; the maintainer view lives at the bottom of `CLAUDE.md` + in this handbook.
- **Project scope:** each cloned project has its own `CLAUDE.md`, `MEMORY.md`, `.claude/`. Project files override / supplement user-scope.

---

## Workflow 1 — Start a new project (paper, lecture deck, supervision folder, etc.)

```powershell
# 1. Decide name + location. Use the project's actual name as the folder, NOT "my-project".
#    The "my-project" in Pedro's README is just a placeholder.
$proj = "C:\Users\P314966\Erasmus Universiteit Rotterdam Dropbox\Sebastian Pfeil\Uni\working folder\Research\NEW-PAPER-NAME"

# 2. Clone the slim fork into that folder.
git clone https://github.com/contest27/claude-code-my-workflow.git $proj
cd $proj

# 3. (Optional but recommended) decouple from the fork's git history if this is a separate project.
#    Two patterns:

#    Pattern A — the new project is its own repo from scratch:
git remote remove origin
git remote remove upstream
Remove-Item -Recurse -Force .git    # wipe Pedro's git history entirely
git init
git add -A
git commit -m "Initial commit from contest27 slim fork"
git remote add origin <your-new-project-github-url>
git push -u origin main

#    Pattern B — keep "upstream" wired to Pedro for future framework pulls, "origin" is the new repo:
git remote rename origin slim-fork-origin    # the slim fork (no longer your push target)
git remote remove upstream                    # Pedro's framework — pull manually if you want updates
git remote add origin <your-new-project-github-url>
git push -u origin main

# 4. Open Claude Code in the new folder. First-session sanity check:
#    Ask: "What's my role and the three identities you know about?"
#    Claude should answer with the researcher / lecturer / supervisor framing
#    (proves user-scope ~/.claude/ auto-loaded).

# 5. Edit CLAUDE.md:
#    a) Fill in [YOUR PROJECT NAME] + [YOUR INSTITUTION] at the top.
#    b) DELETE the entire "Maintainer view (workflow-meta project)" section at the bottom.
#    c) Tailor Folder Structure / Commands / Quality Thresholds / Current State.
#    d) Add a project-specific "Non-Negotiables" section (canonical TeX path, guardrails, etc.).

# 6. Wipe MEMORY.md:
#    a) Delete the slim-fork meta-history content.
#    b) Keep the section headers — populate as you go with [LEARN:project] entries.

# 7. (Optional) Add a project-specific .claude/rules/quality-gates.md
#    if you want project-specific deduction tables. The user-scope version is concept-only.

# 8. (Optional) Promote / copy individual skills from this slim fork if the project needs them.
#    See Workflow 3 below.
```

---

## Workflow 2 — Re-slim after Pedro pushes upstream

**Lesson from the 2026-05-18 v1.2.0 → v1.8.0 re-slim: always branch for non-trivial pulls (>10 commits or any file the slim has modified).** Branching makes rollback trivial if conflict resolution goes wrong; merging directly to `main` doesn't.

```powershell
cd C:\Users\P314966\workflow-template-slim

# 1. Fetch and review.
git fetch upstream                                            # pedrohcgs/claude-code-my-workflow
git rev-list --left-right --count main...upstream/main        # "local-ahead upstream-ahead"
git log --oneline 3840e81..upstream/main                      # commits Pedro added (3840e81 was the initial slim base)
git diff --shortstat 3840e81 upstream/main                    # rough volume

# 2. ALWAYS branch (not optional for non-trivial pulls).
git checkout -b reslim-YYYY-MM-DD

# 3. Merge.
git merge upstream/main                                       # conflicts expected on CLAUDE.md, MEMORY.md, and any user-scope rule files Pedro modified

# 4. Resolve conflicts using these patterns (proven on the v1.8.0 re-slim):

#    Pattern A — "modify/delete" on framework rules at user scope:
#       Pedro modified a rule we deleted because it's at ~/.claude/rules/.
#       Resolution: re-delete (user scope is authoritative). Note Pedro's update as a
#       follow-up to consider for the user-scope copy.
git rm .claude/rules/orchestrator-protocol.md .claude/rules/quality-gates.md .claude/rules/r-code-conventions.md

#    Pattern B — content conflicts on CLAUDE.md and MEMORY.md:
#       Keep our dual-role structure. Manually merge Pedro's improvements:
#       - Skills Quick Reference table: add new entries Pedro shipped.
#       - Commands: add new scripts Pedro added (check-palette-sync, check-surface-sync, etc.).
#       - Folder Structure: add new directories (decision-records, etc.).
#       - Current Project State: add HelloWorld sample if Pedro shipped one.
#       Discard Pedro's [LEARN] entries in MEMORY.md (they're template-development history, not workflow-meta).

# 5. Re-delete the 12 framework rules even if they weren't in conflict (in case any crept back via Pedro's renames or directory moves):
$slimmedRules = @(
    "meta-governance.md", "plan-first-workflow.md", "orchestrator-protocol.md",
    "orchestrator-research.md", "session-logging.md", "verification-protocol.md",
    "single-source-of-truth.md", "quality-gates.md", "exploration-fast-track.md",
    "exploration-folder-protocol.md", "pdf-processing.md", "r-code-conventions.md",
    # Post-v1.8.0 additions to user scope:
    "content-invariants.md", "cross-artifact-review.md",
    "post-flight-verification.md", "summary-parity.md"
)
foreach ($r in $slimmedRules) {
    $p = ".claude/rules/$r"
    if (Test-Path $p) { Remove-Item -Path $p -Force; "Re-slimmed: $r" }
}

# 6. Pedro's NEW files (rules / skills / agents he added):
#    Apply the "biology PhD student" rubric.
#    - Generic backbone (Pedro v1.6.x added summary-parity, post-flight-verification, etc.)?
#      Path-scoped → promote to ~/.claude/, delete here.
#      (NB: even content-targeted rules can be promoted — path scoping keeps them dormant in
#       non-matching projects. Don't over-restrict.)
#    - Lecture-specific (TikZ, Beamer, Quarto-specific)? Keep at fork scope.
#    - Skills / agents? Default keep at fork scope; promote individually per project need.

# 7. Commit on the branch.
git add -A
git commit -m "Pull Pedro v<old> → v<new>; re-slim"

# 8. Fast-forward main to the branch tip and push.
git checkout main
git merge --ff-only reslim-YYYY-MM-DD
git push origin main

# 9. Delete the branch.
git branch -d reslim-YYYY-MM-DD
```

**If manual re-slim becomes tedious** (Pedro's cadence increases), escalate to `.gitattributes` with `merge=ours` on the slimmed paths:

```gitattributes
# .gitattributes — keep the slim version on every future upstream merge
.claude/rules/meta-governance.md merge=ours
.claude/rules/plan-first-workflow.md merge=ours
# ... etc for the 16 slimmed paths
CLAUDE.md merge=ours
MEMORY.md merge=ours
```

Trade-off: you'll miss legitimate upstream improvements to those paths. Default to manual until evidence forces automation.

---

## Workflow 3 — Promote an individual skill / agent / rule incrementally

Pattern from the 2026-05-18 `matlab-reviewer` precedent + the 4-rule batch promotion at the end of the v1.8.0 re-slim.

```powershell
# Example: promote a skill from slim-fork scope to user scope.
$src = "C:\Users\P314966\workflow-template-slim\.claude\skills\compile-latex"
$dst = "C:\Users\P314966\.claude\skills"

# 1. Read the candidate. Check the "biology PhD student" rubric. Check `paths:` /
#    dependency-on-other-skills frontmatter — if it references other skills, decide
#    whether they need promoting too (or whether path-scoping keeps it dormant when
#    they're absent).

# 2. Copy to user scope.
Copy-Item -Path $src -Destination $dst -Recurse -Force

# 3. (Optional) Strip project-specific paths or assumptions. Keep generic.

# 4. Delete from slim fork.
Remove-Item -Path $src -Recurse -Force

# 5. Update ~/.claude/CLAUDE.md if the rule belongs in the Cross-cutting rules table.

# 6. Note the promotion in slim-fork MEMORY.md.

# 7. Commit + push slim fork.
$slim = "C:\Users\P314966\workflow-template-slim"
git -C $slim add -A
git -C $slim commit -m "Promote /compile-latex to user scope"
git -C $slim push origin main

# 8. Verify in a fresh Claude Code session (any folder) that /compile-latex still works.
```

---

## File inventory (as of 2026-05-18 evening, post-v1.8.0 re-slim + 4-rule promotion)

### `~/.claude/` — user scope (NOT committed anywhere; local to this machine)

| Path | Purpose |
|---|---|
| `CLAUDE.md` | Framework: three identities, principles, tone, environment, pointers to rules (now lists 13 of 16 rules in the table) |
| `MEMORY.md` | Cross-project facts: role, RUG CT clock, workflow preferences, environment, lineage |
| `rules/` (16 files) | Initial 12: `meta-governance`, `plan-first-workflow`, `orchestrator-protocol`, `orchestrator-research`, `session-logging`, `verification-protocol`, `single-source-of-truth`, `quality-gates`, `exploration-fast-track`, `exploration-folder-protocol`, `pdf-processing`, `r-code-conventions`. Post-v1.8.0: `content-invariants`, `cross-artifact-review`, `post-flight-verification`, `summary-parity`. |
| `skills/review-matlab/` | Promoted 2026-05-18 morning as precedent |
| `agents/matlab-reviewer.md` | Promoted 2026-05-18 morning |
| `companion-instructions-claude-ai.md` | claude.ai Custom Instructions + Cowork paste source (1633 chars) |

### `workflow-template-slim/` — the slim fork

| Path | Purpose |
|---|---|
| `CLAUDE.md` | Dual-role: template scaffolding top + maintainer view bottom |
| `MEMORY.md` | Workflow-meta history (slim commits, rules promoted/retained, decisions) |
| `README.md` | Pedro's original + slim-fork notice prepended (post-v1.8.0: now with CHANGELOG / CONTRIBUTING badges from Pedro) |
| `MAINTAINER-HANDBOOK.md` | This file |
| `.claude/rules/` (8 files) | Retained Pedro rules: `beamer-quarto-sync`, `no-pause-beamer`, `tikz-visual-quality`, `tikz-measurement` (new v1.3.0), `tikz-prevention` (new v1.3.0), `proofreading-protocol`, `replication-protocol`, `knowledge-base-template` |
| `.claude/skills/` (~30 dirs) | Pedro's full skill kit after v1.8.0 (was 22 pre-v1.8.0; added 8: `audit-reproducibility`, `checkpoint`, `new-diagram`, `permission-check`, `preregister`, `respond-to-referees`, `seven-pass-review`, `verify-claims`) |
| `.claude/agents/` (14 files) | Pedro's full agent kit after v1.8.0 (was 10; added 4: `claim-verifier`, `domain-referee`, `editor`, `methods-referee`) |
| `.claude/references/` (4 files) | Pedro v1.5.0+ reference catalogues: `audit-pet-peeves`, `discipline-cards`, `journal-profiles`, `v1.9-backlog` |
| `.claude/hooks/`, `.claude/scripts/` | Pedro's hooks + statusline scaffolding |
| `quality_reports/plans/2026-05-18_generalize-workflow-HANDOFF.md` | Original handoff brief |
| `quality_reports/session_logs/2026-05-18_generalize-workflow.md` | Build log + re-slim addendum |
| `templates/` (with `tikz-snippets/`) | Pedro's templates incl. session-log, quality-report, decision-record (v1.6.0), journal-profile (v1.5.0), preregistration, response-to-referees, skill-template, + 8 TikZ snippets |
| `scripts/R/`, `scripts/check-*.py`, `scripts/validate-setup.sh` | Pedro's R-pipeline template + audit validators (v1.6.x – v1.8.0) |
| `Slides/HelloWorld.tex`, `Quarto/HelloWorld.qmd`, `Preambles/header.tex`, `Bibliography_base.bib` | Pedro's newcomer demos (v1.3.0+) |
| `CHANGELOG.md`, `TROUBLESHOOTING.md` | Pedro v1.6.x docs |
| `.github/`, `.vscode/settings.json` | Pedro's onboarding scaffolding (v1.3.0+) |

### `workflow-template-upstream/` — Pedro's read-only baseline

| Path | Purpose |
|---|---|
| `C:\Users\P314966\workflow-template-upstream\` | Shallow clone of `pedrohcgs/claude-code-my-workflow` for diff baselines. Don't edit; refresh with `git -C <path> pull --depth 1` if stale. |

### Active projects on this machine

| Project | Location | Notes |
|---|---|---|
| Bank Capital paper | `…\BANK CAPITAL\Latest Version\` | Slim `CLAUDE.md` + project `MEMORY.md` (~194 lines) + project `.claude/` with `revision-protocol` + 5 paper-revision skills + 2 theory agents |
| Practice Theory Gap | `…\Research\Practice-Theory-Gap\` | Confirmed picks up user-scope on 2026-05-18 fresh-session test |
| Other research projects (Calibrating Ambiguity, Price Image, Overconfidence Data Habrok, Dividend Regulation, …) | various `…\Research\<topic>\` | Mix of pre-existing + slim-fork-cloned setups |

---

## Anti-patterns to avoid

- **Don't bulk-promote skills/agents.** Promote per-need. Most of Pedro's skills are lecture-specific or research-pipeline-specific and only become useful in matching projects.
- **Don't push framework changes to the slim fork.** The slim fork ships scaffolding only; framework changes go to `~/.claude/`. Framework changes pushed to the slim fork would shadow user-scope versions in newly-cloned projects.
- **Don't push to `pedrohcgs/claude-code-my-workflow`** (Pedro's repo). Push target: only `contest27/claude-code-my-workflow`.
- **Don't edit files in `workflow-template-upstream/`** — it's a read-only baseline for diffs.
- **Don't conflate the slim fork with a project.** Opening Claude Code IN the slim-fork folder activates the maintainer view of CLAUDE.md (iterating on the workflow). Opening Claude Code in a cloned project activates the project's filled-in CLAUDE.md.
- **Don't rename `my-project/` inside an existing pre-hoisted setup.** Bank Capital has `my-project/` as a subfolder of a pre-existing tree (legacy). For new clones, the clone target folder name should BE the project name; never use `my-project` for a real project.
- **Don't skip the branch step on a non-trivial pull.** The v1.8.0 re-slim conflicted on 5 files; merging directly to `main` would have made rollback awkward. Branch makes it `git checkout main`-cheap.

---

## Companion (claude.ai + Cowork) paste

When the global framework changes, re-paste the block in `~/.claude/companion-instructions-claude-ai.md` (between `<!-- BEGIN PASTE -->` and `<!-- END PASTE -->` markers) into:
- **claude.ai:** Settings → Profile → Custom Instructions
- **Cowork:** its custom-instructions field

Current block: 1633 chars. claude.ai's documented limit is around 1500 chars with some flex. Trim per the in-file guide if rejected (Time-pressure line first, then Notation-canonical, then Figures-publication-ready).

---

## Quick reference — where things live

| What | Where |
|---|---|
| Framework principles | `~/.claude/CLAUDE.md` |
| Cross-project facts | `~/.claude/MEMORY.md` |
| Generic rules (16) | `~/.claude/rules/*.md` |
| Companion paste source | `~/.claude/companion-instructions-claude-ai.md` |
| Slim fork (local clone) | `C:\Users\P314966\workflow-template-slim\` |
| Slim fork (GitHub) | https://github.com/contest27/claude-code-my-workflow |
| Pedro's upstream (local read-only baseline) | `C:\Users\P314966\workflow-template-upstream\` |
| Pedro's upstream (GitHub) | https://github.com/pedrohcgs/claude-code-my-workflow |
| This handbook | `C:\Users\P314966\workflow-template-slim\MAINTAINER-HANDBOOK.md` |
| Slim-fork build log | `…\workflow-template-slim\quality_reports\session_logs\2026-05-18_generalize-workflow.md` |
| Slim-fork original plan | `…\workflow-template-slim\quality_reports\plans\2026-05-18_generalize-workflow-HANDOFF.md` |

---

## Pinned-session usage

When you want a Claude Code session ready to advise on workflow-meta questions:

1. Open Claude Code in `C:\Users\P314966\workflow-template-slim\`. The maintainer view in `CLAUDE.md` auto-loads + user-scope `~/.claude/CLAUDE.md` auto-loads on top.
2. Pin this `MAINTAINER-HANDBOOK.md` as an editor tab in VS Code (right-click tab → "Keep Open").
3. Ask: "Read MAINTAINER-HANDBOOK.md and summarise the three workflows."
4. To start a new project, follow Workflow 1; for an upstream re-slim, follow Workflow 2; for an incremental promotion, Workflow 3.

This session is the **operating manual** — refer to it whenever you need to remember "how do I start a new project" or "how do I re-slim."
