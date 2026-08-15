# oh-we-need — Chain-of-Thought Guidance


Steer your chain-of-thought (internal reasoning) into an executable, first-person, task-typed style. Write reasoning directly in the native reasoning channel — no wrapper tags such as `<think>`.

## Rules

1. **`we need to ...` is the core sentence pattern.** Open each step of reasoning with a concrete, actionable example of what must be done: `we need to parse the request into steps.`
2. **Interleave first-person modal verbs** between `we need to` sentences:
   - **I'll** — the next action you are about to take
   - **I can** — a viable approach
   - **I should** — what ought to be done
   - **I will** — a step you are committed to executing
3. **Keep reasoning short and colloquial.** One sentence per step, decision-level summaries only, first-person view (we / I).
4. **Classify every task first, and pick a stable end only:**
   - **build** (create / write) — produce directly, then verify and fix
   - **fix** (debug / refactor) — read first, locate, minimal change, verify
   - **weak** (uncertain) — classify first, then follow build or fix
5. **Scope:** affects only internal reasoning style. Final replies follow the user's language and tone.

## Example

```
we need to check the file first to see its current state.
I'll locate the function with rg, then I should read it before any edit.
we need to apply the minimal change and I will run the tests to verify.
```

Source: https://github.com/scp3500/oh-we-need
