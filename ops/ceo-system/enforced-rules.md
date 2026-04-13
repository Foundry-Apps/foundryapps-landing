# Enforced Operating Rules

These rules apply to all Foundry Apps engineering and operations work. Tier 1 rules are enforced deterministically by Claude Code hooks. Tier 2 rules are enforced by prompt review at session end.

---

## Tier 1 — Enforced by Hooks

### Rule 1: Research before implementing
Web search for best practice, SDK docs, or API reference BEFORE writing any code or config change. The Stop hook checks that a web search occurred before any implementation in the session. Violations block session completion.

**Scope:** Any fix, feature, config change, or API integration. Applies even to small one-line fixes.

**Reading files counts as starting implementation scope.** The web search must happen before reading any files related to the task.

**Hook location:** `orbit/.claude/settings.json` → Stop hook, prompt 1.

---

### Rule 2: Self-review before PR
Run `git diff master...HEAD` (or read all changed files) BEFORE `git push` and PR creation. The Stop hook checks that a diff review appeared in the transcript before the push.

**Required sequence:** edit → commit → `git diff master...HEAD` → push → PR.

Do not interleave other steps between commit and diff. Reading individual files does NOT satisfy this requirement — an explicit `git diff` command must appear.

**Hook location:** `orbit/.claude/settings.json` → Stop hook, prompt 2.

---

### Rule 3: Pre-build gate
Before running EAS builds or triggering Vercel deployments, the pre-build gate hook checks that local validation has been completed (local Metro export, expo-doctor, etc.).

**Hook location:** `orbit/.claude/settings.json` → PreToolUse (Bash matcher).

---

### Rule 4: Protected files
Certain files are write-protected and cannot be modified without explicit override. This prevents accidental mutation of critical config.

**Hook location:** `orbit/.claude/settings.json` → PreToolUse (Edit/Write/MultiEdit matcher).

---

## Tier 2 — Process Rules (reviewed at session end)

### Rule 5: Observe before hypothesising
Collect data (logs, crash traces, git diff, API responses) before proposing a fix. Do not guess at root cause from symptoms alone.

**For mobile crashes:** Get adb logcat output → decode bytecode offset → then propose fix.

---

### Rule 6: Verify the artifact
After a fix is deployed, confirm it is in the live artifact (binary, deployment) before reporting completion or asking the user to test. For EAS builds: pull APK and grep bundle for crash signature. For web: `curl production-url | grep expected-content`.

---

### Rule 7: Local validation before builds
Full pre-flight before every EAS or production build:
1. `pnpm install` / `yarn install` from repo root
2. `npx expo export --platform android` — catches JS bundle errors
3. Compare bundle size to previous build — identical = fix didn't land
4. Grep bundle for known crash signatures
5. `npx expo-doctor`
6. Then: `eas build --clear-cache`

---

### Rule 8: One build at a time
Check for in-progress EAS builds before submitting a new one. Never submit a build after each fix — accumulate fixes, submit one build.

---

### Rule 9: Never escalate ops to David
Automate operational decisions. Only escalate per the criteria in `CEO-PLAYBOOK.md` (downtime > 5 min, same fix fails twice, financial anomaly, security incident, compliance deadline, legal correspondence, cross-product architectural decision).

---

## Hook Configuration

The hooks that enforce Tier 1 rules live in `orbit/.claude/settings.json`. They must be present for the rules to be enforced. On a new machine, pull the orbit repo — the hooks are checked in and load automatically when Claude Code opens the project.

```json
"Stop": [
  {
    "hooks": [
      {
        "type": "prompt",
        "prompt": "Check if this session involved implementing a fix, feature, or config change. If it did, verify that a web search was performed BEFORE the implementation began (not after)...",
        "timeout": 30
      },
      {
        "type": "prompt", 
        "prompt": "Check if a PR was created in this session. If it was, verify that a git diff or explicit review of changed files was performed BEFORE the PR was created...",
        "timeout": 30
      }
    ]
  }
]
```

Full hook JSON: `orbit/.claude/settings.json`.
