# 调试器入门

调试器是定位程序错误的利器。掌握它，能让你快速找到崩溃位置、观察变量、理解调用栈，并用断点与单步执行重现问题。

## 调试器类型与平台

- Linux/Windows 推荐 `gdb`
- macOS 默认使用 `lldb`（命令与交互略有差异）
- IDE（CLion / VSCode / Visual Studio）内置图形化调试，底层调用 gdb/lldb

---

## ① 关键概念

- 断点（Breakpoint）：在某一行暂停程序执行
- 单步执行（Step Into / Step Over）：逐行运行，进入或越过函数
- 变量查看（print / info locals）：检查当前作用域的变量值
- 调用栈（backtrace / bt）：查看当前函数调用路径
- 栈帧（frame）：切换并检查不同调用层级的上下文

---

## ② 示例程序：制造一次崩溃

创建 `crash.cpp`：

```cpp
#include <iostream>

void crash_here() {
    int* p = nullptr;
    *p = 42;
}

int compute(int x) {
    return x * 2;
}

int main() {
    int a = 21;
    int b = compute(a);
    std::cout << "b = " << b << std::endl;
    crash_here();
    std::cout << "This will not be printed." << std::endl;
    return 0;
}
```

编译：

```bash
g++ -g crash.cpp -o crash_demo
```

> `-g` 选项用于生成调试符号，便于调试器定位源码行号。

---

## ③ 使用 gdb 调试（Linux/WSL/Windows MinGW）

启动与设置断点：

```bash
gdb ./crash_demo
(gdb) break main
(gdb) run
```

单步与变量查看：

```bash
(gdb) next
(gdb) step
(gdb) print a
(gdb) print b
(gdb) info locals
(gdb) backtrace
```

继续运行至崩溃点：

```bash
(gdb) continue
```

此时程序发生段错误（Segmentation Fault），使用：

```bash
(gdb) bt
(gdb) frame 0
(gdb) list
```

你将看到崩溃位于 `crash_here()` 的空指针解引用处。

---

## ④ 使用 lldb 调试（macOS）

```bash
lldb ./crash_demo
(lldb) breakpoint set --name main
(lldb) run
(lldb) next
(lldb) step
(lldb) frame variable
(lldb) bt
(lldb) continue
```

当崩溃发生时，同样使用 `bt` 和 `frame` 检查调用栈与当前栈帧。

---

## ⑤ 调用栈与栈帧分析

- `backtrace/bt`：从 `main` 到当前函数的完整调用路径
- `frame N`：切换到第 `N` 层栈帧，检查该层变量与源码位置
- `info args` / `frame variable`：查看当前函数的形参与局部变量

---

## ⑥ Core Dump（崩溃后离线分析）

在 Linux 上启用核心转储：

```bash
ulimit -c unlimited
./crash_demo
```

若生成 `core` 文件，可离线分析：

```bash
gdb ./crash_demo core
(gdb) bt
```

在 macOS 上通常使用 `lldb` 直接附加或分析崩溃报告：

```bash
lldb ./crash_demo
(lldb) run
(lldb) bt
```

---

## ⑦ IDE 内置调试（推荐）

- 在编辑器中点击代码左侧行号处添加断点
- 选择“调试运行”，使用工具栏进行单步、继续与变量查看
- 变量、监视（Watch）、调用栈面板能直观展示程序状态

---

## ⑧ 实战练习 🎯

- 编译并运行 `crash_demo`，分别使用 gdb/lldb 复现崩溃
- 设置断点在 `crash_here()`，单步进入并观察 `p` 的值
- 使用 `bt` 与 `frame` 定位崩溃发生的确切行号
- 修改代码将 `p` 指向有效地址，验证问题修复

---
