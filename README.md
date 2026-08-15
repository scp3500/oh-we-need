# oh-we-need

一段提示词，把 DeepSeek V4 的思维链（CoT）引导成「可执行、第一人称、任务分型」的风格。核心句式：`we need to ...`。纯提示词层，零依赖。

## 需要什么

- **模型**：DeepSeek V4 系列（`deepseek-v4-pro` / `deepseek-v4-flash`）。R1 / V3.x 未验证，其他厂商模型不适用。
- **客户端**：任意支持 system prompt / rules / skill / 自定义命令的 agent 工具。

## 注入方式（按优先级）

1. **改系统提示词（首选，常驻）**：把 [prompt.md](prompt.md) 全文粘贴进 system prompt / rules / CLAUDE.md。
2. **安装 skill（按需加载）**：把同一段内容放进 skill 文件（如 `~/.pi/agent/skills/thinking-style/SKILL.md`）。
3. **DIY 命令（需要时注入）**：把同一段内容做成 `/think` 命令，会话内按需注入。

一段提示词适配所有客户端：模型理解规范含义后，会自己按客户端机制调整，无需为每个工具单独维护文件。

## 培养口癖

- 把 `we need to` / `we need` 写进系统提示词正文各处（如每条规则的行文），模型在上下文里读到就会学到这个口癖。
- `we need to` / `we need` 不一定只在首句，每一句都可以用；穿插 I'll / I can / I need / I should / I will。
- 不建议用 `let me ...` 开头，用 `we need to ...` / `we need ...` 代替。

## 为什么有效

CoT 以上下文为条件，提示词是上下文的一部分；V4 每轮 CoT 由当前上下文重新生成，引导每轮生效。依据：[官方文档](https://api-docs.deepseek.com/guides/thinking_mode) · [技术报告](https://arxiv.org/abs/2606.19348) · [社区实测](https://blog.csdn.net/weixin_34198881/article/details/92113581)。

## 友链

[dsh-routing-suite](https://github.com/yjh051108/dsh-routing-suite) —— 运行时注入 × 思维模式路由，与本项目互补。

## 许可

[MIT](LICENSE)
