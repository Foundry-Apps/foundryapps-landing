---
name: Source map decode is step one for Hermes crashes
description: Always generate a source-mapped bundle and decode bytecode offsets before attempting any fix for Hermes crashes
type: feedback
---

For any Hermes crash with bytecode offsets (e.g. `anonymous@1:648170`), the first step is to decode the offset to an exact source file and line. Don't guess from the stack trace or error message.

**Why:** We spent ~5 builds guessing the crash cause (duplicate React Navigation, then wrong Metro pin) when one source map decode would have identified `webidl-conversions/lib/index.js:299` in seconds.

**How to apply:**
1. Generate a local bundle with source maps: `npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output bundle.js --sourcemap-output bundle.js.map`
2. Decode the offset with a Node script using `source-map` package: `consumer.originalPositionFor({ line: 1, column: OFFSET })`
3. This gives the exact source file, line, and column
4. Only then propose a fix based on the actual crashing code
