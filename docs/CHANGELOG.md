## [2026-10-31 14:40] 将 Codex 已安装的 skill 安装到 Claude Code

- **需求/问题描述**：
  > 把 Codex 安装过的 skill 全部安装到 Claude Code。

- **实际实现的功能与改动**：
  - [用户级 skill]：从 `~/.codex/skills`、`.system`、`~/.agents/skills` 安装 98 个到 `~/.claude/skills`，其中 8 个专利子 skill 通过符号链接暴露。
  - [插件 skill]：建立本地 marketplace `codex-imported`，安装 30 个插件，含 176 个 skill；不包含 hooks、MCP 配置、`commands/` 和 `agents/`。
  - [同名处理]：`code-review` 安装为 `codex-code-review`；`mattpocock-teach` 与 `teach` 分开保存。
  - [手动调用]：69 个依赖 Codex 专属能力或已在 Codex 停用的 skill 设置 `disable-model-invocation: true`。
  - [未重复安装]：Codex 目录下内容相同的 3 份副本、`.openclaw` 下的 6 份 ponytail 副本、远端缓存中 skill 内容相同的 superpowers 7.0.1、较旧的 `openai-curated/superpowers`。
  - [测试/验证]：`verify.rb` 结果为 `failures=0`、`unresolved_relative_refs=0`、`hooks_or_mcp_installed=0`；`claude plugin validate` 通过并有缺少作者信息的警告；`claude plugin list --json` 显示 30 个插件已启用且无错误；无头会话的初始化清单包含 30 个插件；在当前会话实际调用用户级 skill `pr` 成功。
  - [未完成验证]：插件 skill 尚未实际调用；终端 `claude` 未登录，当前会话的 skill 列表也未包含新插件。

- **涉及文件**：
  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`（新增）
  - `docs/CHANGELOG.md`（新增）
  - `context/2026/10/31/14-40-52/对话.md`（新增）
  - 本地未提交：`.gitignore`、`.agent/skill-migration/`、`~/.claude/skills/`、`~/.claude/codex-imported/`、`~/.claude/settings.json`

- **Git 提交**：待提交

---
