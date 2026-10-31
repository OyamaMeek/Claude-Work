# 完成标准与检查

## Skill 迁移

- `ruby .agent/skill-migration/verify.rb`：`failures=0`、`unresolved_relative_refs=0`、`hooks_or_mcp_installed=0`。
- `claude plugin validate ~/.claude/codex-imported`：通过。
- `claude plugin list --json`：`codex-imported` 的 30 个插件均已启用且无错误。
- 新会话中调用插件 skill，确认内容能够加载。
