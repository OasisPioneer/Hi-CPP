# C++ 基础语法

## 1. 基础语法

### 1.1 数据类型
C++ 提供了多种内置数据类型，用于表示不同类型的数据：

- **整数类型**：
  - `int`：通常为 4 字节，范围约为 -2^31 到 2^31-1
  - `long long`：8 字节，范围约为 -2^63 到 2^63-1
  - 其他整数类型：`short` (2字节), `long` (通常4字节)
  - 无符号整数：`unsigned int`, `unsigned long long` 等

- **浮点类型**：
  - `double`：双精度浮点数，8字节，精度更高，通常优先使用
  - `float`：单精度浮点数，4字节
  - `long double`：扩展精度浮点数

- **布尔类型**：
  - `bool`：表示逻辑值，只有 `true` (1) 和 `false` (0) 两个取值

- **字符类型**：
  - `char`：单个字符，1字节，通常表示 ASCII 字符
  - `wchar_t`：宽字符，用于表示 Unicode 字符
  - `char16_t`, `char32_t`：C++11 引入的 Unicode 字符类型

### 1.2 变量常量

#### 变量初始化
C++ 支持多种变量初始化方式，推荐使用 C++11 引入的列表初始化 (`{}`)，更安全且语法一致：

```cpp
int a = 10;          // 传统初始化
int b(20);           // 构造函数初始化
int c = {30};        // C++11 列表初始化（带等号）
int d{40};           // C++11 列表初始化（不带等号）
int e{};             // 列表初始化，默认值为 0
```

#### 常量
- **`const`**：修饰的变量值不能被修改，运行时常量
  ```cpp
  const int MAX_AGE = 120;  // MAX_AGE 的值不能被修改
  ```

- **`constexpr`**：编译期常量，在编译时求值，性能更高
  ```cpp
  constexpr int PI = 3.14;  // 编译时计算
  constexpr int square(int x) { return x * x; }
  constexpr int area = square(5);  // 编译时计算为 25
  ```

### 1.3 运算符

#### 算术运算符
- `+`, `-`, `*`, `/`, `%` (取模)
- 注意：整数除法会截断小数部分

#### 逻辑运算符
- `&&` (逻辑与), `||` (逻辑或), `!` (逻辑非)
- 短路求值：`&&` 前半部分为假时，后半部分不会执行；`||` 前半部分为真时，后半部分不会执行

#### 位运算符
- `&` (按位与), `|` (按位或), `^` (按位异或), `~` (按位取反)
- `<<` (左移), `>>` (右移)

#### 其他运算符
- `sizeof`：返回类型或表达式的字节大小
  ```cpp
  sizeof(int);      // 4（通常）
  sizeof(double);   // 8
  ```
- 赋值运算符：`=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`
- 比较运算符：`==`, `!=`, `<`, `>`, `<=`, `>=`
- 递增/递减运算符：`++i` (前置), `i++` (后置), `--i`, `i--`

### 1.4 流程控制

#### if 语句
- 基础形式：
  ```cpp
  if (condition) {
      // 条件为真时执行
  } else if (another_condition) {
      // 另一个条件为真时执行
  } else {
      // 所有条件都为假时执行
  }
  ```

- C++17 引入的带初始化的 if 语句：
  ```cpp
  if (int x = getValue(); x > 0) {
      // x 只在 if 块内可见
  }
  ```

#### switch 语句
- 用于多分支选择，基于整数或枚举类型
- 注意：每个 case 后需要 `break`，否则会发生 fallthrough（贯穿）
  ```cpp
  switch (day) {
      case 1:
          cout << "Monday" << endl;
          break;
      case 2:
          cout << "Tuesday" << endl;
          break;
      default:
          cout << "Other day" << endl;
          break;
  }
  ```

#### for 循环
- 传统 for 循环：
  ```cpp
  for (int i = 0; i < 10; i++) {
      // 循环体
  }
  ```

- C++11 范围 for 循环（遍历容器或数组）：
  ```cpp
  int arr[] = {1, 2, 3, 4, 5};
  for (int num : arr) {
      cout << num << " ";
  }
  ```

#### while 循环
- 条件为真时执行循环体
  ```cpp
  while (condition) {
      // 循环体
  }
  ```

- do-while 循环：至少执行一次循环体
  ```cpp
  do {
      // 循环体
  } while (condition);
  ```

### 🎯 练习：猜数字游戏
编写一个“猜数字游戏”，使用 `while` 循环和 `if` 判断，并用 `const` 定义最大尝试次数。

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    srand(time(nullptr));  // 初始化随机数生成器
    const int SECRET_NUMBER = rand() % 100 + 1;  // 生成1-100的随机数
    const int MAX_ATTEMPTS = 10;  // 最大尝试次数
    int guess;
    int attempts = 0;

    cout << "欢迎来到猜数字游戏！" << endl;
    cout << "我已经想好了一个1到100之间的数字。" << endl;
    cout << "你有" << MAX_ATTEMPTS << "次机会来猜它。" << endl;

    while (attempts < MAX_ATTEMPTS) {
        cout << "\n请输入你的猜测：";
        cin >> guess;
        attempts++;

        if (guess == SECRET_NUMBER) {
            cout << "恭喜你！你猜对了！" << endl;
            cout << "你用了" << attempts << "次尝试。" << endl;
            return 0;
        } else if (guess < SECRET_NUMBER) {
            cout << "太小了！" << endl;
        } else {
            cout << "太大了！" << endl;
        }

        cout << "你还有" << MAX_ATTEMPTS - attempts << "次机会。" << endl;
    }

    cout << "\n很遗憾，你没有在规定次数内猜对。" << endl;
    cout << "秘密数字是：" << SECRET_NUMBER << endl;

    return 0;
}
```


## 3. 补充基础语法

### 3.1 枚举类型
枚举（enum）是一种用户定义的数据类型，用于定义命名的整数常量集合。

#### 3.1.1 传统枚举
```cpp
// 定义枚举类型
enum Color {
    RED,    // 0
    GREEN,  // 1
    BLUE    // 2
};

// 使用枚举
enum Color c = RED;
if (c == GREEN) {
    // 处理绿色
}
```

#### 3.1.2 带作用域的枚举（C++11）
带作用域的枚举（enum class）避免了命名冲突，更安全。
```cpp
// 定义带作用域的枚举
enum class Color {
    RED,
    GREEN,
    BLUE
};

// 使用带作用域的枚举
Color c = Color::RED;
if (c == Color::GREEN) {
    // 处理绿色
}
```

#### 3.1.3 自定义枚举值
```cpp
enum Color {
    RED = 1,
    GREEN = 2,
    BLUE = 4
};

// 位运算组合枚举值
Color combined = static_cast<Color>(RED | GREEN);
```

### 3.2 类型推导
C++11引入了`auto`关键字，用于自动推导变量类型，简化代码。

#### 3.2.1 auto 关键字
```cpp
auto i = 10;              // i 是 int 类型
auto d = 3.14;            // d 是 double 类型
auto s = "hello";         // s 是 const char* 类型
auto v = std::vector<int>{1, 2, 3};  // v 是 std::vector<int> 类型
```

#### 3.2.2 decltype 关键字
`decltype`用于推导表达式的类型。
```cpp
int x = 10;
decltype(x) y = 20;       // y 是 int 类型

double f();
decltype(f()) z;          // z 是 double 类型
```

### 3.3 流程控制补充

#### 3.3.1 break 和 continue 语句
- `break`：用于跳出循环或switch语句
- `continue`：用于跳过当前循环的剩余部分，进入下一次循环

```cpp
// break 示例
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // 跳出循环
    }
    std::cout << i << " ";  // 输出：0 1 2 3 4
}

// continue 示例
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // 跳过偶数
    }
    std::cout << i << " ";  // 输出：1 3 5 7 9
}
```

#### 3.3.2 goto 语句
`goto`语句用于无条件跳转到同一函数内的标记位置，不推荐频繁使用，容易导致代码难以维护。

```cpp
// goto 示例
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (i * j > 20) {
            goto end_loop;  // 跳转到标记位置
        }
    }
}

end_loop:
std::cout << "Loop ended early" << std::endl;
```

### 3.4 注释
注释用于解释代码，提高代码可读性，编译器会忽略注释。

#### 3.4.1 单行注释
```cpp
// 这是单行注释
int x = 10;  // 这也是单行注释
```

#### 3.4.2 多行注释
```cpp
/*
这是多行注释
可以跨越多行
*/
int y = 20;
```

#### 3.4.3 文档注释
用于生成文档的特殊注释格式，如Doxygen。
```cpp
/**
 * @brief 计算两个整数的和
 * @param a 第一个整数
 * @param b 第二个整数
 * @return 两个整数的和
 */
int add(int a, int b) {
    return a + b;
}
```

### 🎯 练习：计算器程序
编写一个简单的计算器程序，支持加减乘除四则运算，使用switch语句和循环实现。

```cpp
#include <iostream>

using namespace std;

int main() {
    char operation;
    double num1, num2;
    bool continue_calc = true;
    
    while (continue_calc) {
        // 输入操作符和操作数
        cout << "请输入操作符 (+, -, *, /): ";
        cin >> operation;
        
        cout << "请输入两个数字: ";
        cin >> num1 >> num2;
        
        // 执行计算
        switch (operation) {
            case '+':
                cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;
                break;
            case '-':
                cout << num1 << " - " << num2 << " = " << num1 - num2 << endl;
                break;
            case '*':
                cout << num1 << " * " << num2 << " = " << num1 * num2 << endl;
                break;
            case '/':
                if (num2 != 0) {
                    cout << num1 << " / " << num2 << " = " << num1 / num2 << endl;
                } else {
                    cout << "错误：除数不能为零！" << endl;
                }
                break;
            default:
                cout << "错误：无效的操作符！" << endl;
                break;
        }
        
        // 询问是否继续
        char choice;
        cout << "是否继续计算？(y/n): ";
        cin >> choice;
        if (choice != 'y' && choice != 'Y') {
            continue_calc = false;
        }
        
        cout << "------------------------" << endl;
    }
    
    cout << "计算器程序结束！" << endl;
    return 0;
}
```
