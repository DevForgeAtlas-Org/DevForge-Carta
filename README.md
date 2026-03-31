# DevForge Carta

> Auto-published standalone files from [DevForge Atlas](https://github.com/DevForgeAtlas-Org/DevForge-Atlas).
> Drop a file into any project as `CLAUDE.md` — works immediately, zero install required.

---

## What is Carta?

**Carta** is the standalone delivery channel for DevForge. Every time a new version of DevForge Atlas ships, these files are automatically published here by CI. You never need to visit the Atlas monorepo — just grab the file you need from this repo.

**This repo is a read-only mirror.** All source files live in [DevForge-Atlas](https://github.com/DevForgeAtlas-Org/DevForge-Atlas). To contribute, open issues or PRs there, not here.

---

## Which File Should I Use?

| File | Use when | Size |
|------|----------|------|
| [`DEVFORGE_v5.md`](./DEVFORGE_v5.md) | You want the full DevForge experience — all 87 commands, complete protocols, every feature | ~80KB |
| [`DEVFORGE_LITE.md`](./DEVFORGE_LITE.md) | Scripts, CLIs, quick prototypes — minimal overhead, 14 core commands | ~10KB |
| [`DEVFORGE_COPILOT.md`](./DEVFORGE_COPILOT.md) | GitHub Copilot (`.github/copilot-instructions.md`) | ~15KB |
| [`DEVFORGE_CURSOR.md`](./DEVFORGE_CURSOR.md) | Cursor IDE (`.cursorrules`) | ~15KB |
| [`DEVFORGE_WINDSURF.md`](./DEVFORGE_WINDSURF.md) | Windsurf IDE (`.windsurfrules`) | ~15KB |
| [`INSTALL_GUIDE.md`](./INSTALL_GUIDE.md) | Full install instructions for all DevForge delivery methods | reference |

---

## How to Use (60 Seconds)

**Option 1 — Drag and drop:**
```bash
# Download DEVFORGE_v5.md and rename it
curl -o CLAUDE.md https://raw.githubusercontent.com/DevForgeAtlas-Org/DevForge-Carta/main/DEVFORGE_v5.md
```

Drop `CLAUDE.md` into your project root. Open Claude Code (or Claude Desktop, Cursor, Windsurf). That's it.

**Option 2 — Direct raw URL** (bookmark this):
```
https://raw.githubusercontent.com/DevForgeAtlas-Org/DevForge-Carta/main/DEVFORGE_v5.md
```

**Option 3 — Self-updating:** Once you have `DEVFORGE_v5.md` as your `CLAUDE.md`, run `//update-standalone` at any time to pull the latest version while preserving your project identity.

---

## Want the Full Plugin?

The standalone files give you DevForge's protocols and commands as pure text — no install required. If you want the full power (global brain, session learning, VS Code sidebar, 79 MCP tools), install the plugin:

```bash
npm install -g devforge-atlas
devforge-init
```

→ [DevForge Atlas on GitHub](https://github.com/DevForgeAtlas-Org/DevForge-Atlas)

---

## How Carta Stays Current

Every time a new DevForge Atlas release is published:

1. Atlas CI runs both validation scripts (`validate-standalone.sh` + `validate-skill-counts.sh`)
2. If validation passes → all standalone files are automatically pushed to this repo
3. If validation fails → the push is blocked — this repo stays clean

You always get a verified, consistent set of files. Drift is structurally impossible.

Current version: see [`carta_version.json`](./carta_version.json)

---

## Want to Start a New Project from a Template?

Check out [DevForge Templates](https://github.com/DevForgeAtlas-Org/DevForge-Templates) — full project scaffolds for `node-api`, `react-app`, `python-cli`, and `fullstack-ts`. Each ships with source code, CI, and a pre-filled `devforge/` directory.

---

## Contributing

**Issues and PRs go to [DevForge-Atlas](https://github.com/DevForgeAtlas-Org/DevForge-Atlas), not here.**

This repo is auto-published by CI. Any changes made here directly will be overwritten on the next release. If you want to improve the standalone files, improve the skills in Atlas and they'll show up here automatically.

See [CONTRIBUTING.md](./.github/CONTRIBUTING.md) for details.

---

*Part of the [DevForge Atlas](https://github.com/DevForgeAtlas-Org/DevForge-Atlas) ecosystem.*
*Atlas · Carta · [Templates](https://github.com/DevForgeAtlas-Org/DevForge-Templates)*
