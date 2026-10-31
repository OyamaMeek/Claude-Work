# 总体设计

## Codex skill 迁移到 Claude Code

- 用户级 skill：从 `~/.codex/skills`、`~/.codex/skills/.system`、`~/.agents/skills` 复制到 `~/.claude/skills`，内容相同的副本只保留一份。
- 插件内 skill：打包为本地 marketplace `codex-imported`，以保留 `../../CONNECTORS.md` 等相对引用，并用插件命名空间区分同名 skill。
- 插件只包含 skill 及其引用的文件，不包含 hooks、MCP 配置、`commands/` 和 `agents/`。
- 同名处理：Codex 的 `code-review` 安装为 `codex-code-review`，避免覆盖 Claude Code 自带的 `/code-review`；`mattpocock-teach` 改用目录名，与 `teach` 区分。
- 依赖 Codex 专属工具或连接器的 skill，以及用户在 Codex 中停用的 `hatch-pet`，设置 `disable-model-invocation: true`，只允许手动调用。
