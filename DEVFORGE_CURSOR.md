# DEVFORGE for Cursor
# File: .cursorrules
# Full command set — Cursor supports //commands via chat panel.
# Generated: 2026-03-27
# Home: DevForgeAtlas-Org/DevForge-Atlas
# Source: packages/standalone/DEVFORGE_CURSOR.md

## Session Start
On every new chat session: read devforge/CONTEXT.md and devforge/ROADMAP.md first.
If devforge/ doesn't exist: suggest running //scaffold.

## DevForge Brain (If MCP Available)
If devforge-brain MCP server is configured:
- Session start: call brain_session_start, load relevant patterns
- //reflect: call brain_store_pattern for each learning
- Session end: call brain_session_end to score session
If brain not available: continue normally — all functionality works without it.

## Commands
```
//admin                  Open the admin chat from any project session.
//admin-status           Quick status check without entering the full admin flow
//update-plugin          Check for and install plugin updates from the home repo
//update-standalone      Check for and apply updates to standalone files (CLAUDE
//catch-up               Full 9-step session start. Always run this at the begin
//where-are-we           Quick 2-step status check. No brain query. Faster than 
//context-backup         [optional: session notes]
//devtool-extract        [name]
//devtool-scan           Scan your GitHub account for all `devforge-*` repos and
//devtool-catalog        Show all available devtools from the brain's catalog. N
//devtool-use            [name]
//devtool-update         [name]
//update-roadmap         Sync ROADMAP.md with the actual state of the project.
//update-architecture    Sync ARCHITECTURE.md with the actual codebase structure
//update-api             Sync API_REFERENCE.md with actual API surface.
//update-docs            Run all three update commands in sequence.
//log-bug                [description]
//close-bug              [id]
//git-commit             [optional: message]
//git-branch             [name]
//git-push               Push current branch and offer PR creation.
//git-status             Enhanced git status with devforge doc staleness overlay
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
//reflect                Full session review. Stores learnings to brain. Surface
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
//build                  [feature-name]
//fix                    [description]
//new-feature            [name]
//forge                  [optional: task range or description]
//quick-reference        Print all DevForge commands grouped by category.
//help                   [command]
//health-check           Comprehensive system health audit.
//qa-status              Quality assurance focused on coverage gaps and test hea
//parity-check           Detect drift between plugin skills and all generated/do
//scaffold               Create devforge/ structure for a NEW project from scrat
//onboard                9-phase read-only analysis of an EXISTING project. Neve
//dependabot             Generate a complete `.github/dependabot.yml` for all de
//dependabot-check       Read-only audit of existing Dependabot configuration. N
//dependabot-config      Apply GitHub repository security settings via API.
```

## Architecture Rules
- Layer stack (strict): Routes → Services → Repositories → Models → Integrations
- Feature-first folders: src/features/{name}/ with routes/service/repository/types/test
- No diagonal calls between layers
- All external service calls through Integrations layer only
- Inject dependencies — never import concrete classes directly

## Pre-Build Checklist (Required at //new-feature)
1. Single responsibility
2. Layer placement — no diagonal calls
3. Data isolation if multi-tenant
4. Migration reversible
5. Integration surface defined
6. Caching strategy: TTL + invalidation
7. Idempotency: mutations idempotent
8. OWASP: auth every route, input validated
9. Observability: log, measure, alert defined
10. 10x scale: still holds?

## Secure Coding
- Auth on EVERY route — no exceptions
- Input validation universally
- No hardcoded secrets — env vars only
- N-1 version policy — all deps
- security: commit type for all security changes

## Always
- PLAN block before any change touching 2+ files
- WHY in commit bodies
- Update devforge/ docs as part of every task
- Mark //onboard auto-generated content "HUMAN REVIEW REQUIRED"
