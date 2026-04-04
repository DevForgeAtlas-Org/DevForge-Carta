# DevForge — Platform Install Guide
> All standalone configs are generated from canonical plugin skills.
> To regenerate after skill changes: `cd packages/standalone && npm run generate`

---

## Quick Picks

| Situation | Use This |
|-----------|----------|
| I have Claude Code and just want it installed | Let Claude do it (Option 0) |
| I use Claude Code daily | Install the Plugin manually (Option 1) |
| I want a sidebar dashboard | Also install VS Code Extension (Option 2) |
| New project, no plugin | Drop `DEVFORGE_v5.md` as `CLAUDE.md` (Option 3) |
| Quick project, minimal overhead | Drop `DEVFORGE_LITE.md` as `CLAUDE.md` (Option 4) |
| I use ChatGPT | Paste `DEVFORGE_GPT.md` into Custom Instructions (Option 5) |
| I use GitHub Copilot | Copy `DEVFORGE_COPILOT.md` → `.github/copilot-instructions.md` (Option 6) |
| I use Cursor | Copy `DEVFORGE_CURSOR.md` → `.cursorrules` (Option 7) |
| I use Windsurf | Copy `DEVFORGE_WINDSURF.md` → `.windsurfrules` (Option 8) |

---

## Option 0: Let Claude Install It (Easiest)

**What you get:** Full plugin install — 91 commands, global brain, persistent across all sessions.
No commands to memorize. No docs to read. Claude handles everything.

### Prerequisites
- Claude Code app installed — [claude.ai/download](https://claude.ai/download)
- Claude Code CLI installed — `npm install -g @anthropic-ai/claude-code`

### Step 1: Open Claude Code and paste this

```
Install DevForge Atlas for me and walk me through setup:
https://github.com/DevForgeAtlas-Org/DevForge-Atlas
```

Claude will:
1. Clone the repo to `~/.devforge-plugin/`
2. Run `python3 devforge-install.py` — checks prerequisites, registers the marketplace, installs the plugin persistently
3. Verify 9 checks pass
4. Walk you through `//admin` first-run setup

### Step 2: Follow the prompts

Claude guides you through `//admin` (brain setup, SSH, remote sync) then `//scaffold` or `//onboard` depending on whether you're starting fresh or analysing an existing project.

### That's it

Every future session — terminal or desktop app — type `//quick-reference` to see all 91 commands. The plugin loads automatically, forever.

---

## Option 1: Claude Code Plugin (Primary — Manual Install)

**What you get:** All 91 commands, global brain, cross-project learning, git hooks, GitHub sync.
Works in Claude Code terminal and Claude Code desktop app.

### Prerequisites
- Claude Code installed (`claude --version` should show v2.x+)
- Node.js 20 LTS
- Git

### Step 1: Clone to your home directory
```bash
git clone git@github.com:DevForgeAtlas-Org/DevForge-Atlas.git ~/.devforge-plugin
```

> No SSH key yet? Use HTTPS instead:
> `git clone https://github.com/DevForgeAtlas-Org/DevForge-Atlas.git ~/.devforge-plugin`
> Then run `//setup-ssh` after installing to set up SSH properly.

### Step 2: Register the marketplace (once per machine)
```bash
claude plugin marketplace add $HOME/.devforge-plugin/packages --scope user
```

### Step 3: Install the plugin (once per machine)
```bash
claude plugin install devforge-atlas@devforge-local --scope user
```

### Step 4: Verify
Open Claude Code (terminal or desktop app) → start a **new session** → type:
```
//quick-reference
```
You should see the full 80-command reference table. Plugin is loaded and persistent.

> **Terminal only:** `claude plugin list` shows install status and any errors.
> **Desktop app:** `/plugin list` does not work — use `//quick-reference` to verify instead.

### Step 5: First-run setup
```
//admin
```
Initializes the brain and walks you through configuration.

### Step 6: New project
```
//scaffold
```

### Step 7: Existing project
```
//onboard
```

### Updating
```
//update-plugin
```
Runs `git pull` on `~/.devforge-plugin`. Brain data and project docs are never modified by updates.

---

## Option 2: VS Code Extension (Visual Layer)

**What you get:** Live sidebar dashboard — bug counts, roadmap progress, doc health, quality trend.
Requires the Claude Code plugin + brain to be installed first.

```bash
# Install from marketplace (when published)
code --install-extension devforge.devforge-vscode

# Or install from this package:
cd packages/vscode-extension
npm install && npm run build
code --install-extension devforge-*.vsix
```

---

## Option 3: Standalone — Full (Any Machine, No Install)

**What you get:** All 91 commands as text instructions. Full architecture rules. All 11 docs.
Uses context window tokens (no compiled intelligence). Works anywhere.

```bash
# New project:
cp packages/standalone/DEVFORGE_v5.md /path/to/your-project/CLAUDE.md

# Edit the IDENTITY BLOCK at the top (project name, tech stack, etc)
# Then in Claude Code / Claude Desktop: say "//scaffold"
```

Works with: Claude Code, Claude Desktop, Cursor (as .cursorrules), Windsurf (as .windsurfrules)

---

## Option 4: Standalone — Lite (Minimal Overhead)

**What you get:** 12 core commands, essentials only, under 200 lines. Fastest to get started.

```bash
cp packages/standalone/DEVFORGE_LITE.md /path/to/your-project/CLAUDE.md
```

---

## Option 5: ChatGPT Custom Instructions

1. Go to `chatgpt.com` → click your profile icon → Settings
2. Select "Custom Instructions"
3. In the **"How would you like ChatGPT to respond?"** box:
   - Paste the full contents of `packages/standalone/DEVFORGE_GPT.md`
4. Click Save
5. Start a new chat — these instructions apply to all future conversations

**Note:** You'll need to share your project docs (CONTEXT.md, ROADMAP.md etc) manually since ChatGPT has no file system access.

---

## Option 6: GitHub Copilot

```bash
# In your project root:
mkdir -p .github
cp packages/standalone/DEVFORGE_COPILOT.md .github/copilot-instructions.md
git add .github/copilot-instructions.md
git commit -m "docs: add DevForge Copilot instructions"
git push
```

Copilot picks up `.github/copilot-instructions.md` automatically in VS Code and GitHub web UI.

---

## Option 7: Cursor

```bash
cp packages/standalone/DEVFORGE_CURSOR.md /path/to/your-project/.cursorrules
```

**Optional: Connect the brain to Cursor**
Add to Cursor's MCP settings (`~/.cursor/mcp.json`):
```json
{
  "mcpServers": {
    "devforge-brain": {
      "command": "devforge-brain",
      "args": ["serve"]
    }
  }
}
```

Then restart Cursor. The brain will be available in Cursor's Cascade chat.

---

## Option 8: Windsurf

```bash
cp packages/standalone/DEVFORGE_WINDSURF.md /path/to/your-project/.windsurfrules
```

**Important for Windsurf Cascade:** Windsurf's Cascade is more autonomous than other tools.
The `.windsurfrules` file includes extra approval gate instructions — read them before using Cascade
for multi-file changes.

---

## Using Multiple Options Together

These options are complementary, not exclusive:

```
Recommended full setup on a primary machine:
├── Option 1: Claude Code Plugin (installed globally)
├── Option 2: VS Code Extension (installed once)
├── Option 6: Copilot instructions (per-repo, auto-applied)
└── Option 7: .cursorrules (per-repo, when opening in Cursor)

Recommended minimal setup on a secondary machine:
└── Option 3: DEVFORGE_v5.md as CLAUDE.md (copy to each project)

For any project shared with team members who don't use DevForge:
└── Option 6: Copilot instructions (committed to repo, benefits all Copilot users)
```
