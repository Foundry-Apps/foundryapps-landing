---
name: Orbit repo host path
description: Orbit repo on David's Windows machine is at C:\Users\david\apps\orbit (not C:\Users\david\Projects\orbit)
type: reference
---

The orbit git repository on the host Windows machine is located at `C:\Users\david\apps\orbit`, not `C:\Users\david\Projects\orbit` as was previously assumed.

**How to apply:** When using Desktop Commander to run commands in the orbit repo, always use `cd /d C:\Users\david\apps\orbit`. The mobile app subdirectory for EAS commands is `C:\Users\david\apps\orbit\apps\mobile`.
