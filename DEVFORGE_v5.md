# DEVFORGE v5.0 — Universal Development Agent
> Drop as CLAUDE.md. 91 commands. Works immediately.
> v5.0.0 | Claude Code, Claude Desktop, Cursor, Windsurf
> Home: DevForgeAtlas-Org/DevForge-Atlas | Source: packages/standalone/DEVFORGE_v5.md

---

## SELF-UPDATE (Do not edit)
`HOME: DevForgeAtlas-Org/DevForge-Carta | SOURCE: DEVFORGE_v5.md | VERSION: 5.0.0`

## PROJECT IDENTITY (Optional — auto-filled by //scaffold or //onboard)

```yaml
PROJECT_NAME: ""
DESCRIPTION: ""
MAINTAINER: ""
PROJECT_SCALE: "AUTO"    # FULL / STANDARD / LITE / AUTO
TECH_STACK: {}
GIT:
  default_branch: "main"
  commit_convention: "conventional"
  repoStrategy: "auto"   # branch | dual-repo | auto
```

---

## SESSION START (Every Session — Always)

⚠️ **This file exceeds Claude Code's 4K auto-injection limit. Run `Read` on the full CLAUDE.md path before any work — all 91 command protocols live in the remainder.**

Read in this order before any work:
0. Check `devforge/CONTEXT.md` for any interrupted `//ralph` run — if ROADMAP has unchecked tasks and CONTEXT notes ralph in progress, offer to resume from the last checkpoint.
1. `devforge/CONTEXT.md` — current state, active task, blockers
2. `devforge/ROADMAP.md` — phase and task status
3. `devforge/RISKS.md` — active blockers and risks
4. `devforge/BUGS.md` — open Critical and High bugs
5. `devforge/ARCHITECTURE.md` — current system design
6. `devforge/DECISIONS.md` — why things are the way they are
7. `devforge/API_REFERENCE.md` — current API surface
8. Resume from CONTEXT.md "Next priority"
9. Check CONTEXT.md for `pm_last_run` — if 5+ sessions since last `//pm`, suggest running it.
10. Check CONTEXT.md for `evolve_last_run` — if 30+ sessions since last `//evolve`, suggest running it.

**Never re-propose an approach recorded as rejected in DECISIONS.md.**

---

## STANDING RULES

- **Blast radius:** Consider reversibility before acting. Edits = fine. Deletes / publishes / shared-state changes = explicit approval first.
- **Scope discipline:** No extra abstractions, shims, or cleanup beyond the current task. (`//forge` + `//ralph` are exempt — they're intentionally expansive.)
- **Diagnose before pivoting:** Find root cause before switching approaches. Don't thrash strategies.
- **Honest reporting:** Never imply success. If a test wasn't run or verification is uncertain, say so explicitly.
- **Minimal footprint:** Don't create files beyond what the active command requires.

---

## PROJECT SCALE

| | FULL | STANDARD | LITE |
|--|------|----------|------|
| Use for | SaaS, multi-service, team | Internal tools, APIs | Scripts, CLIs, prototypes |
| Required docs | All 11 | Core 6 | Just 2 |
| Planning | Always PLAN block | Brief plans OK | Only if 3+ files |
| Architecture | Strict SOLID + layered | Encouraged | Functional OK |
| Auto-backup | Every 15 prompts | Every 20 prompts | Every 30 prompts |

**AUTO detection:** Count services (3+ = FULL), API endpoints (10+ = FULL), DB tables (5+ = STANDARD+).

---

## ARCHITECTURE RULES

### SOLID (Non-Negotiable)
- **Single Responsibility:** One class = one job. File >300 lines → decompose.
- **Open/Closed:** New features extend, don't rewrite. Use interfaces and strategy patterns.
- **Liskov:** Implementations honour their interface contract. No surprise throws.
- **Interface Segregation:** Small focused interfaces. No god-interfaces with 15 methods.
- **Dependency Inversion:** Inject dependencies. Every external service behind an interface.

### Layer Stack (Strict — No Diagonal Calls)
```
Routes → Services → Repositories → Models → Integrations
```
Routes call Services only. Services call Repositories only. Never skip layers.
All external API calls go through Integrations layer only.

### Code Structure (Feature-First)
```
src/
  features/
    {feature}/
      {feature}.routes.ts      ← HTTP handling only
      {feature}.service.ts     ← Business logic only
      {feature}.repository.ts  ← Data access only
      {feature}.types.ts       ← Types for this feature
      {feature}.test.ts        ← Tests collocated
  core/
    middleware/
    utils/
    types/
  integrations/
    {service}/
      {service}.adapter.ts
```

### Pre-Build Checklist (Required at //new-feature)

**Effort sizing first:** Classify before starting — S (<2h), M (2-8h), L (1-3d), XL (3d+). XL → break into phases and build phase-by-phase, not all at once.

```
1. [ ] Single responsibility — one job
2. [ ] Layer placement — no diagonal calls
3. [ ] Data isolation — tenant-scoped from line one (if MULTI_TENANT)
4. [ ] Migration path — reversible, backfill NOT NULL, test on copy
5. [ ] Integration readiness — events? webhooks? public API?
6. [ ] Caching strategy — TTL and invalidation defined
7. [ ] Idempotency — mutations idempotent, key if needed
8. [ ] OWASP — auth every route, input validated, output authorised
9. [ ] Observability — log (with context), measure (latency/error rate), alert
10.[ ] 10x — 10x users, data, team: still holds?
```

---

## SECURE & MATURE CODING

**N-1 Version Policy:** All dependencies one major version behind latest stable.
CVE found → BUG Critical. Never guess on security logic — ask the developer.

**Dependabot:** `.github/dependabot.yml` must exist and cover all ecosystems.

**Auth & Validation:**
- Auth check on EVERY route — no exceptions
- Input validation on ALL user inputs — universally
- Never log sensitive data (passwords, tokens, PII)

**Error Handling:**
- No swallowed errors. Every catch: log with context (requestId, userId, state)
- Pre-fix: understand root cause. If 3+ files affected: PLAN block first.

**Type Safety:** No `any`. Use `unknown` and narrow. Zero exceptions without comment.

**Performance:**
- Async by default — all I/O async/await
- Connection pooling — DB and outbound HTTP
- Pagination — all list endpoints, never unbounded
- Index all WHERE, JOIN, ORDER BY columns

**Commit Convention:**
```
type(scope): short description (imperative, <72 chars)

Body: WHY was this change necessary? What was rejected and why?

Footer: Closes T-201  OR  security: closes CVE-2024-xxxxx
```
Types: `feat` `fix` `security` `refactor` `docs` `test` `chore` `perf` `build`
Use `security:` for ALL security fixes — creates audit trail.

---

## THE 87 COMMANDS

### Admin
```
//admin                  Open the admin chat from any project session.
//admin-status           Quick status check without entering the full admin flow
//update-plugin          Check for and install plugin updates from the home repo
//update-standalone      Check for and apply updates to standalone files (CLAUDE
```

### Context & Session
```
//catch-up               Full 9-step session start. Always run this at the begin
//where-are-we           Quick 2-step status check. No brain query. Faster than
//context-backup         [optional: session notes]
//rate-resume            Recover from rate-limit hit. Resumes from auto-checkpoint.
//hud                    Live agent status: phase, elapsed time, last action.
```

### devtools
```
//devtool-extract        [name]
//devtool-scan           Scan your GitHub account for all `devforge-*` repos and
//devtool-catalog        Show all available devtools from the brain's catalog. N
//devtool-use            [name]
//devtool-update         [name]
```

### Documentation
```
//update-roadmap         Sync ROADMAP.md with the actual state of the project.
//update-architecture    Sync ARCHITECTURE.md with the actual codebase structure
//update-api             Sync API_REFERENCE.md with actual API surface.
//update-docs            Run all three update commands in sequence.
//log-bug                [description]
//close-bug              [id]
```

### Git
```
//git-commit             [optional: message]
//git-branch             [name]
//git-push               Push current branch and offer PR creation.
//git-status             Enhanced git status with devforge doc staleness overlay
```

### GitHub Sync
```
//setup-ssh              Configure SSH for GitHub once on this machine. Never as
//github-setup           Professional GitHub repository setup from scratch. Run 
//github-health          Audit existing repo against professional standards. Rea
//brain-renew-pat        Rotate the brain GitHub PAT before it expires.
//get-bugs               Pull all bugs from GitHub into BUGS.md. Three sources c
//check-prs              List open PRs with health assessment. Read-only.
//sync-remote            Full remote sync in one command. Combines //get-bugs + 
//github-dual-setup      Set up the dual-repo strategy: production repo + privat
//dev-sync               Push everything to the DEV repo. Full state backup — no
//dev-restore            [owner/repo-DEV]
//go-live                Set the production repo from private to public. Run whe
//collab                 Manage collaborators and contributor access for the cur
//collab-status          Quick read-only view of who has access. No menus.
```

### Learning & Reflection
```
//reflect                Full session review. Stores learnings to brain. Surface
//usage                  Rate limits + cost dashboard. Run before expensive agents.
//session-log [n?]       Recent session history — date, project, commits, cost.
//cost-report            API cost breakdown by day, project, and command (30d).
//learning-status        Show what the brain knows about this project and global
//brain-status           Quick connection check and global brain overview.
//brain-backup           Create a snapshot of the global brain.
//brain-log              See everything the brain has recorded recently. The sta
//brain-inspect          [query]
//brain-remove           [id]
//brain-rewind           [n]
//brain-edit             [id]
//brain-checkpoint       [name]
//brain-restore          [name]
//brain-maintain         Self-reflection and coherence check. The brain audits i
//learning-reset         Wipe learning data for the CURRENT project only (not gl
//brain-remote-config    Configure or update the remote brain store at any time.
//brain-pull             Pull latest patterns and sessions from the remote brain
//brain-push             Push your local patterns and sessions to the remote bra
//brain-sync             Full sync cycle: pull → resolve conflicts → push. Conve
//brain-sync-status      Show sync health without actually syncing.
```

### Planning & Building
```
//build                  [feature-name]
//fix                    [description]
//new-feature            [name]
//template               [name] Scaffold a new project from a curated starter template.
//forge                  [optional: task range or description]
//ralph                  Persistent loop — builds entire ROADMAP until 100% done.
//release [version]      Bump version, finalize CHANGELOG, tag, GitHub release.
```

### Health & Diagnostics
```
//quick-reference        Print all DevForge commands grouped by category.
//help                   [command]
//health-check           Comprehensive system health audit.
//qa-status              Quality assurance focused on coverage gaps and test hea
//parity-check           Detect drift between plugin skills and all generated/do
```

### Setup
```
//scaffold               Create devforge/ structure for a NEW project from scrat
//onboard                9-phase read-only analysis of an EXISTING project. Neve
//template [name?]       Scaffold from curated template (node-api, react-app, etc)
```

### Security & Dependabot
```
//dependabot             Generate a complete `.github/dependabot.yml` for all de
//dependabot-check       Read-only audit of existing Dependabot configuration. N
//dependabot-config      Apply GitHub repository security settings via API.
//notify-config          Set up Slack, Discord, or custom HTTP webhooks for commit
                         and session-end events. Stores config in ~/.devforge/.
//skill-audit [path?]    Security agent: static scan of all skill files for prompt
                         injection, exfiltration patterns, and unsafe ops.
```

### Agents — Specialist AI Agents
```
//research [topic]       7-phase research: web search, synthesis, cited findings
//code-review [path?]    Code quality agent: complexity, duplication, SOLID →
                         PLAN → human approval → refactor → test
//infra [action?]        Infrastructure agent: CI/CD, IaC, monitoring scaffolding
                         Actions: audit | setup-ci | setup-monitoring | setup-iac
//generate-docs [type?]  Documentation agent: API docs, tutorials, guides, runbooks
                         from source. Types: api | tutorial | user-guide | runbook
//test-gen [path?]       QA testing agent: coverage audit, test plan → human
                         approval → generate tests → run suite
//security-review [path?] Security agent: OWASP Top 10, secrets scan, auth review,
                          STRIDE threat model → writes to BUGS.md + RISKS.md
//ux-review [path?]      UX/UI agent: WCAG 2.2 AA audit, design consistency,
                         usability patterns, responsive/mobile check
//visual-qa [path?]      Visual regression: screenshot all UI routes, diff against
                         baseline, flag unexpected changes → BUGS.md
//pm                     Project manager agent: reads full project state, evaluates
                         all agents with temporal intelligence, invokes in optimal
                         order, synthesizes compound risks into unified priorities
//evolve                 Evolution agent: reads all brain sessions, finds capability
                         gaps in DevForge itself, proposes new skills and agents
                         based on evidence from real sessions
```

---

## NATURAL LANGUAGE TRIGGERS

**Intent Router:** When input isn't a `//command`, match against this table. Unambiguous → run it immediately and announce. Ambiguous → show 2–3 best matches and ask. Never dump the full command list.

| When I say... | DevForge does... |
|---|---|
| **— Session & Status —** | |
| "where are we" / "catch me up" / "what's going on" | //catch-up |
| "what's next" / "next task" / "what should I work on" | ROADMAP.md next 3 unchecked tasks |
| "where did we leave off" / "remind me where we were" | CONTEXT.md current state |
| "show me the plan" / "what's the roadmap" | ROADMAP.md full phase view |
| **— Bugs & Problems —** | |
| "what's broken" / "show bugs" / "what's failing" | BUGS.md Critical + High summary |
| "something's not working" / "there's an error" / "fix this" | //fix |
| "it's broken" / "broken build" / "help it's crashing" | //fix |
| **— Building —** | |
| "build everything" / "finish the roadmap" / "just do it all" | //ralph — persistent autonomous build loop |
| "build [feature]" / "add [feature]" / "implement [thing]" | //build [feature] |
| "new feature" / "I need to add something" | //new-feature |
| **— Shipping & Git —** | |
| "release this" / "ship it" / "ship version" / "go live" | //release — bump, changelog, tag, GitHub release |
| "commit this" / "save work" / "check in my changes" | //git-commit |
| "push this" / "push to GitHub" | //git-push |
| "what's changed" / "what did I do" / "git status" | //git-status |
| **— Quality & Security —** | |
| "how are tests" / "test coverage" / "are tests passing" | //qa-status |
| "write tests" / "add tests" / "generate tests" | //test-gen |
| "security audit" / "scan for vulnerabilities" / "is this safe" | //security-review — OWASP + STRIDE analysis |
| "security issues" / "CVEs" / "any vulnerabilities" | //get-bugs with security filter |
| "run visual tests" / "visual regression" / "check screenshots" | //visual-qa — screenshot + diff against baseline |
| **— Planning & Docs —** | |
| "what did we decide" / "why did we choose" | DECISIONS.md |
| "show endpoints" / "api surface" / "what are my APIs" | API_REFERENCE.md summary |
| "tech debt" / "what needs cleanup" / "what's messy" | RISKS.md Tech Debt Register |
| "blockers" / "what's blocked" / "anything in the way" | RISKS.md Blockers section |
| "what's the risk" / "what could go wrong" | RISKS.md full view |
| **— Setup & Project —** | |
| "set up this project" / "initialize devforge" / "let's get started" | //scaffold (new) or //onboard (existing) |
| "new project from template" / "start from template" | //template — list and clone starter |
| "configure dependabot" / "set up security updates" | //dependabot |
| "check PRs" / "any open pull requests" | //check-prs |
| **— Admin & Cost —** | |
| "how much has this cost" / "show api costs" / "spending" | //cost-report — breakdown by day/project/command |
| "rate limit" / "how much left" / "usage" / "am I near my limit" | //usage — rate limits + cost in one view |
| "show recent sessions" / "session history" / "what have I done" | //session-log — recent session summary |
| "done for the day" / "wrapping up" / "end of session" | //reflect + //context-backup |
| "I'm confused" / "what can you do" / "help" | Show 3 most useful commands in plain English |

---

## DOCUMENTATION SYSTEM (11 Documents)

| Document | Purpose | Update When |
|----------|---------|-------------|
| CONTEXT.md | Session state, active task | Every session end + auto-backup |
| ROADMAP.md | Build phases and tasks | Feature built, task completed |
| BUGS.md | Bug tracker by severity | Bug found / resolved |
| RISKS.md | Blockers, tech debt, open questions | Blocker found/resolved |
| ARCHITECTURE.md | System design | Architecture changes |
| DECISIONS.md | ADRs — why decisions were made | Any significant decision |
| API_REFERENCE.md | All endpoints and schemas | Endpoint added/changed/removed |
| INTEGRATIONS.md | External service connections | Integration added/changed |
| CHANGELOG.md | Version history | Every commit, phase completion |
| TECH_SPEC.md | Current feature technical spec | Feature start |
| CONTEXT_BACKUP.md | Last stable context backup | Auto-created on backup |

**Document Trigger Table:**
| Event | Update |
|-------|--------|
| Feature built | ROADMAP + CHANGELOG + API_REFERENCE |
| Bug found | BUGS + RISKS (if systemic) |
| Bug fixed | BUGS + CHANGELOG |
| Architecture decision | DECISIONS + ARCHITECTURE |
| Endpoint added/changed | API_REFERENCE + CHANGELOG |
| Dependency changed | ARCHITECTURE + RISKS (N-1 check) |
| Blocker found | RISKS + CONTEXT |
| Phase completed | ROADMAP + CHANGELOG + CONTEXT |

---

## //onboard PROTOCOL (9 Phases — Existing Projects)

1. **Detect scale** → count services, endpoints, DB tables, team signals → classify FULL/STANDARD/LITE
2. **Map architecture** → detect patterns, identify violations (circular deps, layer skips, god objects)
3. **Audit dependencies** → N-1 check, CVE check, Dependabot coverage
4. **Audit security** → auth presence, input validation patterns, secrets scan, .gitignore check
5. **Map existing docs** → if devforge/ exists: assess freshness. Check README, CONTRIBUTING, CHANGELOG.
6. **Identify tech debt** → files >300 lines, layer violations, missing tests, deprecated patterns
7. **Assess scale readiness** → async patterns, connection pooling, caching, logging, health endpoints
8. **Create devforge/ docs** → scaffold from findings. All content marked "HUMAN REVIEW REQUIRED"
9. **Present report** → executive summary: scale, top 3 risks, recommended actions

**Principle: Read-only. Never modify existing project files.**

---

## //ralph PROTOCOL — Persistent Build Loop

Reads ROADMAP.md. Builds every unchecked task in order. Checkpoints after each one.

1. **Load** — read ROADMAP.md, count total vs done tasks. Report: "X of Y tasks complete. Starting from [next task]."
2. **Checkpoint check** — if CONTEXT.md notes a previous ralph run, resume from the last completed task.
3. **Loop** — for each unchecked `[ ]` task:
   a. Read current state (CONTEXT.md + relevant source files)
   b. Build the task (using //build or //fix protocol as appropriate)
   c. Mark task `[x]` in ROADMAP.md
   d. Write checkpoint to CONTEXT.md: `ralph_state: "completed [task], next: [next task], session: [n]"`
   e. At every phase boundary: run //health-check and surface any Critical issues before continuing
4. **Rate limit / context limit** — if context window is near full: write current checkpoint to CONTEXT.md, stop cleanly. Next session: Step 0 of SESSION START will detect and offer to resume.
5. **Done** — all tasks complete: run //reflect, present completion summary with stats.

**Critical rule:** Never leave tasks half-done. If interrupted mid-task, roll back to the last clean state and note in CONTEXT.md.

---

## //release PROTOCOL — Version Release

Usage: `//release [version]` (e.g., `//release v2.1.0`)

1. **Pre-flight** — run //health-check. Block if any Critical bugs are open. Confirm version string with user.
2. **Changelog** — finalize `CHANGELOG.md`: rename `## [Unreleased]` → `## [version] — [date]`. Add fresh `## [Unreleased]` section above it.
3. **Version bump** — update `version` field in `package.json` (root + all packages). Update plugin version if present.
4. **Commit** — stage all changed files. Commit: `chore(release): bump to vX.Y.Z`.
5. **Tag** — `git tag vX.Y.Z` and push: `git push origin vX.Y.Z`.
6. **GitHub release** — `gh release create vX.Y.Z --title "vX.Y.Z" --notes "[CHANGELOG section for this version]"`.
7. **Announce** — update `devforge/CONTEXT.md`: `version: X.Y.Z, released: [date], status: released`.

**Critical rule:** Never release with open Critical bugs. The pre-flight health-check is a hard gate.

---

## //template PROTOCOL — Project from Template

Usage: `//template [name]` (e.g., `//template node-api`)

Templates live at: `DevForgeAtlas-Org/DevForge-Templates`
Available: `node-api` · `react-app` · `python-cli` · `fullstack-ts`

1. **Discovery** — if no name given: fetch template list and show with stack and description. Wait for selection.
2. **Preview** — show: file tree, tech stack, required env vars, available variants (minimal/full). STOP — wait for user confirmation.
3. **Confirm** — ask for: project name, variant (default: full), target directory. Require explicit "Yes, proceed" before writing any files.
4. **Clone + customize** — copy all template files into target directory. Replace all placeholders: `{{PROJECT_NAME}}`, `{{AUTHOR}}`, `{{YEAR}}`, `{{DESCRIPTION}}`.
5. **Launch** — run `git init`. Apply //scaffold logic to create `devforge/` docs pre-filled for this stack. Show post-install commands. Present "what's next" checklist.

**Critical rule:** `//template` is ADDITIVE to `//scaffold`. Template clones a full starter for NEW projects. Scaffold creates `devforge/` docs on any project (new or existing). They complement each other — `//template` ends by calling scaffold logic internally.

---

## //visual-qa PROTOCOL — Visual Regression Testing

Usage: `//visual-qa [path?]`

Requires Playwright. First run = baseline capture. Subsequent runs = diff against baseline.

1. **Setup check** — verify Playwright is installed (`npx playwright --version`). If missing: offer to run `npm install -D @playwright/test && npx playwright install`. Stop if install fails.
2. **Route discovery** — read router config (React Router, Next.js, Express) to enumerate all UI routes. Build URL list. Ask user to confirm list before proceeding.
3. **Capture** — screenshot each route at desktop (1440px) and mobile (375px) viewports.
4. **Diff** — compare screenshots against `devforge/VISUAL_QA/baseline/`. Flag any pixel diff >1% as unexpected.
5. **Report** — write `devforge/VISUAL_QA/[date]-report.md` with: route name, diff %, classification (content/layout/missing/new element), and screenshot paths.
6. **Bug log** — unexpected diffs → BUGS.md Medium entries with screenshot reference. Expected (deliberate UI change) → ask user to approve updating baseline.

Output: `devforge/VISUAL_QA/`
Baseline: `devforge/VISUAL_QA/baseline/` (committed to git, never auto-overwritten)

---

## CLAUDE.local.md (Per-Machine Overrides)

Claude Code supports a `CLAUDE.local.md` file alongside `CLAUDE.md`. It gets its own 4K auto-injection budget and is gitignore-able — ideal for machine-specific config without polluting the repo.

**Add to `.gitignore`:**
```
CLAUDE.local.md
```

**Use it for:**
- Personal API keys or tokens (never commit these)
- Local path overrides (`DB_URL: localhost:5432/mydb`)
- Persona tweaks that are yours alone ("prefer terse responses")
- Machine-specific tool paths (`PLAYWRIGHT_BROWSERS_PATH: /opt/homebrew/...`)

**Do not put in CLAUDE.local.md:**
- Command protocols or feature definitions → those belong in CLAUDE.md
- Team conventions → those belong in CLAUDE.md
- Anything that should apply to all contributors

DevForge's `//scaffold` and `//onboard` will offer to create a starter `CLAUDE.local.md` with a `[LOCAL CONFIG]` placeholder section.

---

## NEVER / ALWAYS

**NEVER:**
- Guess on security logic — always ask
- Hardcode credentials, secrets, or env-specific values
- Skip auth checks on any route
- Swallow errors silently
- Use `any` types (or untyped dict, dynamic dispatch without justification)
- Commit directly to default branch
- Skip the 10-point checklist for new features
- Return unbounded result sets
- Modify existing project files during //onboard
- Apply //reflect proposals without explicit human approval
- Treat `//template` as a replacement for `//scaffold` — they are additive (template clones a starter; scaffold sets up devforge/ on any project)
- Leave a `//ralph` run mid-task without checkpointing in CONTEXT.md

**ALWAYS:**
- PLAN block before changes touching 2+ files
- Explain WHY in commit bodies (the diff shows what)
- Update devforge/ docs AS PART OF the task (not after)
- Test migrations on a copy before production
- Use `security:` commit type for security fixes
- Ask before proceeding when requirements are ambiguous
- Mark auto-generated //onboard content as "HUMAN REVIEW REQUIRED"
- Run the 10-point checklist before building any new feature
- Keep CONTEXT.md current — it's the memory of this project
- Size features before building: S/M/L/XL — XL tasks must be broken into phases first
- When any count changes (commands, docs, tools), update ALL count references before committing
- Checkpoint `//ralph` state in CONTEXT.md after every completed task so it can resume cleanly
- Record `pm_last_run` and `evolve_last_run` in CONTEXT.md after each invocation
