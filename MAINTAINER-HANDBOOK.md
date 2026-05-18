# MAINTAINER HANDBOOK — Sebastian's slim fork

Reference guide for Sebastian Pfeil maintaining [`contest27/claude-code-my-workflow`](https://github.com/contest27/claude-code-my-workflow) and starting new Claude Code projects from it. **Pin this file in your IDE** for quick access.

**The three-tier setup (after the 2026-05-18 generalisation):**
- **User scope:** `~/.claude/CLAUDE.md`, `~/.claude/MEMORY.md`, `~/.claude/rules/`, `~/.claude/companion-instructions-claude-ai.md`. Auto-loads in every Claude Code session on this machine.
- **Slim-fork scope:** this repo on disk at `C:\Users\P314966\workflow-template-slim\`, on GitHub at `contest27/claude-code-my-workflow`. Project scaffolding for new clones; the maintainer view (you, reading this) lives at the bottom of `CLAUDE.md` + in this handbook.
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
#    b) DELETE the entire "Maintainer view (workflow-meta project)" section at the bottom
#       (everything from the divider with "Maintainer view" to end-of-file).
#    c) Tailor Folder Structure / Commands / Quality Thresholds / Current State.
#    d) Add a project-specific "Non-Negotiables" section (canonical TeX path, guardrails, etc.).

# 6. Wipe MEMORY.md:
#    a) Delete the slim-fork meta-history content.
#    b) Keep the section headers (Project Context / Team / Workflow Preferences /
#       Local Env / Open Items) — populate as you go with [LEARN:project] entries.

# 7. (Optional) Add a project-specific .claude/rules/quality-gates.md
#    if you want project-specific deduction tables. The user-scope version
#    (~/.claude/rules/quality-gates.md) is concept-only.

# 8. (Optional) Promote / copy individual skills from this slim fork if the project needs them.
#    See Workflow 3 below.
```

---

## Workflow 2 — Re-slim after Pedro pushes upstream

```powershell
cd C:\Users\P314966\workflow-template-slim

# 1. Fetch and review.
git fetch upstream                                            # pedrohcgs/claude-code-my-workflow
git diff main upstream/main                                   # see what Pedro changed

# 2. (Optional) branch first if uncertain about the merge:
# git checkout -b reslim-2026-MM-DD

# 3. Merge.
git merge upstream/main                                       # framework files will creep back in

# 4. Re-delete the 12 framework rules (these are now at ~/.claude/rules/).
$slimmedRules = @(
    "meta-governance.md",
    "plan-first-workflow.md",
    "orchestrator-protocol.md",
    "orchestrator-research.md",
    "session-logging.md",
    "verification-protocol.md",
    "single-source-of-truth.md",
    "quality-gates.md",
    "exploration-fast-track.md",
    "exploration-folder-protocol.md",
    "pdf-processing.md",
    "r-code-conventions.md"
)
foreach ($r in $slimmedRules) {
    $p = ".claude/rules/$r"
    if (Test-Path $p) { Remove-Item -Path $p -Force; "Re-slimmed: $r" }
}

# 5. CLAUDE.md and MEMORY.md likely reverted to Pedro's versions during merge.
#    Manually restore the dual-role state:
#    - CLAUDE.md: slim-fork note at top + maintainer-view section at the bottom (see git log for the working copy you want)
#    - MEMORY.md: the workflow-meta history (slim commit hash, decisions, open items)
#    Quickest: `git checkout HEAD~N -- CLAUDE.md MEMORY.md` where HEAD~N is the
#    last commit before the merge; OR copy from a backup.

# 6. Pedro's NEW files (rules/skills/agents he added since the last sync):
#    Apply the "biology PhD student" rubric. Would a biology PhD forking this benefit?
#    - YES (generic backbone) → promote to ~/.claude/, delete here. See Workflow 3.
#    - NO (lecture-specific, paper-revision-specific, or project-scaffolding) → keep here.
#    When uncertain, keep — moving to user scope is easy later; removing from user scope is harder.

# 7. Update MEMORY.md if the rule inventory changed.

# 8. Commit + push.
git add -A
git commit -m "Pull Pedro's <date> updates; re-slim"
git push origin main

# 9. If you used a branch:
# git checkout main && git merge reslim-2026-MM-DD && git push origin main
```

**If manual re-slim becomes tedious** (Pedro's cadence increases), escalate to `.gitattributes` with `merge=ours` on the slimmed paths:

```gitattributes
# .gitattributes — keep the slim version on every future upstream merge
.claude/rules/meta-governance.md merge=ours
.claude/rules/plan-first-workflow.md merge=ours
.claude/rules/orchestrator-protocol.md merge=ours
# ... etc for the 12 slimmed paths
CLAUDE.md merge=ours
MEMORY.md merge=ours
```

This makes future `git merge upstream/main` auto-keep the slim version (i.e., not re-introduce the framework files / overwrite the dual-role CLAUDE.md). Trade-off: you'll miss legitimate upstream improvements to those paths. Default to manual until you have evidence the cadence justifies automation.

---

## Workflow 3 — Promote an individual skill / agent / rule incrementally

Pattern from the 2026-05-18 `matlab-reviewer` precedent. Apply when an existing fork-scope skill/agent/rule becomes useful across projects.

```powershell
# Example: promote the /compile-latex skill from slim-fork scope to user scope.
$src = "C:\Users\P314966\workflow-template-slim\.claude\skills\compile-latex"
$dst = "C:\Users\P314966\.claude\skills"

# 1. Copy to user scope.
Copy-Item -Path $src -Destination $dst -Recurse -Force

# 2. (Optional) Strip project-specific paths or assumptions in the user-scope copy.
#    Keep it generic.

# 3. Delete from slim fork (so it doesn't shadow).
Remove-Item -Path $src -Recurse -Force

# 4. Note the promotion in slim-fork MEMORY.md (workflow-meta history grows).

# 5. Commit + push slim fork.
$slim = "C:\Users\P314966\workflow-template-slim"
git -C $slim add -A
git -C $slim commit -m "Promote /compile-latex to user scope"
git -C $slim push origin main

# 6. Verify in a fresh Claude Code session (any folder) that /compile-latex still works.
```

Same pattern for agents (`.claude/agents/<name>.md`) and rules (`.claude/rules/<name>.md`).

---

## File inventory (as of 2026-05-18)

### `~/.claude/` — user scope (NOT committed anywhere; local to this machine)

| Path | Lines | Purpose |
|---|---|---|
| `CLAUDE.md` | 119 | Framework: three identities, principles, tone, environment, pointers |
| `MEMORY.md` | 98 | Cross-project facts: role, RUG CT clock, workflow preferences, environment, lineage |
| `rules/` (12 files) | varies | `meta-governance`, `plan-first-workflow`, `orchestrator-protocol`, `orchestrator-research`, `session-logging`, `verification-protocol`, `single-source-of-truth`, `quality-gates`, `exploration-fast-track`, `exploration-folder-protocol`, `pdf-processing`, `r-code-conventions` |
| `skills/review-matlab/` | — | Promoted 2026-05-18 morning as the precedent |
| `agents/matlab-reviewer.md` | — | Promoted 2026-05-18 morning |
| `companion-instructions-claude-ai.md` | 1633 chars (paste block) | claude.ai Custom Instructions + Cowork paste source |

### `workflow-template-slim/` — the slim fork

| Path | Purpose |
|---|---|
| `CLAUDE.md` | Dual-role: template scaffolding top + maintainer view bottom |
| `MEMORY.md` | Workflow-meta history (slim commit, rules promoted/retained, decisions) |
| `README.md` | Pedro's original + slim-fork notice prepended |
| `MAINTAINER-HANDBOOK.md` | This file |
| `.claude/rules/` (6 files) | Retained Pedro rules: `beamer-quarto-sync`, `knowledge-base-template`, `no-pause-beamer`, `proofreading-protocol`, `replication-protocol`, `tikz-visual-quality` |
| `.claude/skills/` (22 dirs) | Pedro's full skill kit (not yet promoted) |
| `.claude/agents/` (10 files) | Pedro's full agent kit |
| `.claude/hooks/`, `.claude/references/` | Pedro's full kit |
| `quality_reports/plans/2026-05-18_generalize-workflow-HANDOFF.md` | Original handoff brief |
| `quality_reports/session_logs/2026-05-18_generalize-workflow.md` | Build log |
| `templates/`, `scripts/`, `master_supporting_docs/`, `explorations/`, `guide/`, `docs/`, `Slides/`, `Quarto/`, `Preambles/`, `Figures/`, `Bibliography_base.bib`, `LICENSE`, `.gitignore` | Pedro's scaffolding for downstream clones |

### `workflow-template-upstream/` — Pedro's read-only baseline

| Path | Purpose |
|---|---|
| `C:\Users\P314966\workflow-template-upstream\` | Shallow clone of `pedrohcgs/claude-code-my-workflow` for diff baselines. Don't edit; re-clone with `git pull --depth 1` if stale. |

### Active projects

| Project | Location | Notes |
|---|---|---|
| Bank Capital paper | `…\BANK CAPITAL\Latest Version\` | Slim `CLAUDE.md` + project `MEMORY.md` (192 lines) + project `.claude/` with `revision-protocol` + 5 paper-revision skills + 2 theory agents |
| Practice Theory Gap | `…\Research\Practice-Theory-Gap\` | Auto-memory confirms "Ella as coauthor"; project layer intact |
| Other research projects (Calibrating Ambiguity, Price Image, Overconfidence Data Habrok, Dividend Regulation, …) | various `…\Research\<topic>\` | Mix of pre-existing + slim-fork-cloned setups |

---

## Anti-patterns to avoid

- **Don't bulk-promote skills/agents.** Promote per-need. Most of Pedro's skills are lecture-specific or not yet validated against your work patterns.
- **Don't push framework changes to the slim fork.** The slim fork ships scaffolding only; framework changes go to `~/.claude/`.
- **Don't push to `pedrohcgs/claude-code-my-workflow`** (Pedro's repo). Your push target is only `contest27/claude-code-my-workflow`.
- **Don't edit files in `workflow-template-upstream/`** — it's a read-only baseline for diffs.
- **Don't conflate the slim fork with a project.** Opening Claude Code IN the slim-fork folder activates the maintainer view (you're iterating on the workflow). Opening Claude Code in a cloned project activates the project's filled-in CLAUDE.md (you're working on the project's content).
- **Don't rename `my-project/` inside an existing pre-hoisted setup.** Bank Capital has `my-project/` as a subfolder because that's where Pedro's clone landed BEFORE the 2026-05-13 dotfile hoisting. Renaming now would break references. For NEW clones, name the clone target after the actual project; never use `my-project` for a real project.

---

## Companion (claude.ai + Cowork) paste

When the global framework changes, re-paste the block in `~/.claude/companion-instructions-claude-ai.md` (between `<!-- BEGIN PASTE -->` and `<!-- END PASTE -->` markers) into:
- **claude.ai:** Settings → Profile → Custom Instructions
- **Cowork:** its custom-instructions field (verify location in Cowork's UI)

Current block: 1633 chars. claude.ai's documented limit is around 1500 chars with some flex. Trim per the in-file guide if rejected (Time-pressure line first, then Notation-canonical, then Figures-publication-ready).

---

## Quick reference — where things live

| What | Where |
|---|---|
| Framework principles | `~/.claude/CLAUDE.md` |
| Cross-project facts | `~/.claude/MEMORY.md` |
| Generic rules | `~/.claude/rules/*.md` |
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
2. Pin this `MAINTAINER-HANDBOOK.md` as an editor tab in VS Code (right-click tab → "Keep Open" or drag to a sidebar group).
3. Ask: "Read MAINTAINER-HANDBOOK.md and summarise the three workflows."
4. To start a new project, follow Workflow 1 above; for an upstream re-slim, follow Workflow 2; for an incremental promotion, Workflow 3.

This session is the **operating manual** — refer to it whenever you need to remember "how do I start a new project" or "how do I re-slim."
