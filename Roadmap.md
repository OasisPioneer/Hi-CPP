> [!CAUTION]
> [EN] This roadmap is not complete and the specific learning sequence is being adjusted gradually.
> 
> [CN] 本路线图并不完整且具体学习顺序正在逐步调整

```Mermaid

%%{init: {
  "theme": "default",
  "themeVariables": {
    "fontFamily": "Source Han Sans, 思源黑体, sans-serif"
  }
}}%%

graph LR
    RootNode(C++ 学习路线)-->PartOne(语言核心);

        PartOne-->PartOne-Chapter-1(学前准备);

            PartOne-Chapter-1-->PartOne-Chapter-1-Section-1(语言介绍);

                %% C++ 的发展历史
                PartOne-Chapter-1-Section-1-->PartOne-Chapter-1-Section-1-FirstParagraph(什么是 C++?);
                %% C++ 的特点与应用领域
                PartOne-Chapter-1-Section-1-->PartOne-Chapter-1-Section-1-SecondParagraph(为什么要学习 C++?);
                PartOne-Chapter-1-Section-1-->PartOne-Chapter-1-Section-1-ThirdParagraph(C VS C++);

            PartOne-Chapter-1-->PartOne-Chapter-1-Section-2(环境搭建);

                PartOne-Chapter-1-Section-2-->PartOne-Chapter-1-Section-2-FirstParagraph(编译器);
                PartOne-Chapter-1-Section-2-->PartOne-Chapter-1-Section-2-SecondParagraph(调试器);
                PartOne-Chapter-1-Section-2-->PartOne-Chapter-1-Section-2-ThirdParagraph(构建工具);
                PartOne-Chapter-1-Section-2-->PartOne-Chapter-1-Section-2-FourthParagraph(开发工具);

        PartOne-->PartOne-Chapter-2(基础语法);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-1(基础数据类型);

                PartOne-Chapter-2-Section-1-->PartOne-Chapter-2-Section-1-FirstParagraph(整数型);
                PartOne-Chapter-2-Section-1-->PartOne-Chapter-2-Section-1-SecondParagraph(浮点型);
                PartOne-Chapter-2-Section-1-->PartOne-Chapter-2-Section-1-ThirdParagraph(布尔型);
                PartOne-Chapter-2-Section-1-->PartOne-Chapter-2-Section-1-FourthParagraph(字符型);
                PartOne-Chapter-2-Section-1-->PartOne-Chapter-2-Section-1-FifthParagraph(空类型);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-2(变量与常量);

                PartOne-Chapter-2-Section-2-->PartOne-Chapter-2-Section-2-FifthParagraph(类型别名：typedef与using);
                PartOne-Chapter-2-Section-2-->PartOne-Chapter-2-Section-2-SixthParagraph(constexpr与常量表达式)

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-3(运算符表达式);

                PartOne-Chapter-2-Section-3-->PartOne-Chapter-2-Section-3-FirstParagraph(算术运算符);
                PartOne-Chapter-2-Section-3-->PartOne-Chapter-2-Section-3-SecondParagraph(关系运算符);
                PartOne-Chapter-2-Section-3-->PartOne-Chapter-2-Section-3-ThirdParagraph(逻辑运算符);
                PartOne-Chapter-2-Section-3-->PartOne-Chapter-2-Section-3-FourthParagraph(位运算符);
                PartOne-Chapter-2-Section-3-->PartOne-Chapter-2-Section-3-FifthParagraph(赋值运算符);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-4(流程控制);

                %% if Switch goto
                PartOne-Chapter-2-Section-4-->PartOne-Chapter-2-Section-4-FirstParagraph(条件语句);
                %% while do-while for
                PartOne-Chapter-2-Section-4-->PartOne-Chapter-2-Section-4-SecondParagraph(循环语句);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-5(函数与作用域);

                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-FirstParagraph(定义函数);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-SecondParagraph(调用函数);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-ThirdParagraph(参数传递);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-FourthParagraph(局部变量);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-FifthParagraph(全局变量);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-SixthParagraph(变量作用域);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-SeventhParagraph(命名空间);
                PartOne-Chapter-2-Section-5-->PartOne-Chapter-2-Section-5-EighthParagraph(函数重载);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-6(数组与字符串);

                PartOne-Chapter-2-Section-6-->PartOne-Chapter-2-Section-6-FirstParagraph(一维数组);
                PartOne-Chapter-2-Section-6-->PartOne-Chapter-2-Section-6-SecondParagraph(多维数组);
                PartOne-Chapter-2-Section-6-->PartOne-Chapter-2-Section-6-ThirdParagraph(C 语言风格字符串);
                PartOne-Chapter-2-Section-6-->PartOne-Chapter-2-Section-6-FourthParagraph(C++ 标准库中的字符串类);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-7(复合类型);

                PartOne-Chapter-2-Section-7-->PartOne-Chapter-2-Section-7-FirstParagraph(结构体);
                PartOne-Chapter-2-Section-7-->PartOne-Chapter-2-Section-7-SecondParagraph(联合体);
                PartOne-Chapter-2-Section-7-->PartOne-Chapter-2-Section-7-ThirdParagraph(枚举类型);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-8(输入输出流);

                PartOne-Chapter-2-Section-8-->PartOne-Chapter-2-Section-8-FirstParagraph(标准流与对象);
                PartOne-Chapter-2-Section-8-->PartOne-Chapter-2-Section-8-SecondParagraph(错误流);
                PartOne-Chapter-2-Section-8-->PartOne-Chapter-2-Section-8-ThirdParagraph(流状态检查);

            PartOne-Chapter-2-->PartOne-Chapter-2-Section-9(预处理器与宏);

                PartOne-Chapter-2-Section-9-->PartOne-Chapter-2-Section-9-FirstParagraph(预处理);
                PartOne-Chapter-2-Section-9-->PartOne-Chapter-2-Section-9-SecondParagraph(宏定义);
                PartOne-Chapter-2-Section-9-->PartOne-Chapter-2-Section-9-ThirdParagraph(条件编译);
                PartOne-Chapter-2-Section-9-->PartOne-Chapter-2-Section-9-FourthParagraph(理解用途和限制);

        PartOne-->PartOne-Chapter-3(面向对象);

            PartOne-Chapter-3-->PartOne-Chapter-3-Section-1(类与对象);

                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-FirstParagraph(类的定义);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-SecondParagraph(创建对象);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-ThirdParagraph(销毁对象);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-FourthParagraph(成员函数);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-FifthParagraph(构造函数);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-SixthParagraph(析构函数);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-SeventhParagraph(拷贝控制);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-EighthParagraph(赋值运算符重载);
                PartOne-Chapter-3-Section-1-->PartOne-Chapter-3-Section-1-NinthParagraph(静态成员和友元函数);

            PartOne-Chapter-3-->PartOne-Chapter-3-Section-2(封装与访问控制);

                PartOne-Chapter-3-Section-2-->PartOne-Chapter-3-Section-2-FirstParagraph(公有);
                PartOne-Chapter-3-Section-2-->PartOne-Chapter-3-Section-2-SecondParagraph(私有);
                PartOne-Chapter-3-Section-2-->PartOne-Chapter-3-Section-2-ThirdParagraph(保护成员);
                PartOne-Chapter-3-Section-2-->PartOne-Chapter-3-Section-2-FourthParagraph(接口与分离实现);

            PartOne-Chapter-3-->PartOne-Chapter-3-Section-3(继承与多态);

                %% 基类与派生类 单继承 多继承
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-FirstParagraph(继承关系);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-SecondParagraph(继承控制);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-ThirdParagraph(虚函数);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-FourthParagraph(抽象类);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-FifthParagraph(接口);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-SixthParagraph(纯虚函数);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-SeventhParagraph(虚析构函数);
                PartOne-Chapter-3-Section-3-->PartOne-Chapter-3-Section-3-EighthParagraph(多态应用);

            PartOne-Chapter-3-->PartOne-Chapter-3-Section-4(运算符重载与类型转换);

                PartOne-Chapter-3-Section-4-->PartOne-Chapter-3-Section-4-FirstParagraph(运算符重载);
                %% 析造函数和类型转换运算符
                PartOne-Chapter-3-Section-4-->PartOne-Chapter-3-Section-4-SecondParagraph(类型转换函数);

        PartOne-->PartOne-Chapter-4(容器与算法);

            PartOne-Chapter-4-->PartOne-Chapter-4-Section-1(容器);

                PartOne-Chapter-4-Section-1-->PartOne-Chapter-4-Section-1-FirstParagraph(序列容器);
                PartOne-Chapter-4-Section-1-->PartOne-Chapter-4-Section-1-SecondParagraph(关联容器);
                PartOne-Chapter-4-Section-1-->PartOne-Chapter-4-Section-1-ThirdParagraph(无序容器);
                PartOne-Chapter-4-Section-1-->PartOne-Chapter-4-Section-1-FourthParagraph(容器适配器);
                PartOne-Chapter-4-Section-1-->PartOne-Chapter-4-Section-1-FifthParagraph(容器选择策略);

            PartOne-Chapter-4-->PartOne-Chapter-4-Section-2(迭代器);

                PartOne-Chapter-4-Section-2-->PartOne-Chapter-4-Section-2-FirstParagraph(迭代器类型);
                PartOne-Chapter-4-Section-2-->PartOne-Chapter-4-Section-2-SecondParagraph(迭代器操作);
                PartOne-Chapter-4-Section-2-->PartOne-Chapter-4-Section-2-ThirdParagraph(迭代器失效);
                PartOne-Chapter-4-Section-2-->PartOne-Chapter-4-Section-2-FourthParagraph(反向迭代器);

            PartOne-Chapter-4-->PartOne-Chapter-4-Section-3(算法);

                PartOne-Chapter-4-Section-3-->PartOne-Chapter-4-Section-3-FirstParagraph(排序算法);
                PartOne-Chapter-4-Section-3-->PartOne-Chapter-4-Section-3-SecondParagraph(查找算法);
                PartOne-Chapter-4-Section-3-->PartOne-Chapter-4-Section-3-ThirdParagraph(变换算法);
                PartOne-Chapter-4-Section-3-->PartOne-Chapter-4-Section-3-FourthParagraph(数值算法);
                PartOne-Chapter-4-Section-3-->PartOne-Chapter-4-Section-3-FifthParagraph(算法与迭代器结合使用);

        PartOne-->PartOne-Chapter-5(指针与内存);

            PartOne-Chapter-5-->PartOne-Chapter-5-Section-1(引用与指针);

                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-FirstParagraph(引用折叠);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-SecondParagraph(完美转发);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-ThirdParagraph(函数指针);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-FourthParagraph(指针数组);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-FifthParagraph(数组指针);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-SixthParagraph(右值引用和移动语义);
                PartOne-Chapter-5-Section-1-->PartOne-Chapter-5-Section-1-SeventhParagraph(转发引用与模板参数推导);

            PartOne-Chapter-5-->PartOne-Chapter-5-Section-2(智能指针);

                PartOne-Chapter-5-Section-2-->PartOne-Chapter-5-Section-2-FirstParagraph(unique_ptr);
                PartOne-Chapter-5-Section-2-->PartOne-Chapter-5-Section-2-SecondParagraph(shared_ptr);
                PartOne-Chapter-5-Section-2-->PartOne-Chapter-5-Section-2-ThirdParagraph(weak_ptr);
                PartOne-Chapter-5-Section-2-->PartOne-Chapter-5-Section-2-FourthParagraph(智能指针与原始指针的转换);

            PartOne-Chapter-5-->PartOne-Chapter-5-Section-3(内存管理);

                PartOne-Chapter-5-Section-3-->PartOne-Chapter-5-Section-3-FirstParagraph(动态内存分配与释放);
                PartOne-Chapter-5-Section-3-->PartOne-Chapter-5-Section-3-SecondParagraph(内存池与定制分配器);
                PartOne-Chapter-5-Section-3-->PartOne-Chapter-5-Section-3-ThirdParagraph(智能指针在资源管理中的应用);
                PartOne-Chapter-5-Section-3-->PartOne-Chapter-5-Section-3-FourthParagraph(RAII 原则);
                PartOne-Chapter-5-Section-3-->PartOne-Chapter-5-Section-3-FifthParagraph(内存泄露检测与避免);

        PartOne-->PartOne-Chapter-6(模板与泛型编程);

            PartOne-Chapter-6-->PartOne-Chapter-6-Section-1(模板);
                PartOne-Chapter-6-Section-1-->PartOne-Chapter-6-Section-1-FirstParagraph(函数模板);
                PartOne-Chapter-6-Section-1-->PartOne-Chapter-6-Section-1-SecondParagraph(类模板);
                %% 全特化 偏特化
                PartOne-Chapter-6-Section-1-->PartOne-Chapter-6-Section-1-ThirdParagraph(模板特化);
                %% 编译器计算 type_traits
                PartOne-Chapter-6-Section-1-->PartOne-Chapter-6-Section-1-FourthParagraph(模板元编程基础);
                %% 通用算法 容器适配
                PartOne-Chapter-6-Section-1-->PartOne-Chapter-6-Section-1-FifthParagraph(泛型编程);

        PartOne-->PartOne-Chapter-7(异常处理);

            PartOne-Chapter-7-->PartOne-Chapter-7-Section-1(异常机制);
            PartOne-Chapter-7-->PartOne-Chapter-7-Section-2(异常类型);
            PartOne-Chapter-7-->PartOne-Chapter-7-Section-3(异常安全);
            PartOne-Chapter-7-->PartOne-Chapter-7-Section-4(noexcept 关键字);

        PartOne-->PartOne-Chapter-8(多线程);

            PartOne-Chapter-8-->PartOne-Chapter-8-Section-1(线程的创建和管理);
            PartOne-Chapter-8-->PartOne-Chapter-8-Section-2(线程同步);

                PartOne-Chapter-8-Section-2-->PartOne-Chapter-8-Section-2-FirstParagraph(互斥锁);
                PartOne-Chapter-8-Section-2-->PartOne-Chapter-8-Section-2-SecondParagraph(条件变量);
                PartOne-Chapter-8-Section-2-->PartOne-Chapter-8-Section-2-ThirdParagraph(信号量);

            PartOne-Chapter-8-->PartOne-Chapter-8-Section-3(原子操作);
            PartOne-Chapter-8-->PartOne-Chapter-8-Section-4(线程池);
            PartOne-Chapter-8-->PartOne-Chapter-8-Section-5(并发);

        PartOne-->PartOne-Chapter-9(文件处理);

            PartOne-Chapter-9-->PartOne-Chapter-9-Section-1(文件流);
            PartOne-Chapter-9-->PartOne-Chapter-9-Section-2(文本文件读写);
            PartOne-Chapter-9-->PartOne-Chapter-9-Section-3(二进制文件读写);
            PartOne-Chapter-9-->PartOne-Chapter-9-Section-4(文件系统的遍历和操作);

        PartOne-->PartOne-Chapter-10(性能分析与调优);

            PartOne-Chapter-10-->PartOne-Chapter-10-Section-1(性能分析工具);
            PartOne-Chapter-10-->PartOne-Chapter-10-Section-2(代码调试技巧);
            PartOne-Chapter-10-->PartOne-Chapter-10-Section-3(编译优化);

        PartOne-->PartOne-Chapter-11(现代特性);

            PartOne-Chapter-11-->PartOne-Chapter-11-Section-1(C++ 11);
            PartOne-Chapter-11-->PartOne-Chapter-11-Section-2(C++ 14);
            PartOne-Chapter-11-->PartOne-Chapter-11-Section-3(C++ 17);
            PartOne-Chapter-11-->PartOne-Chapter-11-Section-4(C++ 20);
            PartOne-Chapter-11-->PartOne-Chapter-11-Section-5(C++ 23);

    RootNode-->PartTwo(网络编程);

        %% 什么是网络编程
        %% 网络基础（TCP/IP）
        %% 如何实现网络通信
        %% Socket 编程
        %% 异步 IO 模型
        %% 开发简单的服务器和客户端项目
        %% 学习 Boost.Asio 等网络框架
        %% 高并发服务器设计

    RootNode-->PartThree(数据库);

        %% 什么是数据库
        %% 从零开始制作数据库
        %% 学习主流数据库

    RootNode-->PartFour(图形界面);

        %% TUI GUI
        %% 实现简单的 TUI 界面
        %% 学习 Qt 框架



    %% ===============================
    %%      Mermaid 颜色
    %% ===============================

    classDef Root fill:#3366cc,color:#fff;
    classDef PartOne_lv2 fill:#99cc33,color:#fff;
    classDef PartTwo_lv2 fill:#9933cc,color:#fff;
    classDef PartThree_lv2 fill:#33cccc,color:#fff;
    classDef PartFour_lv2 fill:#cc3333,color:#fff;

    class RootNode Root;
    class PartOne PartOne_lv2;
    class PartTwo PartTwo_lv2;
    class PartThree PartThree_lv2;
    class PartFour PartFour_lv2;
```