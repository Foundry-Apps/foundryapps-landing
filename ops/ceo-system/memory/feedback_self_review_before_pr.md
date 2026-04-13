---
name: Self-review diff before creating PR
description: Must run git diff master..HEAD or explicitly read all changed files BEFORE pushing and creating a PR — Stop hook enforces this
type: feedback
---

Run `git diff master...HEAD` (or read all changed files) BEFORE creating a PR. The Stop hook checks the session transcript for evidence of this review.

**Why:** The Stop hook verifies a diff review happened before PR creation. If `git push` and PR creation appear in the transcript without a preceding diff, the hook returns `{"ok": false}` and flags the violation.

**How to apply:**
- The ONLY valid sequence is: edit → commit → `git diff master...HEAD` → push → PR
- `git diff master...HEAD` must be the very next bash command after `git commit` — do not run push or PR creation before it
- Do NOT interleave other steps (TodoWrite, expo export, etc.) between commit and diff — run diff immediately after commit
- Reading individual files does NOT satisfy the hook — an explicit `git diff` command must appear in the transcript before the push
- `git diff --no-index` on untracked files before staging does NOT satisfy the requirement — only `git diff master...HEAD` after committing counts
- `git diff --cached --stat` does NOT satisfy the requirement — it only shows staged changes, not the branch vs master comparison. The exact form `git diff master...HEAD` is required.
- The review must come BEFORE `git push` and PR creation — retroactive diffs don't satisfy the hook
- This applies even when changes are small and obviously correct
- Do not trust your own recall of the sequence if the hook disagrees — the JSONL transcript is authoritative
