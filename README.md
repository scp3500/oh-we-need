# oh-we-need

一段提示词，把 DeepSeek V4 的思维链（CoT）引导成「可执行、第一人称、任务分型」的风格。核心句式：`we need to ...`。纯提示词层，零依赖。

## 需要什么

- **模型**：DeepSeek V4 系列（`deepseek-v4-pro` / `deepseek-v4-flash`）。R1 / V3.x 未验证，其他厂商模型不适用。
- **客户端**：任意支持 system prompt / rules / skill / 自定义命令的 agent 工具。

## 注入方式（按优先级）

1. **改系统提示词（首选，常驻）**：把 [`core/prompt.md`](core/prompt.md) 全文粘贴进 system prompt / rules / CLAUDE.md。
2. **安装 skill（按需加载）**：把 `adapters/pi/SKILL.md` 放进 `~/.pi/agent/skills/thinking-style/`。
3. **DIY 命令（需要时注入）**：把 `adapters/claude-code/commands/think.md` 放进 `.claude/commands/`。会话内用 `/think` 注入；`/think build`、`/think fix` 指定任务模式。

## 其他适配器

| 文件 | 客户端 |
|---|---|
| `adapters/cursor/.cursorrules` | Cursor，放项目根目录 |
| `adapters/codex/AGENTS.md` | OpenAI Codex，放项目根目录或 `~/.codex/` |
| `adapters/generic/system-prompt.md` | 任意 API / 客户端，直接作 system prompt |

适配器是同一规范的容器，内容一致，客户端支持哪种机制就用哪种。

## 为什么有效

CoT 以上下文为条件，提示词是上下文的一部分；V4 每轮 CoT 由当前上下文重新生成，引导每轮生效。依据：[官方文档](https://api-docs.deepseek.com/guides/thinking_mode) · [技术报告](https://arxiv.org/abs/2606.19348) · [社区实测](https://blog.csdn.net/weixin_34198881/article/details/92113581)。

## 友链

[dsh-routing-suite](https://github.com/yjh051108/dsh-routing-suite) —— 运行时注入 × 思维模式路由，与本项目互补。

## 许可

[MIT](LICENSE)
