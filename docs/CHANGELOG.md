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

- **Git 提交**：`379805c docs: record Codex skill migration to Claude Code`

---

## [2026-10-31 20:42] 安装 lemo-opuscar 插件

- **需求/问题描述**：
  > 安装 https://github.com/lemomo-ai/lemo-opuscar

- **实际实现的功能与改动**：
  - [插件]：按仓库 README 添加 marketplace `lemolab`，以用户级范围安装 `lemo-opuscar@lemolab`（版本 `f17136060781`）。插件只含一个 skill 和 `setup.sh`，没有 hooks 或 MCP 配置。
  - [风格库]：运行 `setup.sh`，把风格库下载到 `~/lemo-opuscar`（提交 `f171360`，占用 30M）。
  - [测试/验证]：`claude plugin list` 显示插件已启用；安装后的 `setup.sh` 与仓库版本内容相同；`setup.sh` 退出码为 0。
  - [未完成]：缺少 ffmpeg 7+ 和 Python 3.11+（或 uv），本机 Python 为 3.9.6；`setup.sh deps` 尚未运行；没有实际渲染影片；当前会话的 skill 列表未包含新插件。

- **涉及文件**：
  - `memory/agents.md` (+2 / -0)
  - `docs/CHANGELOG.md`
  - `context/2026/10/31/20-42-32/对话.md`（新增）
  - 本地未提交：`~/.claude/settings.json`、`~/.claude/plugins/`、`~/lemo-opuscar/`

- **Git 提交**：`1aabf4c docs: record lemo-opuscar plugin installation`

---

## [2026-10-31 20:47] 安装 lemo-opuscar 的渲染依赖

- **需求/问题描述**：
  > 安装渲染所需的依赖；用户询问本机是否已有 Python。

- **实际实现的功能与改动**：
  - [Python 核实]：本机只有系统自带的 Python 3.9.6，低于要求的 3.11+。
  - [系统工具]：通过 Homebrew 安装 ffmpeg 9.0.2 和 uv 0.13.6；安装 ffmpeg 时 Homebrew 同时安装或升级了相关依赖，其中 xz 从 5.8.3 升级到 5.8.4。
  - [风格库依赖]：运行 `setup.sh deps voice music`，安装 Node 包、Chrome Headless Shell、`.venv` 内的 Python 3.12.16 和三个层级的 Python 包，并下载 Kokoro 语音模型。`~/lemo-opuscar` 现占用 853M。
  - [测试/验证]：`setup.sh` 不再报告缺失项；Python 包全部可以导入；用 2 秒测试页面依次运行 `video.mjs`、`tts.py`、`asr_check.py`（mismatches 为 0）和 `mux.sh`，退出码均为 0；成片含 h264 和 aac 轨道，时长 2 秒，首尾帧校验值不同，解码无错误。
  - [未完成验证]：`mux.sh` 对测试成片报告响度 -17.9 LUFS，未达到 -14 LUFS 目标，测试音频只有 1.36 秒，原因尚未核实；没有渲染风格库中的风格；未下载乐器采样库和 HDRI；未按视觉验证流程查看画面。

- **涉及文件**：
  - `memory/agents.md` (+1 / -1)
  - `docs/CHANGELOG.md`
  - `context/2026/10/31/20-47-35/对话.md`（新增）
  - 本地未提交：`.agent/lemo-opuscar-smoke/`、`~/lemo-opuscar/`、Homebrew 安装内容、`~/Library/Caches/ms-playwright/`

- **Git 提交**：`cfa7ebe docs: record lemo-opuscar dependency installation`

---

## [2026-10-31 23:34] 删除 iphone-use MCP 服务器

- **需求/问题描述**：
  > 用户发送 MCP 服务器窗口截图，要求删除其中的 iphone-use。

- **实际实现的功能与改动**：
  - [移除服务器]：运行 `claude mcp remove iphone-use -s user`，从 `~/.claude.json` 的用户级配置中移除该服务器。
  - [测试/验证]：命令退出码为 0；`claude mcp get iphone-use` 报告服务器不存在；`~/.claude.json` 的 `mcpServers` 为空，全文不再包含 `iphone-use`。
  - [未完成验证]：没有重新打开桌面应用的 MCP 服务器窗口核对显示结果。

- **涉及文件**：
  - `docs/CHANGELOG.md`
  - `context/2026/10/31/23-34-56/对话.md`（新增）
  - 本地未提交：`~/.claude.json`

- **Git 提交**：`477b6cd docs: record iphone-use MCP server removal`

---

## [2026-11-02 12:38] 移除 rea MCP 服务器

- **需求/问题描述**：
  > 用户发送连接器窗口中 Rea 的截图，要求不要连接 rea。

- **实际实现的功能与改动**：
  - [移除服务器]：运行 `claude mcp remove rea -s user`，从 `~/.claude.json` 的用户级配置中移除该服务器；`/opt/homebrew/bin/rea` 程序本身保留。
  - [测试/验证]：命令退出码为 0；`claude mcp get rea` 报告服务器不存在；`~/.claude.json` 不再包含 `"rea"` 配置项。
  - [未完成验证]：当前会话的连接器状态仍显示 rea 已连接，已加载的进程在会话结束前不会断开；没有开启新会话核对显示结果。

- **涉及文件**：
  - `docs/CHANGELOG.md`
  - `context/2026/11/02/12-38-51/对话.md`（新增）
  - 本地未提交：`~/.claude.json`

- **Git 提交**：`d01f3c9 docs: record rea MCP server removal`

---
