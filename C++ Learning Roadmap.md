# 🚀 C++ 学习路线图

## 第一部分：C++ 语言核心 (Core C++)

### 0. 准备阶段 (Preparation)

- [ ] **历史简介**
    - [ ] 发展历史：C with Classes -> C++98 -> C++11 (现代分水岭) -> C++20/23。
    - [ ] 语言特点：零开销抽象、RAII、高性能、多范式。
    - [ ] 应用领域：游戏引擎 (Unreal)、嵌入式、高频交易、AI 基础设施。
    - [ ] **🎯 练习**：查阅资料，列出 3 个你常用的软件中哪些是用 C++ 开发的。
- [ ] **环境搭建**
    - [ ] 编译器：GCC (Linux), MSVC (Windows), Clang (MacOS/LLVM)。
    - [ ] 构建工具：**CMake** (行业标准，必须掌握编写 CMakeLists.txt)。
    - [ ] 开发工具：Visual Studio (IDE), VS Code (轻量级), CLion (JetBrains)。
    - [ ] 包管理器：Vcpkg 或 Conan (现代 C++ 依赖管理)。
    - [ ] **🎯 练习**：并在本地安装 GCC 和 CMake，编写一个 `CMakeLists.txt` 来编译 "Hello World"。
- [ ] **调试器入门**
    - [ ] 调试器使用：GDB (命令行) 或 IDE 内置调试器。
    - [ ] 核心技能：设置断点 (Breakpoint)、单步执行 (Step Over/Into)、查看变量。
    - [ ] 堆栈跟踪：理解 Call Stack，分析 Crash 时的核心转储 (Core Dump)。
    - [ ] **🎯 练习**：编写一个故意会 Crash 的程序（如访问空指针），使用调试器定位崩溃行号。

### 第一阶段：基础语法 (Basic Syntax)

- [ ] **基础语法**
    - [ ] 数据类型：整数 (int, long long)、浮点 (double)、布尔 (bool)、字符 (char)。
    - [ ] 变量常量：变量初始化 (C++11 `{}` 列表初始化)、`const`、`constexpr` (编译期常量)。
    - [ ] 运算符：算术、逻辑、位运算、`sizeof`。
    - [ ] 流程控制：`if` (带初始化 C++17)、`switch` (fallthrough 特性)、`for` (范围 for 循环)、`while`。
    - [ ] **🎯 练习**：编写一个“猜数字游戏”，使用 `while` 循环和 `if` 判断，并用 `const` 定义最大尝试次数。
- [ ] **函数与作用域**
    - [ ] 函数定义与调用：分离声明 (.h) 与实现 (.cpp)。
    - [ ] **参数传递 (核心)**：值传递 vs **引用传递 (`&`)** vs 指针传递。
    - [ ] 命名空间：`namespace` 的定义、`using` 声明、避免在头文件使用 `using namespace std`。
    - [ ] 函数重载：同名不同参的实现原理 (Name Mangling)。
    - [ ] **🎯 练习**：编写一个 `swap` 函数，使用“引用传递”交换两个整数的值；再重载它以支持浮点数。
- [ ] **数组与字符串**
    - [ ] 数组：C 风格数组的局限性 vs `std::array` (C++11 固定大小数组)。
    - [ ] 字符串：`std::string` 的增删改查、拼接、子串查找。
    - [ ] 字符串视图：`std::string_view` (C++17 无拷贝字符串切片)。
    - [ ] **🎯 练习**：输入一行英文句子，使用 `std::string` 统计其中单词的个数，并反转整个句子输出。

### 第二阶段：面向对象 (OOP)

- [ ] **类与对象**
    - [ ] 构造与析构：默认构造、初始化列表 (效率更高)、析构函数 (资源释放)。
    - [ ] **三/五法则**：拷贝构造、拷贝赋值、移动构造、移动赋值。
    - [ ] 静态成员 (`static`)：类共享数据，非特定对象所有。
    - [ ] **🎯 练习**：设计一个 `Student` 类，包含姓名和成绩，使用初始化列表构造，并统计当前内存中有多少个 `Student` 对象（使用 static）。
- [ ] **封装与访问控制**
    - [ ] 访问权限：`public` (接口), `private` (数据), `protected` (子类可见)。
    - [ ] `const` 成员函数：保证函数不修改对象状态。
    - [ ] **🎯 练习**：创建一个 `BankAccount` 类，余额为 private，提供 `deposit` 和 `withdraw` 方法，确保余额不能为负数。
- [ ] **继承与多态 (重难点)**
    - [ ] 继承关系：继承的权限 (`public` 继承最常用)。
    - [ ] **虚函数 (`virtual`)**：动态多态、虚函数表 (vtable) 原理。
    - [ ] 纯虚函数与抽象类：定义接口 (Interface)。
    - [ ] `override` 与 `final` (C++11)：显式标记重写与禁止继承。
    - [ ] 虚析构函数：防止删除基类指针时子类泄漏。
    - [ ] **🎯 练习**：实现 `Shape` 抽象类（含纯虚函数 `area()`），派生出 `Circle` 和 `Rectangle`，用 `Shape*` 指针数组循环计算总面积。

### 第三阶段：STL 标准库 (STL)

- [ ] **容器 (Containers)**
    - [ ] 序列容器：`std::vector` (动态数组，首选), `std::list` (双向链表), `std::deque`。
    - [ ] 关联容器：`std::map` (红黑树 Key-Value), `std::set` (去重)。
    - [ ] 无序容器：`std::unordered_map` (哈希表，O(1) 查找)。
    - [ ] **🎯 练习**：给定一个整数列表，使用 `std::map` 统计每个数字出现的频率，并按频率从高到低输出。
- [ ] **迭代器 (Iterators)**
    - [ ] 概念：泛型指针，容器与算法的桥梁 (`begin()`, `end()`)。
    - [ ] 失效问题：`vector` 扩容或删除元素后迭代器会失效。
    - [ ] **🎯 练习**：使用迭代器遍历 `vector`，删除其中所有的偶数（注意正确处理迭代器更新）。
- [ ] **算法 (Algorithms)**
    - [ ] 常用算法：`std::sort`, `std::find`, `std::reverse`, `std::accumulate`。
    - [ ] Lambda 表达式：匿名函数 `[](int x){ return x > 0; }`，作为算法的谓词。
    - [ ] **🎯 练习**：创建一个自定义结构体 `Person`，使用 `std::sort` 和 Lambda 表达式按“年龄”对 `vector<Person>` 进行降序排序。

### 第四阶段：高级特性 (Advanced)

- [ ] **智能指针 (Smart Pointers)**
    - [ ] `std::unique_ptr`：独占所有权，取代裸指针，零开销。
    - [ ] `std::shared_ptr`：引用计数，共享所有权。
    - [ ] `std::weak_ptr`：解决 shared_ptr 循环引用问题。
    - [ ] **🎯 练习**：构建一个双向链表节点，使用 `shared_ptr` 指向下一个节点，使用 `weak_ptr` 指向前一个节点，验证对象能否正确析构。
- [ ] **模板与泛型编程**
    - [ ] 函数/类模板：编写与类型无关的代码 (`template <typename T>`)。
    - [ ] 模板特化：针对特定类型（如 `bool` 或 `char*`）做特殊处理。
    - [ ] **🎯 练习**：实现一个简易的泛型栈 `Stack<T>`，支持 `push`, `pop`, `top` 操作。
- [ ] **移动语义 (Move Semantics)**
    - [ ] 左值与右值：理解 `lvalue` (持久对象) vs `rvalue` (临时对象)。
    - [ ] 右值引用 (`&&`) 与 `std::move`：所有权转移，避免深拷贝。
    - [ ] 移动构造函数：接管资源而非复制资源。
    - [ ] **🎯 练习**：编写一个管理大内存块的类，实现移动构造函数。对比使用 `std::move` 前后，放入 `vector` 时的性能/日志差异。

### 第五阶段：系统编程 (System Programming)

- [ ] **内存管理**
    - [ ] RAII 原则：资源获取即初始化，利用栈对象自动释放资源。
    - [ ] 内存对齐与 Padding：结构体大小的计算。
    - [ ] **🎯 练习**：编写一个简单的 `FileHandler` 类，遵循 RAII 原则，在构造中打开文件，析构中自动关闭文件。
- [ ] **多线程与并发**
    - [ ] 线程管理：`std::thread` 的创建与 `join/detach`。
    - [ ] 互斥与同步：`std::mutex`, `std::lock_guard` (自动解锁)。
    - [ ] 原子操作：`std::atomic` 实现无锁计数器。
    - [ ] 条件变量：`std::condition_variable` 实现生产者-消费者模型。
    - [ ] **🎯 练习**：实现“生产者-消费者”模型：一个线程往队列写数据，两个线程从队列读数据，使用互斥锁保护队列。

### 第六阶段：现代 C++ 与工程化

- [ ] **现代 C++ 新特性 (C++17/20)**
    - [ ] C++17：结构化绑定 `auto [x, y] = pair`，`std::optional`。
    - [ ] C++20：**Modules** (模块，替代头文件)，**Concepts** (约束模板)，**Coroutines** (协程)。
    - [ ] **🎯 练习**：使用 C++17 `std::filesystem` 遍历一个文件夹下的所有文件，并打印文件名。
- [ ] **设计模式**
    - [ ] 单例模式 (Singleton)：线程安全的懒汉式实现。
    - [ ] 工厂模式 (Factory)：解耦对象的创建。
    - [ ] 观察者模式 (Observer)：事件通知机制。
    - [ ] **🎯 练习**：使用观察者模式设计一个“气象站”，当温度更新时，自动通知所有注册的显示屏更新读数。

---

## 第二部分：网络编程 (Network Programming)

- [ ] **基础理论**
    - [ ] 网络协议：TCP/IP 协议栈，UDP vs TCP 的区别，三次握手与四次挥手。
    - [ ] I/O 模型：阻塞 I/O, 非阻塞 I/O, I/O 多路复用 (Select/Poll/Epoll)。
    - [ ] **🎯 练习**：使用 Wireshark 抓包，观察并分析一次 TCP 连接建立的过程。
- [ ] **Socket 编程**
    - [ ] 原生 API：`socket()`, `bind()`, `listen()`, `accept()`, `connect()` (Linux/Windows API)。
    - [ ] 字节序：大端序与小端序转换 (`htons`, `ntohl`)。
    - [ ] **🎯 练习**：编写一个基于 TCP 的简易 **Echo Server**（回显服务器）：客户端发送消息，服务器原样返回。
- [ ] **高性能网络库**
    - [ ] **Boost.Asio**：现代 C++ 异步网络编程事实标准。
    - [ ] 异步编程模型：Proactor 模式，回调函数与 `std::future`。
    - [ ] 序列化：Protobuf 或 JSON (nlohmann/json) 的使用。
    - [ ] **🎯 练习**：使用 Boost.Asio 实现一个简单的异步 HTTP Server，能响应 "Hello World" 请求。

---

## 第三部分：数据库编程 (Database)

- [ ] **基础与 SQL**
    - [ ] 关系型数据库：MySQL/PostgreSQL 基础，表设计，索引优化。
    - [ ] SQL 语句：`SELECT`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`。
    - [ ] **🎯 练习**：设计一个“图书管理系统”的数据库表结构（书名、作者、ISBN、库存）。
- [ ] **C++ 数据库接口**
    - [ ] **SQLite**：轻量级嵌入式数据库，C 语言 API 的 C++ 封装。
    - [ ] MySQL Connector/C++：连接 MySQL 数据库。
    - [ ] ORM (对象关系映射)：了解 ODB 或 SQLite_orm 库，将 C++ 类映射到数据库表。
    - [ ] **🎯 练习**：编写 C++ 程序，创建一个 SQLite 数据库文件，插入 10 条图书记录，并查询打印出来。
- [ ] **连接池技术**
    - [ ] 连接池原理：复用数据库连接，避免频繁握手开销。
    - [ ] **🎯 练习**：(进阶) 实现一个简单的数据库连接池类，维护固定数量的连接供多线程获取。

---

## 第四部分：GUI 开发 (Graphical User Interface)

- [ ] **Qt 框架 (首选)**
    - [ ] 核心机制：**信号与槽 (Signals & Slots)**，元对象系统 (MOC)。
    - [ ] 基础控件：`QPushButton`, `QLabel`, `QLineEdit`, 布局管理器 (`QVBoxLayout`)。
    - [ ] 事件处理：重写 `mousePressEvent` 等事件函数。
    - [ ] **🎯 练习**：使用 Qt 编写一个简易计算器，包含数字按钮和显示屏，实现加减乘除功能。
- [ ] **ImGui (工具开发首选)**
    - [ ] 立即模式 GUI (Immediate Mode GUI)：适合游戏调试工具或轻量级应用。
    - [ ] 渲染循环：在 OpenGL/DirectX 循环中绘制 UI。
    - [ ] **🎯 练习**：集成 Dear ImGui 到一个简单的窗口程序中，创建一个可以调节背景颜色的滑动条。