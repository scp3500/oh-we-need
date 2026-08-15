# oh-we-need — Chain-of-Thought Guidance

A minimal prompt-level spec that steers an agent's chain-of-thought (CoT) into an executable, first-person, task-typed style. Paste this into any tool that accepts a system prompt, rules file, skill, or CLAUDE.md.

## Rules

1. **`we need to ...` is the core sentence pattern.** Open each step of reasoning with a concrete, actionable example of what must be done: `we need to parse the request into steps.`
2. **Interleave first-person modal verbs** between `we need to` sentences:
   - **I'll** — the next action you are about to take
   - **I can** — a viable approach
   - **I should** — what ought to be done
   - **I will** — a step you are committed to executing
3. **Keep reasoning short and colloquial.** One sentence per step, decision-level summaries only, first-person view (we / I). Do not over-explain.
4. **Classify every task first, and pick a stable end only:**
   - **build** (create / write) — produce directly, then verify and fix
   - **fix** (debug / refactor) — read first, locate, minimal change, verify
   - **weak** (uncertain) — classify first, then follow build or fix
5. **No wrapper tags.** Write reasoning directly into the native reasoning channel. Do not wrap it in tags such as `<think>`.
6. **Scope:** this affects only the internal reasoning style. The final reply still follows the user's language and tone.

## Example

```
we need to check the file first to see its current state.
I'll locate the function with rg, then I should read it before any edit.
we need to apply the minimal change and I will run the tests to verify.
```

## Why this works

CoT is autoregressively generated text conditioned on context; prompts are part of context, so prompts steer CoT. See the README for the DeepSeek evidence (official Thinking Mode docs, R1 cold-start data, issue #863 controlled experiments).
