---
status: DRAFT — handoff brief for a fresh session
created: 2026-05-18
author: Sebastian Pfeil (drafted via Claude)
target_session: cold start in a new chat, no prior context
---

# HANDOFF: Generalize the workflow framework to user scope

## Goal

Extract the **generic, cross-project** backbone of Sebastian's current Claude Code workflow into user-scope files at `~/.claude/`, so the framework auto-loads in every Claude Code project on this machine. Produce a condensed companion text for manual paste into claude.ai and Cowork custom-instruction fields.

The Bank Capital project's `my-project/` is a local clone of Sebastian's own GitHub fork [`contest27/claude-code-my-workflow`](https://github.com/contest27/claude-code-my-workflow) (Sebastian's GitHub handle is `contest27`). That fork was created on GitHub from Pedro Santanna's original `claude-code-my-workflow` template. For the clean baseline we want **Pedro's original**, not Sebastian's fork — the fork may carry Sebastian's pushes, and even if untouched on GitHub, the local clone has been heavily extended for Bank Capital.

The Bank Capital project's `CLAUDE.md` and `.claude/` tree should be slimmed afterwards to contain only Bank-Capital-specific content; the global backbone backs it up automatically.

## Why this matters (constraints worth knowing)

- Sebastian is on the RUG career-track clock — CT auto-expires end-2026. Speed-to-publication is the binding constraint, not workflow elegance. **Time-box this refactor.** Do not let it eat cycles that belong to the JMCB R3 → Review of Finance Fast Track resubmission (decision logged 2026-05-13).
- The Bank Capital project is the current proving ground. It must keep working after the refactor — its `CLAUDE.md` will become shorter, not absent.
- The fork has accumulated ~3 years of personal extensions (the matlab-reviewer skill was just promoted today, as a precedent for how this generalization should work).

## Starting state on disk

```
C:\Users\P314966\Erasmus Universiteit Rotterdam Dropbox\Sebastian Pfeil\Uni\working folder\Research\dynamic macro\BANK CAPITAL\Latest Version\
├── CLAUDE.md                 # current — mixes generic framework + Bank Capital specifics
├── MEMORY.md                 # project-scoped memory (committed)
├── .claude/
│   ├── rules/                # 16 .md rule files (mix of generic + specific — see audit below)
│   ├── skills/               # project-scoped skills
│   ├── agents/               # project-scoped agents
│   ├── hooks/                # hooks
│   ├── state/                # gitignored personal memory
│   └── settings*.json
└── my-project/
    ├── .git/                 # upstream tracking → contest27/claude-code-my-workflow
    ├── CLAUDE.md             # stub pointing to ../CLAUDE.md (hoisted 2026-05-13)
    ├── templates/, scripts/, quality_reports/, explorations/, master_supporting_docs/, guide/
```

```
C:\Users\P314966\.claude\        # user scope — currently mostly empty for the workflow concern
├── skills/review-matlab/SKILL.md    # added 2026-05-18 as precedent
├── agents/matlab-reviewer.md        # added 2026-05-18 as precedent
└── projects/<hash>/memory/           # auto-memory, per-project (per-project not user-wide!)
```

The matlab work (2026-05-18) is the **template precedent**: take a generic-portable artifact, write it to user scope, delete the project-scoped duplicate. Same pattern applies to most of `.claude/rules/`.

## Approach

### Phase 1 — Discover the baseline (do not skip)

1. **Discover Pedro's original repo via the fork relationship.** Run:
   ```powershell
   gh repo view contest27/claude-code-my-workflow --json parent --jq '.parent.url'
   ```
   This returns the URL of the repo Sebastian forked from on GitHub. If `gh` is not authenticated, run `gh auth login` first (browser flow). If the lookup fails for any reason, ask Sebastian directly for Pedro Santanna's `claude-code-my-workflow` URL.
2. **Clone Pedro's original fresh** into a scratch folder OUTSIDE the Bank Capital tree, e.g., `C:\Users\P314966\scratch\workflow-template-upstream\`. Use a shallow clone (`--depth 1`) — history isn't needed.
3. **Inventory the upstream `.claude/` and `CLAUDE.md`** — that's the **generic baseline** as Pedro intended. Anything in there is by definition cross-project (modulo Pedro's own institutional context, which `.claude/rules/meta-governance.md` already accounts for).
4. **Diff against the Bank Capital project** to identify three buckets:
   - **Unchanged from upstream** → goes to user scope verbatim
   - **Modified by Sebastian** → may go to user scope (if the modification is itself generic) or stay project-scope
   - **Pure Sebastian additions** → classify as generic or Bank-Capital-specific case by case

A useful diff approach:
```powershell
Compare-Object (Get-ChildItem -Recurse "<scratch>\.claude") (Get-ChildItem -Recurse ".\.claude") -Property Name
# Then diff individual file contents where names match
```

### Phase 2 — Classify with the meta-governance rubric

Read [`.claude/rules/meta-governance.md`](.claude/rules/meta-governance.md) — Sebastian already wrote the rubric. The litmus test is the question at the bottom:

> "Would a biology PhD student forking this repo for lab protocols benefit from this knowledge?"
> If yes → user scope. If no → project scope.

For each file in `.claude/rules/`, classify. My read from this conversation (verify, don't trust blindly):

| File | Likely classification | Notes |
|---|---|---|
| `meta-governance.md` | Generic | Describes the framework itself |
| `plan-first-workflow.md` | Generic | Universal pattern |
| `orchestrator-protocol.md` | Generic | Contractor-mode loop |
| `orchestrator-research.md` | Generic | Research-mode variant |
| `session-logging.md` | Generic | Three-trigger pattern |
| `verification-protocol.md` | Generic | Compile/render/test |
| `quality-gates.md` | Mixed — concepts generic, numbers (80/90/95) and deduction rubrics partly specific | Promote concepts, parameterize numbers |
| `single-source-of-truth.md` | Generic | Universal principle |
| `knowledge-base-template.md` | Generic | Template |
| `exploration-fast-track.md` | Generic | |
| `exploration-folder-protocol.md` | Generic | |
| `r-code-conventions.md` | Cross-project if Sebastian uses R elsewhere; else project | Decide based on whether R appears in lectures/other projects |
| `pdf-processing.md` | Likely generic | Verify |
| `replication-protocol.md` | Likely project-specific (bank capital numerics) | Verify |
| `revision-protocol.md` | Paper-revision specific — keep project | Could go to a `~/.claude/rules/papers/` subtree if Sebastian revises papers often |
| `proofreading-protocol.md` | Lecture-specific or generic-academic? | Verify by reading |

Do the same for skills (`.claude/skills/`) and agents (`.claude/agents/`). The `matlab-reviewer`/`review-matlab` pair was already promoted today; treat that as the worked example.

### Phase 3 — Author the user-scope files

**Hard target:** `~/.claude/CLAUDE.md` must stay **under 200 lines** (per the meta-governance file's own size constraint — it stays in every Claude Code session's system prompt and longer files are truncated).

The file should be a slim framework that:
- States the user's role / responsibilities at a high level (researcher, lecturer, supervisor — three identities; the global CLAUDE.md should know them all without privileging one project)
- Lists the core principles (plan first, verify after, single source of truth, two-tier memory)
- Points to `~/.claude/rules/*.md` for path-scoped detail
- Does NOT inline content that belongs in a rule file

**Promote selected rules** to `~/.claude/rules/`. The path-scoped frontmatter (e.g., `paths: ["**/*.R"]`) makes them auto-fire in any project where matching files exist — this is exactly the desired behavior.

**Promote selected skills and agents** to `~/.claude/skills/` and `~/.claude/agents/`. Delete the project-scoped duplicates after.

### Phase 4 — Slim the Bank Capital project

Rewrite the project's `CLAUDE.md` to contain only:
- Project identity (paper, authors, status, JMCB-vs-RoF decision)
- Canonical-sources block (Overleaf TeX, references.bib, Mathematica/MATLAB code)
- Folder map
- Project-specific commands (XeLaTeX compile, Mathematica/MATLAB invocations, quality scoring)
- Current paper state and outstanding referee asks
- Project non-negotiables
- Pointer to `~/.claude/CLAUDE.md` for the global framework

It should drop:
- The "Core Principles" section (now in `~/.claude/CLAUDE.md`)
- The "Quality Thresholds" generic intro (numbers may stay if project-specific)
- The "Two-Tier Memory" generic description (now global)
- Generic skill quick-reference rows that aren't paper-specific

Target: cut Bank Capital `CLAUDE.md` roughly in half (~200 lines or less).

**Backup before rewriting:**
```powershell
Copy-Item CLAUDE.md CLAUDE.md.pre-generalize.bak
git -C "<path-to-overleaf-folder>" status   # check that no co-author edit is in flight
```

Note: the Bank Capital repo itself is not under git (per the environment header `Is a git repository: false`). The Overleaf-Dropbox folder IS under local git as of 2026-05-13 — that's the TeX backup, not the workflow files. Workflow files have no automatic backup; the `.bak` copy is the safety net for the rewrite.

### Phase 4.5 — Slim the GitHub template fork (so future projects clone clean)

The template at [`contest27/claude-code-my-workflow`](https://github.com/contest27/claude-code-my-workflow) must mirror the slimmed state: framework content lives in `~/.claude/`, the template ships project-scaffolding only. Otherwise new projects clone a fat copy and inherit the shadowing problem (project-scope wins on conflict, so global edits become invisible in any future project).

Steps:

1. **Clone the fork** to a scratch folder outside the Bank Capital tree:
   ```powershell
   git clone https://github.com/contest27/claude-code-my-workflow.git C:\Users\P314966\scratch\workflow-template-slim
   ```
2. **Apply the same delete/slim treatment as Phase 4** — remove every file whose content is now in `~/.claude/`. Keep only:
   - Project-scaffolding placeholders (CLAUDE.md skeleton with `[YOUR PROJECT NAME]` style fills)
   - `my-project/` support folders (`templates/`, `scripts/`, `quality_reports/`, etc.) if Pedro's template ships them
   - `.gitignore`, `.gitattributes`, README
3. **Wire Pedro's repo as `upstream`** (URL discovered in Phase 1) for future pulls:
   ```powershell
   git remote add upstream <pedro's repo URL>
   git fetch upstream
   ```
4. **Update the slim fork's README** to document (a) that the framework is sourced from user-scope `~/.claude/`, not from this repo, and (b) the maintenance workflow below.
5. **Commit and push:**
   ```powershell
   git add -A
   git commit -m "Slim template — framework content now lives in user-scope ~/.claude/"
   git push origin main
   ```

**Maintenance when Pedro pushes upstream updates** (Sebastian's choice: Option 1, manual re-slim — accepted because Pedro's update frequency is low):

```powershell
cd C:\Users\P314966\scratch\workflow-template-slim
git fetch upstream
git diff main upstream/main          # review what Pedro changed
git merge upstream/main               # accept the merge; framework files crept back in
# Manually delete framework files re-introduced by the merge (the same paths slimmed in step 2)
# Pedro's newly added files: keep if it's project-scaffolding, delete if its content belongs in ~/.claude/
git add -A
git commit -m "Pull Pedro's <date> updates; re-slim"
git push origin main
```

If manual re-slim later becomes tedious (Pedro's pace picks up), escalate to `.gitattributes` with `merge=ours` on the slimmed paths — see this conversation's exchange on 2026-05-18 for the config snippet. For now, manual is the deliberate baseline.

**Done when:**
- [ ] `contest27/claude-code-my-workflow` main branch contains no content duplicated in `~/.claude/`
- [ ] `upstream` remote points to Pedro's repo
- [ ] Slim fork's README explains the maintenance workflow

### Phase 5 — Produce condensed manual-paste text

For claude.ai (Settings → Profile → Custom Instructions) and Cowork (its custom-instructions field, exact location to verify):

- **~1500 character target** for claude.ai (their UI limit is around this; verify current limit).
- Distill the global framework to one screen: identity, principles, response-style preferences, when to ask vs proceed, double-check / verify-after norm.
- Save the canonical version on disk (e.g., `~/.claude/companion-instructions-claude-ai.md`) so updates have a clear home. Sebastian pastes from this file when it changes.

### Phase 6 — Verify

1. Open a **new project folder** (not Bank Capital) — ideally cloned from the slim template fork (`git clone https://github.com/contest27/claude-code-my-workflow.git <test-project>`), which is the realistic new-project test path. Confirm that user-scope `CLAUDE.md` and rules auto-load and that the cloned project ships thin (no framework duplication).
2. Re-open the Bank Capital project — confirm both global and project files load, no duplication, no contradictions.
3. Try one slash command (e.g., `/review-matlab` if there are any `.m` files in the test folder; the universalized version should fire).
4. Spot-check a few rule files — does the path-scoped frontmatter still trigger on the right file patterns?

## Decision points the next session should ask Sebastian upfront

1. **Pedro's repo URL** — if `gh repo view contest27/claude-code-my-workflow --json parent` fails, ask Sebastian directly. (`contest27` is Sebastian's own GitHub handle; we need the original parent, not the fork.)
2. **Scratch clone location?** Recommend somewhere outside Dropbox to avoid sync pressure. Confirm path.
3. **Quality-gates numbers (80/90/95).** Promote as-is to global, or parameterize? The numbers reflect Sebastian's calibration for journal-grade theory papers; lectures and exploratory projects might want different cutoffs.
4. **MEMORY.md at user scope?** Auto-memory is per-project. Should there be a user-wide `~/.claude/MEMORY.md` (manually maintained) for cross-project learnings, or accept that workflow-level lessons re-learn themselves in each project? Trade-off: another file to keep in sync vs. losing memory across projects.
5. **Other projects this should serve?** Lecture slides directory? MSc/BA supervision folders (`Bachelor/2026/ESE`, `Master/2026/ESE`, UvA supervision)? Knowing the target set helps calibrate "generic."
6. **Co-author etiquette.** Do Rochet / De Nicolò / Klimenko ever pull this repo onto their own machines? If yes, the global `~/.claude/` won't reach them — keep the Bank Capital project self-sufficient (slim, but still functional alone).

## Things NOT to do

- **Do not touch the canonical Bank Capital TeX** at `Apps\Overleaf\BankCapital\Bank_capital.tex`. The workflow refactor and the paper are orthogonal.
- **Do not delete project files without backing them up first.** Bank Capital `CLAUDE.md` and `.claude/rules/` are gitless on the workflow side — a `.bak` copy or zip is mandatory before any rewrite.
- **Do not push anything to GitHub** (the upstream fork or Sebastian's copy) without explicit confirmation. The fork's role here is to read, not to merge back.
- **Do not promote project-specific Bank-Capital content** (Overleaf paths, referee point numbers, paper notation registry) to user scope. The "biology PhD student" rubric is the test.
- **Do not exceed ~200 lines** in `~/.claude/CLAUDE.md`. If it bulges, factor content out into rule files.
- **Do not let the refactor steal more than ~3 hours of Sebastian's time** in any single session. He has a JMCB resubmission to ship.

## Definition of done

- [ ] `~/.claude/CLAUDE.md` exists, under 200 lines, framework-only
- [ ] `~/.claude/rules/` contains the promoted rule files with their original path-scoped frontmatter intact
- [ ] User-scope skills and agents inventory complete (including the already-promoted matlab pair)
- [ ] Bank Capital `CLAUDE.md` is slimmed and verified to still produce sensible Claude behavior
- [ ] Bank Capital `.claude/rules/` is pruned (duplicates removed, project-specific ones kept)
- [ ] `contest27/claude-code-my-workflow` is slimmed, pushed, with `upstream` wired to Pedro's repo; slim fork's README documents the manual re-slim workflow
- [ ] `companion-instructions-claude-ai.md` exists and is under the claude.ai char limit
- [ ] One non-Bank-Capital scratch test confirms the global framework auto-loads
- [ ] A short note added to Bank Capital `MEMORY.md`: "Global workflow framework now at user scope. Project CLAUDE.md is the Bank-Capital-specific delta only."

## References to read before starting

- `CLAUDE.md` (Bank Capital project root) — the current concrete instantiation
- `.claude/rules/meta-governance.md` — the generic-vs-specific rubric
- `.claude/rules/plan-first-workflow.md` — workflow norms this very handoff follows
- `.claude/rules/quality-gates.md` — for the 80/90/95 number question
- `~/.claude/skills/review-matlab/SKILL.md` and `~/.claude/agents/matlab-reviewer.md` — the worked precedent

## Suggested first message to open the next session

> "Read `my-project/quality_reports/plans/2026-05-18_generalize-workflow-HANDOFF.md` and start at Phase 1. Use `gh repo view contest27/claude-code-my-workflow --json parent` to find Pedro's repo, then confirm with me before cloning."
