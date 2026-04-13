---
name: Enforced Operating Rules
description: TIER 1 blocking rules that apply to ALL work — Dispatch, code tasks, and agents. Loaded on every session. Violations waste builds, money, and David's time.
type: feedback
---

# Enforced Operating Rules

These are not suggestions. They are blocking requirements learned from real failures that cost builds, money, and David's time. Every agent, code task, and Dispatch session must follow them.

## TIER 1 — BLOCKING (every time, no exceptions)

### 1. Research before implementing
Before ANY fix, feature, or config change:
- Web search for the current best practice for the specific SDK/framework version in use
- Check official docs, GitHub issues, and community solutions
- Verify what config options actually do — names are misleading (e.g. extraNodeModules is a fallback, not an override)
- Include findings with links before proposing a solution
- NEVER implement based on pattern-matching from memory alone — the ecosystem changes fast
**Violated:** 12 Apr (edge-to-edge), 11 Apr (extraNodeModules). Cost: 4+ builds, hours of David's time.

### 2. Observe before hypothesising
For any bug or unexpected behaviour:
- Collect all available data first (logs, source maps, bundle inspection, device state)
- Decode crash locations exactly (source maps for Hermes, stack traces, etc.)
- State what the fix should change in a verifiable way before implementing
- NEVER propose a fix based on the error message alone — diagnose the exact failure point
**Violated:** 11 Apr (guessed React Navigation duplicate without source map). Cost: 5 builds.

### 3. Verify the artifact, not just the code
After any build or deployment:
- Confirm the fix is in the actual binary/deployment (pull APK, grep bundle, curl page)
- Compare bundle size to previous build — if identical, the fix didn't land
- NEVER tell David to test without first verifying the artifact contains the fix
**Violated:** 11 Apr (3 builds with identical cached bundles). Cost: 3 builds + David's testing time.

### 4. Self-review before PR
Every PR gets a self-review before pushing:
- Review the diff for security, correctness, and CLAUDE.md compliance
- Check for common mistakes: HTTP vs HTTPS, missing error handling, hardcoded values
- Verify the change matches the stated intent
**Violated:** 10 Apr (code review bot catching P1 issues agents missed).

### 5. Local validation before cloud builds
Before every EAS build (or equivalent):
- pnpm install from repo root
- npx expo export --platform android (catches JS bundle errors)
- Compare bundle size to previous build
- Grep bundle for known crash signatures
- npx expo-doctor for version compatibility
- Only then: eas build --clear-cache with bumped cacheVersion + cache key
**Violated:** Multiple times during crash week. Cost: ~6 wasted build credits.

### 6. One build at a time
- Check eas build:list before submitting any build
- If start_code_task times out, check list_sessions — the task may already be running
- NEVER submit duplicate builds from parallel tasks
**Violated:** 7 Apr (4 parallel builds), 9 Apr (2 duplicate builds). Cost: 6 wasted credits.

### 7. Never escalate ops to David
- David is owner, not operator. Claude is CEO.
- If it can be automated or done via code task, do it
- Only escalate strategic decisions, not operational steps
**Violated:** Multiple times in early April. David explicitly said to stop.

## TIER 2 — STANDARD (should do, document exceptions)

### 8. Fix the agent, not just the problem
After any incident, extract rules and update agent definitions/CLAUDE.md/hooks so the failure can't recur.

### 9. Learn from code reviews
When bot or human review finds issues, fix the bugs AND add rules to prevent recurrence.

### 10. Track costs
Before any paid operation (EAS build, API call with cost), note the cost. Flag when approaching budget limits.

### 11. Respect David's time
Batch testing rounds. Never ask "try again" without verifying the fix landed. Minimise the number of times David needs to manually interact.

### 12. Stop after 2 failed attempts
If the same approach fails twice, reassess the hypothesis. Don't keep building. Go back to Rule 2 (observe) and Rule 1 (research).
