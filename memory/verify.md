# 完成标准与检查

## Skill 迁移

- `ruby .agent/skill-migration/verify.rb`：`failures=0`、`unresolved_relative_refs=0`、`hooks_or_mcp_installed=0`。
- `claude plugin validate ~/.claude/codex-imported`：通过。
- `claude plugin list --json`：`codex-imported` 的 30 个插件均已启用且无错误。
- 新会话中调用插件 skill，确认内容能够加载。

## 快速排序演示页面

- `python3 .agent/quick-sort/extract_cpp.py` 从页面提取 C++ 源码，`clang++ -std=c++17 -Wall -Wextra -Werror` 编译测试程序，随机数组结果与 `std::sort` 一致。
- 浏览器打开页面，控制台无错误；`buildSteps` 对大量随机数组（含重复值、已排序、逆序）的最终顺序有序，每次 pivot 归位时左侧都小于 pivot、右侧都不小于 pivot。
- 按钮、滑块、自定义输入（含非法输入的报错）按预期工作。

## 选择排序演示页面

- `python3 .agent/selection-sort/extract_cpp.py` 提取页面中的 C++ 源码，`clang++ -std=c++17 -Wall -Wextra -Werror -fsanitize=address,undefined` 编译测试程序，随机、已排序、逆序、多重复值数组与 `std::sort` 一致。
- 浏览器中 `buildSteps` 对大量数组：最终有序；比较次数等于 n(n-1)/2；每趟结束时 a[i] 为 a[i..n-1] 的最小值；记录表行数等于趟数；交换次数等于 `minIdx != i` 的趟数。
- 按钮、滑块、快捷键、自定义输入（含非法输入的报错）按预期工作，控制台无错误；375px 宽度下无横向页面滚动。
