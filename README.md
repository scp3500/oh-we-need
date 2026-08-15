# oh-we-need

> **DeepSeek V4 系列特化的思维链引导规范** —— 任何 agent 工具皆可接入，不绑定任何客户端。
> 核心句式只有一句：`we need to ...`

**oh-we-need** 是一套针对 DeepSeek V4 系列的最小化思维链（CoT）引导规范：用一段提示词，把模型的内部推理引导成「可执行、第一人称、任务分型」的风格。纯提示词层——无插件、无 hook、无运行时注入，只要能接入 DeepSeek V4 的 agent 工具，直接粘贴即可生效。

## 模型支持范围

**目前只对 DeepSeek V4 系列生效。**

| 模型 | 状态 |
|---|---|
| `deepseek-v4-pro` | ✅ 已验证生效 |
| `deepseek-v4-flash` | ✅ 已验证生效 |
| DeepSeek R1 / V3.x | ⚠️ 未验证，不保证 |
| 其他厂商模型 | ❌ 不适用，未验证 |

引导依赖 V4 系列思维链的特性；其他模型（含旧版 DeepSeek）的效果不在本项目承诺范围内。

## 定位

| 维度 | oh-we-need | 运行时注入类方案（如 dsh-routing-suite） |
|---|---|---|
| 模型 | **DeepSeek V4 系列特化** | 特定运行时 |
| 客户端 | 任意 agent 工具 | 深度绑定特定工具（如 DSH） |
| 层 | 纯提示词层 | 运行时层 |
| 依赖 | 零依赖，一段文本 | 插件 / 注入器 / 重启 |
| 作用 | 引导思维链的风格与结构 | 注入工具链、路由预设 |

模型特化、客户端无关、纯提示词层——这就是本项目的全部优势。

## 为什么 DeepSeek V4 的思维链可以被提示词引导

本项目的前提是一句话：**思维链具有可塑性，提示词可以引导它。** 以 DeepSeek V4 为例，证据有三层：

1. **生成机制（官方文档）**：V4 在输出最终答案前先生成 `reasoning_content`（CoT），每一轮、每一个 token 都以当前上下文为条件。提示词是上下文的一部分，因此提示词直接参与 CoT 的分布。
   —— [官方文档 Thinking Mode](https://api-docs.deepseek.com/guides/thinking_mode)（覆盖 `deepseek-v4-pro` / `deepseek-v4-flash`）：CoT 与最终答案分离返回；无工具调用时，上一轮 CoT **不**拼入下一轮上下文，每轮 CoT 都由当前上下文重新生成——引导每轮生效。

2. **模型侧（技术报告）**：DeepSeek-V4 系列经过大规模预训练（32T tokens）与 comprehensive post-training 管线，推理能力本身由训练塑造——思维链不是外部挂件，而是模型内在能力，因此可以从外部被引导。
   —— [DeepSeek-V4 技术报告](https://arxiv.org/abs/2606.19348)（预览版：V4-Pro 1.6T/49B，V4-Flash 284B/13B，均支持百万 token 上下文）

3. **实测（社区）**：V4-Pro 上线后，社区实测（37 个推理任务，含 API 思维链调用与推理预算控制）表明思维链已从“提示工程技巧”变成可编程、可控的基础设施能力；第三方文档也演示了用 `thinking.type` 与 `reasoning_effort` 控制每轮思考。
   —— [DeepSeek-V4-Pro 思维链调用实测](https://blog.csdn.net/weixin_34198881/article/details/92113581)、[第三方 thinking 参数文档](https://docs.infini-ai.com/docs/guide/llm/deepseek.html)

结论：CoT 不是固定不可改的，风格、语言、结构都能被提示词引导。oh-we-need 就是把这种引导固化成一段可复用的规范——**特化到 DeepSeek V4 系列上**。

## 方法论

### 核心句式

1. **`we need to ...` 是核心句式**：思维链尽量以 `we need to` 开头给出具体推理示例，一句说清一步。
   `we need to parse the request into steps.`
2. **穿插第一人称情态动词**：
   - **I'll** —— 即将采取的动作
   - **I can** —— 可行的方案
   - **I should** —— 应该做的事
   - **I will** —— 确定要执行的步骤
3. **短句、口语化**，保持第一人称视角（we / I），只保留决策级摘要。
4. **任务分型**：任务开始先分两类，只选稳定端，不选中间态：
   - **build**（新做/写）→ 直接产出，写-验证-修
   - **fix**（修/查/重构）→ 先读定位，最小改动，改完验证
   - 拿不准 → **weak**：先分类，再按上面两型执行
5. **不包裹标签**：推理直接写进模型的**原生推理通道**，不加 `<think>` 之类的包裹标签。
6. **只影响推理风格，不影响最终回复**：最终回复仍跟随用户语言与风格。

### 示例

```
we need to check the file first to see its current state.
I'll locate the function with rg, then I should read it before any edit.
we need to apply the minimal change and I will run the tests to verify.
```

完整核心提示词见 [`core/prompt.md`](core/prompt.md)（英文，可直接粘贴），中文说明见 [`core/prompt.zh-CN.md`](core/prompt.zh-CN.md)。

## 适配器

同一段核心提示词，适配到各 agent 客户端的原生机制（**客户端只是容器，模型必须是 DeepSeek V4**）：

| 客户端 | 文件 | 用法 |
|---|---|---|
| Pi（pi-coding-agent） | [`adapters/pi/SKILL.md`](adapters/pi/SKILL.md) | 放进 `~/.pi/agent/skills/thinking-style/` |
| Claude Code | [`adapters/claude-code/CLAUDE.md`](adapters/claude-code/CLAUDE.md) | 追加进项目或全局 CLAUDE.md |
| Claude Code slash 命令 | [`adapters/claude-code/commands/think.md`](adapters/claude-code/commands/think.md) | 放进 `.claude/commands/`，用 `/think` 触发 |
| Cursor | [`adapters/cursor/.cursorrules`](adapters/cursor/.cursorrules) | 放进项目根目录 |
| OpenAI Codex | [`adapters/codex/AGENTS.md`](adapters/codex/AGENTS.md) | 放进项目根目录或 `~/.codex/` |
| 通用（任意 API / 客户端） | [`adapters/generic/system-prompt.md`](adapters/generic/system-prompt.md) | 直接作为 system prompt 粘贴 |

适配器只是**同一规范的不同容器**：客户端支持哪种机制，就用哪种容器；容器本身不影响规范内容。新增一个客户端只需新增一个适配文件——这就是「任何 agent 工具皆可接入」的含义（前提：接的是 DeepSeek V4）。

## 快速开始

1. 确认所用模型是 DeepSeek V4 系列（`deepseek-v4-pro` / `deepseek-v4-flash`）。
2. 打开 [`core/prompt.md`](core/prompt.md)，复制全文。
3. 粘贴到你所用 agent 客户端的 system prompt / rules / skill / CLAUDE.md 中（或直接用上面的适配器文件）。
4. 开始对话，观察思维链是否以 `we need to ...` 起步、穿插 I'll / I can / I should / I will。

## 友链 Friends

- **[dsh-routing-suite](https://github.com/yjh051108/dsh-routing-suite)** —— 注入器 × 思维模式路由套装。正是它引发了本项目最初的思考。它为 DSH 提供运行时注入器与 P1-P23 实测的路由预设，在运行时层做深度优化。oh-we-need 与它互补：想要运行时管理、路由预设与深度绑定，用 dsh-routing-suite；想要零依赖、客户端无关、纯提示词层的 DeepSeek V4 思维链引导，用 oh-we-need。

## 许可

[MIT](LICENSE)
