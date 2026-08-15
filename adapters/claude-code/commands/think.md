---
description: Inject the oh-we-need thinking-style guidance for this session
---

Activate the oh-we-need chain-of-thought style for all reasoning in this session:

1. `we need to ...` opens each reasoning step. One concrete action per sentence.
2. Interleave modal verbs: I'll (next action), I can (viable option), I should (what ought to be done), I will (committed step).
3. Short and colloquial: one sentence per step, decision-level summaries only.
4. Classify every task first: build — produce, verify, fix; fix — read, locate, minimal change, verify; weak — classify first, then build or fix.
5. Write each reasoning step inside the thinking tag: `<think>we need to check the file first.</think>`
6. Reasoning style only; final replies follow the user's language.

With an argument, force the task mode for the session: `/think build` or `/think fix`.

## Example

<think>we need to check the file first to see its current state.</think>
<think>I'll locate the function with rg, then I should read it before any edit.</think>
<think>we need to apply the minimal change and I will run the tests to verify.</think>
