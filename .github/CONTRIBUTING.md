# Contributing to DevForge Carta

## This repo is a read-only mirror

DevForge Carta is auto-published by CI from [DevForge Atlas](https://github.com/DevForgeAtlas-Org/DevForge-Atlas) on every release. Any changes made directly to this repo will be overwritten the next time a release is published.

## Where to contribute

**All issues and pull requests go to DevForge Atlas:**
→ https://github.com/DevForgeAtlas-Org/DevForge-Atlas

- Found a bug in a standalone file? Open an issue in Atlas.
- Want to improve a command or protocol? Open a PR in Atlas against `packages/standalone/`.
- Want to add a new command? Propose it in Atlas — the standalone files are generated from the plugin skills.

## Why this structure?

The standalone files are generated from the plugin skill files in Atlas. Editing them here would create drift. The Atlas monorepo contains the validation scripts that ensure every published file is consistent and correct.

Once your change is merged in Atlas and a new release is cut, Carta will automatically update within 2 minutes.
