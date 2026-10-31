# 注意事项

- Claude Code 只发现 `~/.claude/skills/<name>/SKILL.md` 这一层；嵌套 skill 需要在第一层建立符号链接。
- 插件内 skill 依赖插件目录结构（如 `../../CONNECTORS.md`、`${CLAUDE_PLUGIN_ROOT}`），不能直接平铺到 `~/.claude/skills`。
