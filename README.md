# oh-we-need

面向 DeepSeek V4 Agent 的思维链风格引导提示词。目标是让内部推理更接近「可执行、第一人称、任务分型」的风格，核心句式为 `we need to ...`。纯提示词层，零依赖。

**效果边界：** 这个提示词只能大幅提高目标思维风格出现的概率，并不能保证一定生效。若某次没有按目标风格输出，可在当前会话临时注入 [prompt.md](prompt.md)，再继续任务。

## 规范源

[prompt.md](prompt.md) 是唯一的规范源。Agent 需要获取完整规则时，应直接读取并注入该文件；README 只说明适用范围和接入方式。

## 适用范围

- **模型**：已验证 DeepSeek V4 系列（`deepseek-v4-pro`、`deepseek-v4-flash`）。R1 / V3.x 未验证，其他厂商模型不保证适用。
- **客户端**：任意支持 system prompt、rules、skill 或自定义命令的 Agent 工具。

## 接入

1. **常驻注入（首选）**：将 `prompt.md` 全文放入 system prompt、rules 或 `CLAUDE.md`。
2. **临时注入（补救）**：当当前会话没有保持目标风格时，将 `prompt.md` 全文作为本轮指令注入，再继续任务。
3. **按需加载**：将同一内容放入 skill 文件，或封装为 `/think` 等自定义命令。

**首句位置：** `prompt.md` 的 `First sentence rule` 应位于系统提示词最开头。上下文首部的指令权重最高，这会提高首句规则的遵循概率。

## 目标行为

完整规则以 [prompt.md](prompt.md) 为准。接入后，Agent 的内部推理应具备以下特征：

- `<think>` 内第一句话必须以 `we need to ...` / `we need ...` 开头。
- 后续推理以 `we need to ...` / `we need ...` 为核心模式，一步一句，保持简短、口语化。
- 先区分 build / fix / weak 等任务类型，再执行对应流程。
- 不在最终回复泄漏 `<think>` 标签或内部推理。

## 作用机制

CoT 由当前上下文生成，提示词是该上下文的一部分；V4 在每轮生成时重新接收这些引导。参考：[官方 Thinking Mode 文档](https://api-docs.deepseek.com/guides/thinking_mode) · [DeepSeek-V4 技术报告](https://arxiv.org/abs/2606.19348)。

## 友链

[dsh-routing-suite](https://github.com/yjh051108/dsh-routing-suite) 提供运行时注入与思维模式路由，可与本项目搭配使用。

## 许可

[MIT](LICENSE)
