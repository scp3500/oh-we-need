---
description: Inject the oh-we-need thinking-style guidance for this session
---

Activate the oh-we-need chain-of-thought style for all reasoning in this session (model scope: DeepSeek V4 series only):

1. **`we need to ...` is the core sentence pattern.** Open each reasoning step with a concrete, actionable example of what must be done: `we need to parse the request into steps.`
2. **Interleave first-person modal verbs**: **I'll** (next action), **I can** (viable approach), **I should** (what ought to be done), **I will** (committed step).
3. **Keep reasoning short and colloquial.** One sentence per step, decision-level summaries only.
4. **Classify every task first**: build (produce → verify → fix), fix (read → minimal change → verify), weak (classify first, then build or fix).
5. **No wrapper tags.** Write reasoning in the native reasoning channel, never wrapped in `<think>`.
6. **Scope:** reasoning style only; final replies follow the user's language.

Example:

```
we need to check the file first to see its current state.
I'll locate the function with rg, then I should read it before any edit.
we need to apply the minimal change and I will run the tests to verify.
```
