# 代理与工具

- 当前代理：Claude Code（桌面应用 Code 标签页），命令行版本 2.1.268。
- 终端内的 `claude` 命令行尚未登录，无法发起模型请求；`claude plugin` 等本地管理命令可用。
- Skill 位置：
  - `~/.claude/skills/`：从 Codex 复制的用户级 skill（98 个，另有已存在的 `ego-browser`）。
  - `~/.claude/codex-imported/`：本地 marketplace `codex-imported` 的来源目录，含 30 个插件。
  - `~/.claude/plugins/cache/codex-imported/`：Claude Code 安装后的插件副本。
  - `~/.claude/plugins/cache/lemolab/`：插件 `lemo-opuscar@lemolab`，来源为 GitHub 仓库 `lemomo-ai/lemo-opuscar`。
  - `~/lemo-opuscar/`：lemo-opuscar 的风格库，依赖已安装（ffmpeg 9.0.2、uv 0.13.6、`.venv` 内的 Python 3.12.16、voice 和 music 层）；系统 Python 仍为 3.9.6；乐器采样库和 HDRI 按需用 `tools/fetch.sh` 下载。
- 迁移脚本与验证输出：`.agent/skill-migration/`（本地文件，不提交）。
