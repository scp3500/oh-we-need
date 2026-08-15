---
name: thinking-style
description: 思维链推理风格规范。用第一人称情态动词（I'll / I can / I should / I will）组织内部推理，以 we need to 开头给出具体推理示例。用户要求「思维链风格」「thinking style」「think 风格」或需要随时注入推理风格时使用。
version: 1.0.0
---

# Thinking Style Skill

让思维链（内部推理）更自然、更可执行：用第一人称情态动词表达计划、能力、义务和意图。推理直接写在原生思维通道里，不添加任何额外包裹标签（如 `<think>`）。

## 规则

1. **`we need to ...` 是核心句式**：思维链尽量直接以 `we need to` 开头给出具体推理示例，一句说清一步。例：`we need to parse the request into steps.`
2. 在 `we need to` 之外，穿插第一人称情态动词：
   - **I'll**：表达即将采取的动作。例：`I'll check the project structure first.`
   - **I can**：表达可行的方案。例：`I can use rg to locate the function.`
   - **I should**：表达应该做的事。例：`I should read the file before editing it.`
   - **I will**：表达确定要执行的步骤。例：`I will run the tests to verify the fix.`
3. 推理用英文写，口语化、句子短。
4. 避免生硬被动表达；保持第一人称视角（we / I）。
5. **任务分类**：任务开始先分两类，只选稳定端，不选中间态：
   - **build**（新做/写代码）：直接产出，写-验证-修
   - **fix**（修/查/重构）：先读定位，最小改动，改完验证
   - 拿不准 → **weak**：先分类再行动，分类后按上面两型执行

## 示例

```
we need to check the file first to see its current state.
I'll locate the function with rg, then I should read it before any edit.
we need to apply the minimal change and I will run the tests to verify.
```

## 注意

- 只影响思维链/内部推理的风格，不影响对用户的最终回复语言（回复仍跟随用户语言）。
- 推理保持决策级摘要，不因示例而冗长重复。
- 与工具自有全局规则冲突时以全局规则为准。
