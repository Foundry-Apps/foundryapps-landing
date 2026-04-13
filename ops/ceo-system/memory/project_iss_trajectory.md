---
name: ISS Trajectory Line Follow-Up
description: After push notifications, user wants to add a trajectory line to the ISS map
type: project
---

The ISS map component at src/components/iss/ISSMap.tsx needs a trajectory/orbit path line added as a follow-up to the push notifications task.

**Why:** User mentioned this as the next task after push notifications are done.

**How to apply:** When the user asks about the ISS map or trajectory line, check the current ISSMap.tsx and ISSPositionPanel.tsx to understand the current implementation before proposing changes. The ISS API is at api.wheretheiss.at and already polled via useISS hook.
