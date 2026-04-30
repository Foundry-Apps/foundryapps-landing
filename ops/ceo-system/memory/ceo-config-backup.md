---
name: CEO config backup repo
description: Foundry-Apps/ceo-config (private) — git-tracked snapshot of .auto-memory/ and global CLAUDE.md. First seeded 2026-04-19.
type: reference
originSessionId: a3a07943-25ea-4687-842b-baa4fad0c808
---
Private repo: https://github.com/Foundry-Apps/ceo-config

**What's tracked:**
- `auto-memory/MEMORY.md` + individual memory files
- `auto-memory/_archive/` — historical memories (kept for provenance)
- `claude/CLAUDE.md` — global user instructions

**Why:** The source files live in the Cowork VM mount, not otherwise git-tracked. This repo is the safety net against machine rebuild / mount corruption / accidental deletion.

**Initial snapshot:** 6a8e08c0611f (2026-04-19) — 74 files.

**Restore procedure:**
1. Clone `Foundry-Apps/ceo-config` locally.
2. Copy `auto-memory/*` back into the Cowork VM mount path (`/sessions/<session>/mnt/.auto-memory/` from VM, or its host-side equivalent).
3. Copy `claude/CLAUDE.md` into the Cowork VM mount path (`/sessions/<session>/mnt/.claude/CLAUDE.md`).
4. Restart Cowork.

**Sync cadence:** Initial snapshot only as of 2026-04-19. Automated daily sync is NOT set up yet — ongoing changes to memory/CLAUDE.md need manual re-sync. On-demand: ask Claude to "sync the CEO config repo".

**How to apply:** If you're making significant memory or CLAUDE.md changes, bump the repo within ~24h. Otherwise drift risk accumulates. Consider promoting to scheduled task if manual cadence proves unreliable.
