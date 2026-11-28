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

## 选择排序演示页面 `selection-sort.html`

- 单文件 HTML：左侧柱状图、“当前最小值”水平线、逐趟记录表与控制区，右侧 C++ 代码与变量 i、j、minIdx、a[minIdx]。
- 视觉方案（按 `frontend-design` skill 设计）：整页固定为教室黑板（深板绿底，粉笔白、粉笔黄、粉笔粉、粉笔蓝），不随系统深浅色切换；粉笔黄只表示当前最小值，粉笔粉表示正在扫描的 a[j]，粉笔蓝表示已排好的前缀；标题字体为龙藏体（Long Cang），代码和数字为 JetBrains Mono（Google Fonts，离线时回退到系统字体）。
- 重点元素：一条横跨未排序区的粉笔虚线，高度等于当前最小值，扫描中遇到更小的数时下降。
- 逐趟记录表：每完成一趟追加一行数组快照，第 i 格圈出本趟选出的最小值，已排好的前缀加底色，形成阶梯。
- 算法为标准选择排序，`minIdx != i` 时才交换；C++ 源码放在 `<script type="text/plain" id="cppSource">` 中，页面与编译测试使用同一份文本。
- 元素个数 5–20，自定义数组 2–20 个正整数；其余交互与快速排序页面相同。
