# DEVFORGE LITE — Quick Project Config
> Drop as CLAUDE.md. 14 core commands. Minimal overhead. Works immediately.
> For full version: use DEVFORGE_v5.md
> Generated: 2026-03-29
> Home: DevForgeAtlas-Org/DevForge-Atlas
> Source: packages/standalone/DEVFORGE_LITE.md

---

`HOME: DevForgeAtlas-Org/DevForge-Carta | SOURCE: DEVFORGE_LITE.md` *(Do not edit)*

`PROJECT: "" | STACK: "" | SCALE: AUTO | GIT: main`

## SESSION START
0. Check CONTEXT.md for interrupted `//ralph` run — if present, offer to resume from last checkpoint.
1. Read `devforge/CONTEXT.md` → active task, blockers
2. Read `devforge/ROADMAP.md` → current phase, next task
3. Resume from CONTEXT.md "Next priority"

---

## ARCHITECTURE RULES

- **One job per class/file.** >300 lines → decompose.
- **Layers:** Routes → Services → Repositories → Models. No skipping. No diagonal calls.
- **Feature folders:** `src/features/{name}/` — routes, service, repository, types, tests collocated.
- **Dependencies injected.** All external services behind an interface.
- **Async by default.** All I/O async/await. Connection pooling on DB.
- **No `any`.** Use `unknown` + type narrowing.

## SECURE CODING
- Auth check on EVERY route. Input validation on ALL inputs.
- No hardcoded secrets. `.gitignore` covers `.env*`, `*.key`, `*.pem`.
- N-1 version policy. `.github/dependabot.yml` must exist.
- `security:` commit type for all security changes (audit trail).

## COMMITS
```
type(scope): what changed

WHY was this change necessary?
```

---

## 14 COMMANDS

```
//catch-up           Full session start — reads all devforge/ docs, resumes work.
//where-are-we       Quick 2-step status check. No brain query. Faster than //catch-up.
//context-backup     [optional: session notes]
//update-roadmap     Sync ROADMAP.md with the actual state of the project.
//log-bug            [description]
//git-commit         [optional: message]
//git-branch         [name]
//build              [feature-name]
//fix                [description]
//new-feature        [name]
//quick-reference    Print all DevForge commands grouped by category.
//scaffold           Create devforge/ structure for a NEW project from scratch.
//ralph              Persistent loop — builds entire ROADMAP until 100% done. Checkpoints after every task.
//release [version]  Bump version, finalize CHANGELOG, tag, create GitHub release.
```

## 5-POINT CHECKLIST (//new-feature)

**Size it first:** S (<2h) · M (2-8h) · L (1-3d) · XL (3d+). XL → break into phases before building.

```
1. One job only
2. No layer skips
3. Auth on every route
4. Migration reversible
5. What to log and measure
```

## DOCS TO MAINTAIN
`CONTEXT.md` `ROADMAP.md` `BUGS.md` `CHANGELOG.md` `ARCHITECTURE.md`

Update docs AS PART of every task. PLAN before changes touching 2+ files.

## INTENT ROUTING
When input isn't a command: match intent, run the best match, announce it.
Ambiguous → show 2-3 options. No match → ask one question.

| Say... | Does... |
|---|---|
| "broken" / "error" / "not working" | //fix |
| "ship it" / "release" / "go live" | //release |
| "done for today" / "wrapping up" | //reflect + context save |
| "build [thing]" / "add [feature]" | //build |
| "what's next" / "what should I do" | ROADMAP next tasks |
| "write tests" / "test coverage" | //test-gen |
| "commit this" / "save work" | //git-commit |
| "security check" / "vulnerabilities" | //security-review |
| "set up this project" / "initialize" | //scaffold or //onboard |
| "build everything" / "finish it all" | //ralph |

## STANDING RULES
- **Blast radius:** Edits fine. Deletes/publishes/shared-state = approval first.
- **Scope:** No extras beyond the task (`//ralph` exempt).
- **Diagnose first:** Root cause before switching approach.
- **Honest:** Never imply success. Unverified = say so.
- **Minimal footprint:** No files beyond what the command requires.

## NEVER
Guess on security · Hardcode secrets · Skip auth · Swallow errors · Commit to main directly
