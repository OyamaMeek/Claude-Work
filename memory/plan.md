# 总体设计

## Codex skill 迁移到 Claude Code

- 用户级 skill：从 `~/.codex/skills`、`~/.codex/skills/.system`、`~/.agents/skills` 复制到 `~/.claude/skills`，内容相同的副本只保留一份。
- 插件内 skill：打包为本地 marketplace `codex-imported`，以保留 `../../CONNECTORS.md` 等相对引用，并用插件命名空间区分同名 skill。
- 插件只包含 skill 及其引用的文件，不包含 hooks、MCP 配置、`commands/` 和 `agents/`。
- 同名处理：Codex 的 `code-review` 安装为 `codex-code-review`，避免覆盖 Claude Code 自带的 `/code-review`；`mattpocock-teach` 改用目录名，与 `teach` 区分。
- 依赖 Codex 专属工具或连接器的 skill，以及用户在 Codex 中停用的 `hatch-pet`，设置 `disable-model-invocation: true`，只允许手动调用。

## 快速排序演示页面 `quick-sort.html`

- 单文件 HTML：左侧柱状图、递归区间条带与控制区，右侧 C++ 代码与变量。
- 视觉方案（按 `frontend-design` skill 设计）：浅色为工程方格纸、深色为蓝图纸；墨水蓝为主色，红色只用于 pivot 和交换，荧光黄表示比较，已归位元素用墨水填实；标题字体为站酷小薇，代码和数字为 IBM Plex Mono（Google Fonts，离线时回退到系统字体）。
- 调用栈以柱子下方按深度排列的区间条带呈现，条带区高度按该数组的最大递归深度固定。
- 算法采用 Lomuto 分区（`a[high]` 为 pivot）；C++ 源码放在 `<script type="text/plain" id="cppSource">` 中，页面与编译测试使用同一份文本。
- 预先生成全部步骤，支持播放、暂停、单步前进与后退、重置、随机数组、元素个数、速度、自定义数组。
- 页面文件与测试文件只保留在本地，不提交。
