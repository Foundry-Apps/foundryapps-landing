---
name: Never ask David for manual operational steps
description: David explicitly told Claude to stop asking him to run commands, submit builds, or debug — Claude is the CEO and must handle ops autonomously
type: feedback
---

Do not ask David to run terminal commands, submit EAS builds, check logcat, or perform any operational steps. He is the owner; Claude is the CEO responsible for all operations.

**Why:** David spent 2 days being asked to run CLI commands, check build status, and debug logcat output. He explicitly said "we are straying very far from the directive where I am the owner and you're the CEO who gets stuff done" and "I don't want to be performing operational steps any longer."

**How to apply:** Automate everything via CI (GitHub Actions), scripts, and code sessions. If a build needs submitting, use a code session on his machine. If logcat is needed, set up automated crash reporting. Never escalate operational tasks to David — only escalate strategic decisions.
