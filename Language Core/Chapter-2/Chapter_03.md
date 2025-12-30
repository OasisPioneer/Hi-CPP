# C++ 数组与字符串

## 1. 数组

### 1.1 C风格数组

C风格数组是从C语言继承而来的数组类型，它具有以下特点：

- **固定大小**：数组大小必须在编译时确定，不能动态改变
- **连续内存**：数组元素在内存中连续存储
- **隐式转换**：数组名会隐式转换为指向首元素的指针
- **无边界检查**：访问越界元素会导致未定义行为

#### 1.1.1 数组的定义与初始化

**基本语法：**
```cpp
数据类型 数组名[数组大小];
```

**示例：**
```cpp
// 定义一个包含5个整数的数组
int arr[5];

// 初始化数组
int arr1[5] = {1, 2, 3, 4, 5};  // 初始化所有元素
int arr2[5] = {1, 2, 3};         // 前3个元素初始化，其余为0
int arr3[] = {1, 2, 3, 4, 5};    // 编译器自动推导数组大小为5
int arr4[5] = {};                // 所有元素初始化为0

// 字符数组（C风格字符串）
char str1[6] = "hello";          // 包含结束符'\0'
char str2[] = "world";           // 编译器自动计算大小为6（包含'\0'）
```

#### 1.1.2 数组的访问与操作

**示例：**
```cpp
int arr[5] = {1, 2, 3, 4, 5};

// 访问数组元素
int first = arr[0];      // 第一个元素，值为1
int last = arr[4];       // 最后一个元素，值为5

// 修改数组元素
arr[2] = 10;             // 将第三个元素改为10

// 遍历数组
for (int i = 0; i < 5; i++) {
    std::cout << arr[i] << " ";
}
std::cout << std::endl;

// 数组大小计算
size_t size = sizeof(arr) / sizeof(arr[0]);  // 5
```

#### 1.1.3 C风格数组的局限性

1. **大小固定**：无法在运行时动态调整大小
2. **容易越界**：没有内置的边界检查机制
3. **隐式指针转换**：数组名隐式转换为指针，丢失了大小信息
4. **传参问题**：作为函数参数时，退化为指针，无法直接获取大小
5. **不安全的字符串操作**：C风格字符串需要手动管理结束符'\0'

### 1.2 std::array（C++11）

`std::array` 是C++11引入的固定大小数组容器，它结合了C风格数组的性能和STL容器的安全性与便利性。

#### 1.2.1 std::array的定义与初始化

**头文件：** `<array>`

**基本语法：**
```cpp
std::array<数据类型, 数组大小> 数组名;
```

**示例：**
```cpp
#include <array>

// 定义一个包含5个整数的std::array
std::array<int, 5> arr;

// 初始化std::array
std::array<int, 5> arr1 = {1, 2, 3, 4, 5};  // 初始化所有元素
std::array<int, 5> arr2 = {1, 2, 3};         // 前3个元素初始化，其余为0
std::array<int, 5> arr3{};                   // 所有元素初始化为0

// 使用列表初始化（C++11及以上）
std::array<int, 5> arr4{1, 2, 3, 4, 5};
```

#### 1.2.2 std::array的访问与操作

`std::array` 提供了多种成员函数来访问和操作数组元素：

**示例：**
```cpp
std::array<int, 5> arr = {1, 2, 3, 4, 5};

// 访问元素
int first = arr[0];              // 下标访问，无边界检查
int second = arr.at(1);          // 带边界检查的访问
int third = arr.front();         // 第一个元素
int last = arr.back();           // 最后一个元素

// 修改元素
arr[2] = 10;
arr.at(3) = 20;

// 获取大小
size_t size = arr.size();        // 5
bool is_empty = arr.empty();     // false

// 遍历数组
// 方式1：传统for循环
for (size_t i = 0; i < arr.size(); i++) {
    std::cout << arr[i] << " ";
}

// 方式2：范围for循环（C++11）
for (int num : arr) {
    std::cout << num << " ";
}

// 方式3：迭代器
for (auto it = arr.begin(); it != arr.end(); ++it) {
    std::cout << *it << " ";
}

// 填充数组
arr.fill(0);                     // 所有元素设置为0

// 交换两个数组
std::array<int, 5> arr5 = {6, 7, 8, 9, 10};
arr.swap(arr5);                  // 交换arr和arr5的内容
```

#### 1.2.3 std::array的优势

1. **类型安全**：提供了类型安全的访问方式
2. **边界检查**：`at()` 成员函数提供边界检查
3. **保留大小信息**：作为函数参数时不会退化为指针，保留大小信息
4. **STL兼容**：可以使用STL算法和迭代器
5. **高性能**：与C风格数组性能相当，无额外开销

### 1.3 数组作为函数参数

#### 1.3.1 C风格数组作为函数参数

C风格数组作为函数参数时，会退化为指针，丢失大小信息。因此，通常需要同时传递数组的大小。

**示例：**
```cpp
// 错误：数组退化为指针，无法获取大小
void print_array(int arr[]) {
    // sizeof(arr) 返回的是指针大小，不是数组大小
    size_t size = sizeof(arr) / sizeof(arr[0]);  // 错误
}

// 正确：同时传递数组和大小
void print_array(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

// 调用示例
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    print_array(arr, size);
    return 0;
}
```

#### 1.3.2 std::array作为函数参数

`std::array` 作为函数参数时，会保留大小信息，更加安全和方便。

**示例：**
```cpp
// 使用模板参数推导大小
template <size_t N>
void print_array(const std::array<int, N>& arr) {
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

// 调用示例
int main() {
    std::array<int, 5> arr = {1, 2, 3, 4, 5};
    print_array(arr);  // 自动推导N=5
    return 0;
}
```

## 2. 字符串

### 2.1 C风格字符串

C风格字符串是一个以空字符'\0'结尾的字符数组，它具有以下特点：

- **以'\0'结尾**：必须以空字符结尾，否则无法正确处理
- **不安全操作**：字符串操作函数（如`strcpy`、`strcat`）没有边界检查
- **手动管理内存**：需要手动分配和释放内存

**常用的C风格字符串函数：**
- `strlen(s)`：计算字符串长度（不包括'\0'）
- `strcpy(dst, src)`：复制字符串
- `strcat(dst, src)`：拼接字符串
- `strcmp(s1, s2)`：比较字符串
- `strncpy(dst, src, n)`：复制最多n个字符
- `strncat(dst, src, n)`：拼接最多n个字符

**示例：**
```cpp
#include <cstring>

char str1[20] = "Hello";
char str2[20] = "World";

// 计算字符串长度
size_t len1 = strlen(str1);  // 5

// 拼接字符串
strcat(str1, " ");          // str1变为"Hello "
strcat(str1, str2);         // str1变为"Hello World"

// 比较字符串
int result = strcmp(str1, str2);  // 非0，表示不相等

// 复制字符串
strcpy(str2, str1);         // str2变为"Hello World"
```

### 2.2 std::string（C++98）

`std::string` 是C++标准库提供的字符串类，它提供了安全、方便的字符串操作方式。

#### 2.2.1 std::string的定义与初始化

**头文件：** `<string>`

**示例：**
```cpp
#include <string>

// 默认构造
std::string s1;

// 从C风格字符串构造
std::string s2 = "Hello";
std::string s3("World");

// 从字符和长度构造
std::string s4(5, 'a');      // "aaaaa"

// 从另一个string构造
std::string s5(s2);          // 拷贝构造，s5="Hello"

// 从string的一部分构造
std::string s6(s2, 1, 3);    // 从索引1开始，长度3，s6="ell"

// 从迭代器构造
std::string s7(s2.begin(), s2.end());  // s7="Hello"
```

#### 2.2.2 std::string的基本操作

**示例：**
```cpp
std::string s = "Hello";

// 获取长度
size_t len = s.length();     // 5
size_t size = s.size();       // 5

// 检查是否为空
bool is_empty = s.empty();    // false

// 清空字符串
s.clear();                    // s变为空字符串

// 重新设置字符串
s = "World";
```

#### 2.2.3 std::string的访问与修改

**示例：**
```cpp
std::string s = "Hello";

// 访问字符
char c1 = s[0];               // 'H'，无边界检查
char c2 = s.at(1);            // 'e'，带边界检查
char c3 = s.front();          // 'H'
char c4 = s.back();           // 'o'

// 修改字符
s[0] = 'h';                   // s变为"hello"
s.at(1) = 'E';                // s变为"hEllo"
s.back() = 'O';               // s变为"hEllO"

// 末尾添加字符
s.push_back('!');             // s变为"hEllO!"
s += '?';                    // s变为"hEllO!?"

// 插入字符
s.insert(5, " World");        // s变为"hEllO World!?"

// 删除字符
s.erase(5, 6);               // 从索引5开始删除6个字符，s变为"hEllO!?"

// 替换字符
s.replace(0, 5, "Hello");    // 从索引0开始，替换5个字符，s变为"Hello!?"
```

#### 2.2.4 std::string的字符串操作

**示例：**
```cpp
std::string s1 = "Hello";
std::string s2 = "World";

// 拼接字符串
std::string s3 = s1 + " " + s2;  // "Hello World"
s1 += " " + s2;                  // s1变为"Hello World"

// 比较字符串
bool eq = (s1 == s3);           // true
bool neq = (s1 != s2);          // true
bool lt = (s1 < s2);            // false
bool gt = (s1 > s2);            // true

// 查找子串
size_t pos1 = s1.find("World");  // 6，返回子串起始位置
size_t pos2 = s1.find('o');      // 4，返回字符第一次出现的位置
size_t pos3 = s1.rfind('o');     // 7，返回字符最后一次出现的位置
size_t pos4 = s1.find("xyz");    // std::string::npos，表示未找到

// 获取子串
std::string sub1 = s1.substr(0, 5);  // "Hello"，从索引0开始，长度5
std::string sub2 = s1.substr(6);     // "World"，从索引6开始到末尾

// 转换为C风格字符串
const char* c_str = s1.c_str();      // 返回const char*
const char* data = s1.data();        // C++17前返回const char*，C++17后返回char*

// 转换大小写（需要自己实现或使用第三方库）
// 例如：将字符串转换为大写
for (char& c : s1) {
    c = std::toupper(c);
}
// s1变为"HELLO WORLD"
```

#### 2.2.5 std::string的优势

1. **安全**：自动管理内存，避免缓冲区溢出
2. **方便**：提供了丰富的成员函数和操作符
3. **高效**：内部实现优化，性能良好
4. **兼容**：可以与C风格字符串相互转换
5. **STL兼容**：可以使用STL算法和迭代器

### 2.3 std::string_view（C++17）

`std::string_view` 是C++17引入的字符串视图类，它提供了一种非所有权的字符串访问方式，可以高效地查看字符串而无需拷贝。

#### 2.3.1 std::string_view的定义与初始化

**头文件：** `<string_view>`

**示例：**
```cpp
#include <string_view>

// 从C风格字符串构造
std::string_view sv1 = "Hello";

// 从std::string构造
std::string s = "World";
std::string_view sv2 = s;

// 从字符数组和长度构造
const char* arr = "Hello World";
std::string_view sv3(arr, 5);  // "Hello"

// 从另一个string_view构造
std::string_view sv4(sv1);     // 拷贝构造
```

#### 2.3.2 std::string_view的操作

`std::string_view` 提供了与 `std::string` 类似的接口，但不提供修改字符串内容的操作。

**示例：**
```cpp
std::string_view sv = "Hello World";

// 获取长度
size_t len = sv.length();     // 11
size_t size = sv.size();       // 11

// 检查是否为空
bool is_empty = sv.empty();    // false

// 访问字符
char c1 = sv[0];               // 'H'
char c2 = sv.at(1);            // 'e'
char c3 = sv.front();          // 'H'
char c4 = sv.back();           // 'd'

// 查找子串
size_t pos1 = sv.find("World");  // 6
size_t pos2 = sv.find('o');      // 4

// 获取子串
std::string_view sub1 = sv.substr(0, 5);  // "Hello"
std::string_view sub2 = sv.substr(6);     // "World"

// 移除前缀和后缀
sv.remove_prefix(6);           // sv变为"World"
sv.remove_suffix(1);           // sv变为"Worl"

// 转换为std::string
std::string s = static_cast<std::string>(sv);  // "Worl"
```

#### 2.3.3 std::string_view的优势

1. **高效**：不需要拷贝字符串，节省内存和时间
2. **灵活**：可以指向任何字符串类型（C风格字符串、std::string、字符数组等）
3. **安全**：提供边界检查，避免越界访问
4. **轻量级**：只包含指针和长度，开销很小

#### 2.3.4 std::string_view的注意事项

1. **不拥有所有权**：它只是字符串的视图，不管理底层字符串的生命周期
2. **底层字符串必须保持有效**：如果底层字符串被销毁或修改，string_view会变得无效
3. **不能修改字符串内容**：string_view是只读的，不能修改字符串

## 3. 字符串与数字的转换

### 3.1 字符串转数字

C++11及以上提供了以下函数来将字符串转换为数字：

- `std::stoi(s)`：转换为int
- `std::stol(s)`：转换为long
- `std::stoll(s)`：转换为long long
- `std::stof(s)`：转换为float
- `std::stod(s)`：转换为double
- `std::stold(s)`：转换为long double

**示例：**
```cpp
#include <string>
#include <iostream>

int main() {
    std::string s1 = "123";
    std::string s2 = "3.14";
    
    // 字符串转整数
    int i = std::stoi(s1);           // 123
    long l = std::stol(s1);          // 123
    long long ll = std::stoll(s1);   // 123
    
    // 字符串转浮点数
    float f = std::stof(s2);         // 3.14f
    double d = std::stod(s2);        // 3.14
    long double ld = std::stold(s2); // 3.14L
    
    return 0;
}
```

### 3.2 数字转字符串

C++11及以上提供了以下函数来将数字转换为字符串：

- `std::to_string(n)`：将各种数字类型转换为std::string

**示例：**
```cpp
#include <string>
#include <iostream>

int main() {
    int i = 123;
    double d = 3.14;
    
    // 整数转字符串
    std::string s1 = std::to_string(i);  // "123"
    
    // 浮点数转字符串
    std::string s2 = std::to_string(d);  // "3.140000"
    
    return 0;
}
```

## 🎯 练习：统计单词个数并反转句子

**任务：** 输入一行英文句子，使用 `std::string` 统计其中单词的个数，并反转整个句子输出。

**解决方案：**

```cpp
#include <iostream>
#include <string>
#include <algorithm>

// 统计句子中的单词个数
int count_words(const std::string& sentence) {
    int count = 0;
    bool in_word = false;
    
    for (char c : sentence) {
        if (std::isspace(static_cast<unsigned char>(c))) {
            in_word = false;
        } else if (!in_word) {
            in_word = true;
            count++;
        }
    }
    
    return count;
}

// 反转整个句子
std::string reverse_sentence(std::string sentence) {
    // 首先反转整个句子
    std::reverse(sentence.begin(), sentence.end());
    
    // 然后反转每个单词
    auto start = sentence.begin();
    while (start != sentence.end()) {
        // 找到单词的结束位置
        auto end = std::find(start, sentence.end(), ' ');
        
        // 反转当前单词
        std::reverse(start, end);
        
        // 移动到下一个单词的开始
        if (end != sentence.end()) {
            start = end + 1;
        } else {
            break;
        }
    }
    
    return sentence;
}

int main() {
    std::string sentence;
    
    std::cout << "请输入一行英文句子：" << std::endl;
    std::getline(std::cin, sentence);  // 使用getline读取整行，包括空格
    
    // 统计单词个数
    int word_count = count_words(sentence);
    std::cout << "单词个数：" << word_count << std::endl;
    
    // 反转句子
    std::string reversed = reverse_sentence(sentence);
    std::cout << "反转后的句子：" << reversed << std::endl;
    
    return 0;
}
```

**输入输出示例：**
```
请输入一行英文句子：
Hello world this is a test
单词个数：6
反转后的句子：test a is this world Hello
```

## 🎯 进阶练习：字符串处理工具函数

**任务：** 实现一个字符串处理工具类，包含以下功能：
1. 判断字符串是否为回文
2. 去除字符串两端的空格
3. 将字符串按分隔符分割成vector
4. 替换字符串中的所有指定子串

**解决方案：**

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <cctype>

class StringUtils {
public:
    // 判断字符串是否为回文
    static bool is_palindrome(const std::string& s) {
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            // 跳过非字母数字字符（可选，根据需求调整）
            while (left < right && !std::isalnum(static_cast<unsigned char>(s[left]))) {
                left++;
            }
            while (left < right && !std::isalnum(static_cast<unsigned char>(s[right]))) {
                right--;
            }
            
            // 比较字符，忽略大小写
            if (std::tolower(static_cast<unsigned char>(s[left])) != 
                std::tolower(static_cast<unsigned char>(s[right]))) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
    
    // 去除字符串两端的空格
    static std::string trim(const std::string& s) {
        if (s.empty()) {
            return s;
        }
        
        size_t start = 0;
        size_t end = s.length() - 1;
        
        // 找到第一个非空格字符
        while (start <= end && std::isspace(static_cast<unsigned char>(s[start]))) {
            start++;
        }
        
        // 找到最后一个非空格字符
        while (end >= start && std::isspace(static_cast<unsigned char>(s[end]))) {
            end--;
        }
        
        return s.substr(start, end - start + 1);
    }
    
    // 将字符串按分隔符分割成vector
    static std::vector<std::string> split(const std::string& s, char delimiter) {
        std::vector<std::string> result;
        std::string current;
        
        for (char c : s) {
            if (c == delimiter) {
                if (!current.empty()) {
                    result.push_back(current);
                    current.clear();
                }
            } else {
                current += c;
            }
        }
        
        if (!current.empty()) {
            result.push_back(current);
        }
        
        return result;
    }
    
    // 替换字符串中的所有指定子串
    static std::string replace_all(const std::string& s, const std::string& old_str, const std::string& new_str) {
        if (old_str.empty()) {
            return s;
        }
        
        std::string result = s;
        size_t pos = 0;
        
        while ((pos = result.find(old_str, pos)) != std::string::npos) {
            result.replace(pos, old_str.length(), new_str);
            pos += new_str.length();
        }
        
        return result;
    }
};

int main() {
    // 测试回文判断
    std::string palindrome = "A man a plan a canal Panama";
    std::cout << "\"" << palindrome << "\" 是回文吗？ " << (StringUtils::is_palindrome(palindrome) ? "是" : "否") << std::endl;
    
    // 测试trim
    std::string with_spaces = "   Hello World   ";
    std::cout << "原始字符串：\"" << with_spaces << "\"" << std::endl;
    std::cout << "trim后：\"" << StringUtils::trim(with_spaces) << "\"" << std::endl;
    
    // 测试split
    std::string to_split = "apple,banana,orange,grape";
    std::vector<std::string> fruits = StringUtils::split(to_split, ',');
    std::cout << "分割结果：";
    for (const auto& fruit : fruits) {
        std::cout << fruit << " ";
    }
    std::cout << std::endl;
    
    // 测试replace_all
    std::string to_replace = "Hello World Hello";
    std::string replaced = StringUtils::replace_all(to_replace, "Hello", "Hi");
    std::cout << "原始字符串：\"" << to_replace << "\"" << std::endl;
    std::cout << "替换后：\"" << replaced << "\"" << std::endl;
    
    return 0;
}
```

**输出结果：**
```
"A man a plan a canal Panama" 是回文吗？ 是
原始字符串："   Hello World   "
trim后："Hello World"
分割结果：apple banana orange grape 
原始字符串："Hello World Hello"
替换后："Hi World Hi"
```

## 总结

- **数组**：C风格数组是基础但不安全，std::array提供了类型安全和STL兼容性
- **字符串**：std::string是C++中处理字符串的首选，提供了安全、方便的字符串操作
- **字符串视图**：std::string_view是C++17引入的高效字符串查看方式，避免不必要的拷贝
- **字符串转换**：C++11提供了方便的字符串与数字之间的转换函数

通过学习和掌握这些内容，你将能够在C++中高效、安全地处理数组和字符串，为后续的C++学习打下坚实的基础。