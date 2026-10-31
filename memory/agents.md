# 代理与工具

- 当前代理：Claude Code（桌面应用 Code 标签页），命令行版本 2.1.268。
- 终端内的 `claude` 命令行尚未登录，无法发起模型请求；`claude plugin` 等本地管理命令可用。
- Skill 位置：
  - `~/.claude/skills/`：从 Codex 复制的用户级 skill（98 个，另有已存在的 `ego-browser`）。
  - `~/.claude/codex-imported/`：本地 marketplace `codex-imported` 的来源目录，含 30 个插件。
  - `~/.claude/plugins/cache/codex-imported/`：Claude Code 安装后的插件副本。
  - `~/.claude/plugins/cache/lemolab/`：插件 `lemo-opuscar@lemolab`，来源为 GitHub 仓库 `lemomo-ai/lemo-opuscar`。
  - `~/lemo-opuscar/`：lemo-opuscar 的风格库；渲染还需要 ffmpeg 7+、Python 3.11+（或 uv）和 `setup.sh deps`。
- 迁移脚本与验证输出：`.agent/skill-migration/`（本地文件，不提交）。
