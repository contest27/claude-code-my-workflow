# Project Memory — Slim Fork (workflow-meta project)

Corrections and learned facts that persist across sessions.
When a mistake is corrected, append a `[LEARN:category]` entry below; most recent at bottom.

---

## Workflow Patterns

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

[LEARN:files] Templates belong in `templates/` with descriptive names. Don't enumerate the inventory here — a hand-kept list goes stale (this entry's own list was missing three files when audited); `ls templates/` is the inventory.

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

[LEARN:memory] Two-tier memory solves template vs working project tension: MEMORY.md (generic patterns, committed) + native auto memory (`~/.claude/projects/<project>/memory/`, machine-local) → cross-machine sync + local privacy. *(Second tier was `personal-memory.md` until v2.5; retired for the native mechanism.)*

[LEARN:memory] Hooks prompt reflection, don't auto-append (e.g. the Stop-hook session-log reminder) → user maintains control while building habit.

[LEARN:open] **Skills/agents promotion to user scope:** incremental, per project need.

[LEARN:open] **Reconcile user-scope rule updates from Pedro v1.8.0:** `orchestrator-protocol.md`, `quality-gates.md`, `r-code-conventions.md` at user-scope are at Pedro's pre-PR-#35 content; Pedro's newer versions are in `workflow-template-upstream/.claude/rules/` for diff.

[LEARN:open] **Re-slim on next Pedro push:** follow `MAINTAINER-HANDBOOK.md` Workflow 2.

[LEARN:open] **Companion claude.ai paste:** Sebastian to paste the contents of [`~/.claude/companion-instructions-claude-ai.md`](file:///C:/Users/P314966/.claude/companion-instructions-claude-ai.md) into claude.ai Custom Instructions + Cowork field. 1633 chars; trim per the in-file guide if the field rejects.

[LEARN:open] **Wife's custom instructions:** drafted in the 2026-05-18 session; Sebastian to fill in name + language and paste into her account.

[LEARN:drift] `replace_all` on one phrasing (e.g., `"26 skills"`) misses sibling phrasings — `"26 skills, and 21 rules"` (extra "and"), `"26 slash commands"`, `"template's 26"`, `"N skills on day one"` (prose). Count drift hit us 3 times in v1.5.x (PRs #70, #76, #78). Solution: `scripts/check-surface-sync.py` with compound regex patterns as a pre-commit gate. Adding a new phrasing to documentation requires adding a matching regex to the script, otherwise it won't be caught.

[LEARN:drift] Guard against false positives when scanning for template counts: `"3 parallel agents"`, `"17 specialized agents"` (clo-author attribution), `"start with 2-3 skills"` are all legitimate non-template uses of `N + category` phrases. Use compound patterns requiring multiple template-specific tokens on the same line.

## Claude Code Hooks

[LEARN:hooks] Stop-hook block protocol has TWO valid forms: (a) legacy — `exit 2` + reason on stderr; (b) modern — `exit 0` + JSON `{"decision":"block","reason":"..."}` on stdout. `log-reminder.py` uses the modern form. Audit agents unfamiliar with the modern protocol will flag this as "should exit 2" — false alarm. Documented in `/deep-audit` skill's false-alarm list.

[LEARN:hooks] `initialPermissionMode` in VSCode settings only fires at **session start**. Mid-session mode toggles (via `Shift+Tab` or `/permission-mode`) override the file settings until session end. The 6-tier permission stack: VSCode user / workspace / CLI user / project / project-local / in-session runtime — the last is authoritative. "Prompts fire despite bypass config" is almost always a stale session, not a settings bug.

## Plan→Bypass Framing

[LEARN:safety] Do NOT frame Plan→Bypass as a "safety boundary" or "safety guarantee." Plan approval gives you a chance to review the APPROACH before execution, but exiting plan mode returns the session to `defaultMode` (bypassPermissions), at which point any tool call runs under the full allowlist. Frame as "review-before-execute convenience." If a user needs a real enforcement boundary, they should keep `defaultMode: "default"` and approve each high-risk tool individually.

## Privacy in Diagnostic Skills

[LEARN:privacy] Diagnostic skills that read host-global config (e.g., `~/.claude/`, VSCode user settings) must require **explicit user confirmation** before crossing the repo boundary — especially in template repos that get forked. Phase the skill: repo-local auto, host-global opt-in with key redaction. Codex correctly flagged this pattern as a template-adopter privacy risk in PR #75.

## Claim-vs-Reality Framing

[LEARN:framing] **The orchestrator became a real runtime in v2.0.0 (2026-06-09)** (fan-out → reduce → judge + hallucination gate → loop-until-dry), superseding its earlier "pattern, not a runtime" framing, retired 2026-08-21. What holds regardless: there is **no daemon and no post-plan-approval trigger** — the loop is always user- or skill-initiated, a documented non-goal. Any doc claiming it "activates automatically after plan approval" is wrong.

[LEARN:framing] **A gate is only as enforced as its installation.** v2.0.0 replaced the "quality gates" claim (then enforced only inside `/commit`) with a real pre-commit hook — but it is live only **after the user runs `./scripts/install-hooks.sh`**, and `SKIP_QUALITY_GATE=1` / `--no-verify` bypass it. Docs must say "enforced once installed", never "always enforced". *(v2.0.0; retired the older framing 2026-08-21.)*

[LEARN:framing] Cross-artifact review is **pattern-based detection**, not universal auto-invocation. If the manuscript has no `\input{scripts/...}` signals, no cross-artifact work happens even without `--no-cross-artifact`. Document detection signals explicitly.

## Dogfooding Gaps Found in Round-1 Audit (2026-04-16)

[LEARN:dogfooding] Empty `quality_reports/plans/`, `specs/`, `session_logs/` directories in a WORKING FORK are a red flag — claimed dogfooding nobody follows. (In the shipped template these dirs are gitignored by design, so the heuristic applies to your own fork, not the clean tree.) The Stop-hook log reminder validates itself by catching missing logs; plan-first has no equivalent automation.

[LEARN:audit] "Claim-vs-reality" is the highest-ROI audit lens for a governance-heavy template repo. More valuable than skill-consistency or doc-drift checks because it surfaces where the template oversells itself — the exact thing forkers will discover and call out.

[LEARN:audit] Whack-a-mole anti-pattern: surgically fixing a bot-flagged phrase in a summary paragraph usually introduces new drift in the same paragraph (3× on v1.6.1). Two flags on one paragraph = rewrite it structurally, don't patch word-by-word. See `summary-parity.md`.

## Verification Architecture (three complementary patterns)

[LEARN:pattern] Verification here operates at three architectural levels, each addressing a different failure mode. Do NOT collapse them — they are complementary, not redundant:

1. **Critic-fixer loop** (`/qa-quarto`, `/review-paper --adversarial`) — **two agents, serial** — one flags issues, the other applies fixes; loop until APPROVED. Best for **presentation + structural** bugs (Beamer↔Quarto parity, manuscript completeness). Both see the full artifact; the tension comes from role assignment.

2. **Cross-artifact review** (`/review-paper` + `/review-r` + `/audit-reproducibility`) — **horizontal dependency traversal** — a manuscript's claims depend on scripts' outputs, so the paper reviewer spawns script reviewers and reproducibility checkers alongside it. Best for **paper ↔ code consistency** (ATTs, coefficients, N match the outputs that produced them).

3. **Post-Flight Verification / CoVe** (`/verify-claims` + `claim-verifier` agent, v1.7.0) — **single agent, fresh-context fork** — the verifier has never seen the draft; it answers verification questions from the source material alone, using `context: fork` to architecturally enforce independence. Best for **factual hallucination** (fabricated citations, wrong dataset fields, misattributed findings). Adapted from Dhuliawala et al. 2023 ([arXiv:2309.11495](https://arxiv.org/abs/2309.11495)).

The key insight: each enforces independence differently — role tension, dependency-graph traversal, context isolation. A skill needing all three (e.g. `/review-paper --peer`) invokes them at different phases.

[LEARN:pattern] Post-Flight Reports (v1.7.0) are the output-side twin of Pre-Flight Reports (v1.6.0). Pre-Flight proves inputs were read, Post-Flight proves claims hold, and both use structured output blocks, fail-closed fallbacks, and explicit opt-outs. With summary-parity (v1.6.1) they form the **discipline-pattern trilogy** — input, framing, output discipline. Ask of a new text-generating skill: does it need all three?

[LEARN:audit] **Skill frontmatter `allowed-tools` must cover every tool the body invokes** — easy to miss, because the body reads as English ("spawn the verifier via Agent") while the frontmatter reads as a bureaucratic array. Four skills promised a tool in prose their `allowed-tools` omitted (PR #92, flagged by two external reviewers); the runtime failure is a permission error or a silent bypass. Sibling check: if rule X's `paths:` names skill Y, confirm Y actually implements X — rule-vs-implementation drift is the same bug one layer up.

[LEARN:audit] Deterministic bug classes (field exists, anchor resolves, count matches disk) belong in mechanical scripts — agent attention drifts, scripts don't. Reserve audit agents for judgment calls. `check-skill-integrity.py` ships the mechanical batch; `audit-pet-peeves.md` catalogues the judgment classes.

[LEARN:audit] When writing a parity-check regex, always strip inline code spans (` `` `) and fenced code blocks (` ``` `) before pattern-matching. Docs use example syntax like `[text](path#anchor)` inside backticks to illustrate; a naive regex treats those as real links. Replace matched code with spaces (preserving line numbers) before running the rest of the check.

[LEARN:audit] Audit-scope ATROPHY: audit agents only check what their prompt scopes, so any new code directory bypasses audit by default (6 bot-caught bugs in unscoped `scripts/`). **When adding a code location, expand audit scope first** — audit-debt accumulates silently.

## Scheduling Autonomous Work

[LEARN:scheduling] `CronCreate` is session-only in practice — it dies with the REPL (hit 2026-04-16 via a rate-limit termination). Work that must survive session death uses **Routines** (cloud-side). CronCreate is fine for short polling inside a live session, not "run this in an hour".

[LEARN:hooks] PreCompact hooks can BLOCK (modern protocol), which is how `pre-compact.py` can hold compaction while a plan is still DRAFT. Any such block must be opt-in, must fire at most once, and must fail open — a guard that can wedge a session is worse than the context it saves.

## v1.8.0 Cycle Lessons (2026-04-27)

[LEARN:permissions] **Protected-path behavior is mode-dependent — re-verify, never assume** (re-verified 2026-08-22 vs the permission-modes doc: `bypassPermissions` disables prompts and safety checks INCLUDING protected paths — the earlier "`.claude/` always prompts" version of this entry was stale). Auto mode classifier-gates risky actions and since 2026-08-14 is the built-in starting mode on Pro/Max/Team. Forkers in default mode still see prompts on `.claude/` edits.

[LEARN:vscode] **`claudeCode.allowDangerouslySkipPermissions` is a typo trap** — the canonical key has NO `claudeCode.` prefix (unlike `claudeCode.initialPermissionMode`). The wrong key is silently ignored. Documented in `TROUBLESHOOTING.md`.

[LEARN:edits] **Batch edits to protected `.claude/` paths: use Bash + `python3` heredoc.** Edit fires the protected-paths gate; Bash does not. For 5+ edits, one read→modify→write script via Bash avoids the prompt storm.

[LEARN:audit] **Surface-sync checks counts and MARKED tables** (`<!-- surface-sync-table: ... -->`, since v2.0) — tables without the marker are invisible to it (the guide appendix shipped 58 of 60 rows in v2.5 until a semantic sweep caught it). New skill/agent: add the row AND confirm the table is marker-covered or hand-checked.

[LEARN:pattern] **`disable-model-invocation: true` is load-bearing-write discipline.** Set it on skills writing persistent files the user must intend (lecture .tex, SKILL.md, preregistration); not on transient-report skills. It only blocks model auto-trigger; `/skill-name` still works. (Codified in `templates/skill-template.md`.)

## v1.9.0 Cycle Lessons (2026-05-20)

[LEARN:workflow] **Plan-first scales to multi-pass releases.** v1.9.0 shipped 6 skills + 2 agents + 2 rules across 9 PRs from one comprehensive plan file; each pass became a small reviewable PR, and mid-flight additions got a Pass slot in the plan. For multi-PR releases, the plan file is the navigation, not the conversation.

[LEARN:pattern] **Detect-only beats auto-rewrite for prose quality.** `/humanize` ships without `--rewrite`: cross-vendor findings show auto-rewriting AI-voice tells degrades quality and adds new tells. For any "fix my prose" skill, detect-and-flag with line numbers; the author edits. Same rationale keeps `/proofread` advisory.

[LEARN:pattern] **Distil-don't-truncate for long sessions.** Auto-compaction drops early turns; `/compress-session` writes a structured note instead (decisions, files, open questions, next actions, **discarded-as-noise**). Listing failed hypotheses explicitly stops them ghost-haunting future context. Companion to `/checkpoint`, not a replacement.

[LEARN:pattern] **Five-critic isolated voting beats single-critic composite judgment.** `/promote-memory` graduates `[LEARN]` entries via 5 forked critics (generality / staleness / redundancy / evidence / format), one dimension each, votes hidden from each other — isolation prevents groupthink. The user is the final gate even at 5-of-5. (Adapted with attribution from claudeblattman v2.1.)

[LEARN:pattern] **Provenance as a YAML artifact, not a folder.** `templates/passport-template.yaml`: per-paper numeric claims with source line, output field, tolerance, status; `/audit-reproducibility` rewrites it in place. Queryable beats folder reports. (Scope-reduced from Imbad0202/ARS "Material Passport" to numeric claims only.)

[LEARN:pattern] **Variance reporting > point estimate for peer review.** ~37% of verdicts vary purely from referee-disposition sampling (AgentReview, arXiv:2406.12708), so `--variance N` returns a verdict distribution + K-of-N concern table instead of one verdict. Bimodal spreads and tight majorities are both information. Referees route to Sonnet; hard cap N=5.

[LEARN:pattern] **HIGH-WARN must-fix for fabricated citations.** `/verify-claims` tiers: HIGH-WARN (fabricated reference / numerical or directional contradiction) is must-fix before commit; MED-WARN transient; LOW-WARN inaccessible source. Be conservative assigning HIGH-WARN — false positives erode the gate. The CoVe forked verifier (never sees the draft) is the architecture; the must-fix policy makes it consequential.

[LEARN:pattern] **70/20/10 model routing for cost discipline** (`model-routing.md`): Haiku tier mechanical, Sonnet tier review/critique, Opus tier high-judgment. 50–80% savings with no quality loss on the mechanical tier. Anti-pattern: down-tiering claim-verifier / methods-referee / editor — one false-positive PASS costs more than the routing saves. (Primary source: Anthropic "Decoupling brain from hands", Apr 2026.)

[LEARN:research] **Research-grounded plans beat eyeballed roadmaps.** When scope is "what should we add?", run parallel research agents first (ecosystem / community / cross-vendor / internal audit) and verify uncertainties before planning — the plan becomes traceable to URLs and verified facts instead of opinions. ~30 min of dispatch buys non-redundant, currently-true items.

[LEARN:workflow] **Surface-sync must check enumerative tables, not just counts.** Count assertions catch "N skills" drift but not missing table rows (the v1.5.0 agent trio was absent from README for 3 releases; the guide appendix shipped 58 of 60 rows in v2.5 until a semantic sweep caught it). Every skill/agent addition: update count assertions AND the guide appendix AND the README table.

## v2.5 Cycle Lessons (2026-08-21)

[LEARN:process] **Plan mode is not optional on a vague, multi-hour ask.** A vague "update our workflow" session with no plan mode, no spec, no `AskUserQuestion` paid the documented 30-50% rework: north star, guide plan, version scheme, and phase framing all rewritten mid-flight — each fixable by a 5-question spec in one turn. **Trigger: vague ask, multiple readings, >1 hour or >3 files → spec first, via `AskUserQuestion`.**

[LEARN:process] **Survey the machine before the world.** An ecosystem review searched the web first and found the owner's own `~/.claude/skills/` and private repos only after being asked — three times; the strongest material was local every time. **Order: own repos and `~/.claude/` → ecosystem → literature.**

[LEARN:framing] **Never write an exclusivity claim into a plan — it propagates to the webpage.** "The only public workflow that..." is unfalsifiable marketing. Use a dated survey finding plus repo-checkable claims. Banned in shipped copy: *the only, the first, nobody else, unmatched, best-in-class*.

[LEARN:process] **Do not propose restructuring an artifact you have not read.** A guide restructure drafted from its heading tree would have destroyed field-tested patterns that already solved the problem and handed every fork a merge conflict. **Headings are not the artifact.**

[LEARN:audit] **A green gate proves internal consistency, not external truth.** The model gate exited 0 while the SSoT named superseded tiers — surfaces merely agreed with each other. Currency gates need an external oracle plus a staleness expiry, or stale-but-consistent is indistinguishable from current.

[LEARN:audit] **Tool-name drift silently disarms hooks and gates.** When `Task` became `Agent`, 33 skills still declared `Task`, a `Bash|Task` hook matcher stopped firing, and the integrity checker certified the dead contract green. **Migrate tool names by registering both matchers, and source checker tool lists from the current reference, never hard-coded.**

[LEARN:safety] **Promoting a global skill into a public repo is a higher-blast-radius edit than it looks.** A candidate carried an unpublished paper's title and authors in its `description:` — and that field is a shared contract governing model auto-invocation machine-wide, so a global `~/.claude/skills/` edit has *wider* reach than a project one. **Scrub attributions with a fail-closed deny-list scan over publishable surfaces (pre-commit + CI, term list gitignored) before the port begins, and edit `description:` under `blast-radius`.**

[LEARN:audit] **A gate you did not re-qualify is a gate you may no longer have.** It goes quiet two ways: editing a *checked surface* can drop it out of coverage (a rewrite changed the count phrasing, gates stayed green because nothing matched — a gate that matches nothing reports nothing), and tuning a *checker* one way blinds the other. **After editing either, re-seed both directions: a planted defect must still be caught AND legitimate prose must still pass. A falling assertion count is the investigate signal.**

[LEARN:process] **Verify the branch actually changed before committing.** A `git checkout -b` bundled with a hook-blocked command never ran; ten commits landed on `main`. **A blocked hook fails the WHOLE call — anything bundled with it silently did not happen. After any branch op, echo `git rev-parse --abbrev-ref HEAD` and read it.**

[LEARN:governance] **Methodological content in the owner's own field ships only with the owner's CURRENT sign-off.** A skill was vetoed despite earlier commits recording sign-off: **a sign-off attaches to the content it reviewed, not to the surface's name** — after substantial edits or promotion into a public template it is void until renewed, however well the surface evals. Scope widened twice (2026-08-22/23): all prescriptive empirical-practice content, then causal methods generally. Taxonomy and conditional package pointers ship; prescriptions do not. Dated rulings: [`meta-governance.md`](.claude/rules/meta-governance.md).

## v2.5.1 Cycle Lessons (2026-08-23)

[LEARN:audit] **Gate every number you publish — including in the release that adds the rule.** A release stating *a count is a computation, not a reading* shipped three counts of its own test battery: one agent wrote the prose while another was still adding cases. **Sequence the change and its count — never parallelize them — and make the count derived**, so a checker recomputing it from source turns silent drift into a red gate.

[LEARN:safety] **When a check keeps leaking, stop patching cases — stop predicting.** A clean-tree guard tried to infer from a chained command whether the tree would still be dirty by the merge. Enumerating safe forms leaked; deny-on-doubt leaked less but still leaked, because each round found one more unmodelled dimension — flags, subcommands, segments, redirection, substitution — then a semantic one: `git stash` does not stash untracked files, so a correctly-parsed *this cleans the tree* was false. Deleting the prediction was necessary and not sufficient: a reading taken before execution proves only that the tree was clean when the command was *authorized*, and a referee chained a write ahead of the op on a clean tree. The class closed only once the op was also required to be a **standalone simple command** — nothing left on the line that could write in between. **Predicting an effect you could measure is itself the defect — and a measurement taken before the effect is not a measurement of it.**
