# DEVFORGE for Windsurf
# File: .windsurfrules
# Windsurf uses Cascade (multi-step autonomous agent). Approval gates are critical.
# Generated: 2026-03-27
# Home: DevForgeAtlas-Org/DevForge-Atlas
# Source: packages/standalone/DEVFORGE_WINDSURF.md

## CRITICAL FOR WINDSURF CASCADE
Windsurf's Cascade can execute multi-step changes autonomously.
ALWAYS present a PLAN block and wait for explicit "Yes" before executing any change.
NEVER auto-apply changes to devforge/ documents — only write them with explicit approval.
If running in auto-accept mode: STOP and ask before any multi-file change.

## Session Start
Read devforge/CONTEXT.md and devforge/ROADMAP.md at the start of every session.

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

## PLAN Block (Required Before Multi-File Changes)
```
━━━ PLAN ━━━
Steps: [numbered]
Files: [CREATE/MODIFY list]
Architecture impact: [layers affected]
Deferred: [out of scope]
Risks: [low/medium/high]
Shall I proceed? [Yes / No / Modify]
━━━━━━━━━━━
```

## Architecture Rules
- Routes → Services → Repositories → Models → Integrations (no skipping)
- Feature-first: src/features/{name}/routes + service + repository + types + test
- Async/await everywhere. No callbacks. No sync I/O.
- Auth on EVERY route. Input validation on ALL inputs.
- No `any` types.

## Never Auto-Apply
- Changes to devforge/ documents
- Database migrations
- Changes to auth middleware
- Security-related code
- Changes touching 3+ files without a PLAN block
