# C++ 类与对象

## 1. 类与对象的基本概念

### 1.1 什么是类和对象
- **类 (Class)**：是一种用户定义的数据类型，用于封装数据和操作数据的方法。类是对象的蓝图或模板。
- **对象 (Object)**：是类的实例，具有类中定义的属性和方法。

### 1.2 面向对象的三大特性
1. **封装 (Encapsulation)**：将数据和操作数据的方法封装在一起，隐藏实现细节，只暴露公共接口。
2. **继承 (Inheritance)**：允许创建新类，继承现有类的属性和方法，实现代码复用。
3. **多态 (Polymorphism)**：允许不同类的对象对同一消息做出不同响应，提高代码的灵活性和可扩展性。

## 2. 类的定义与对象的创建

### 2.1 类的定义
类的定义使用 `class` 关键字，包含成员变量（属性）和成员函数（方法）。

**语法：**
```cpp
class 类名 {
public:
    // 公共成员（对外接口）
    返回类型 成员函数名(参数列表);
    
private:
    // 私有成员（内部实现，对外隐藏）
    数据类型 成员变量名;
    
protected:
    // 保护成员（仅子类可访问）
    数据类型 成员变量名;
};
```

**示例：**
```cpp
class Person {
public:
    // 成员函数声明
    void setName(const std::string& name);
    void setAge(int age);
    void printInfo() const;
    
private:
    // 成员变量
    std::string m_name;
    int m_age;
};
```

### 2.2 类的实现
类的成员函数通常在类外实现，使用作用域解析运算符 `::` 来指定所属的类。

**示例：**
```cpp
// 实现Person类的成员函数
void Person::setName(const std::string& name) {
    m_name = name;
}

void Person::setAge(int age) {
    if (age >= 0) {
        m_age = age;
    }
}

void Person::printInfo() const {
    std::cout << "姓名：" << m_name << ", 年龄：" << m_age << std::endl;
}
```

### 2.3 对象的创建与使用

**示例：**
```cpp
int main() {
    // 创建对象
    Person p1;  // 默认构造函数
    
    // 使用成员函数
    p1.setName("张三");
    p1.setAge(20);
    p1.printInfo();  // 输出：姓名：张三, 年龄：20
    
    // 指针方式创建对象
    Person* p2 = new Person();
    p2->setName("李四");
    p2->setAge(25);
    p2->printInfo();  // 输出：姓名：李四, 年龄：25
    
    // 释放动态创建的对象
    delete p2;
    
    return 0;
}
```

## 3. 构造函数与析构函数

### 3.1 构造函数
构造函数是一种特殊的成员函数，用于初始化对象，在对象创建时自动调用。

**特点：**
- 函数名与类名相同
- 没有返回类型（包括 void）
- 可以有参数，支持重载
- 可以被显式调用

#### 3.1.1 默认构造函数
默认构造函数是没有参数或所有参数都有默认值的构造函数。如果类中没有定义任何构造函数，编译器会自动生成一个默认构造函数。

**示例：**
```cpp
class Person {
public:
    // 默认构造函数
    Person() {
        m_name = "";
        m_age = 0;
        std::cout << "默认构造函数被调用" << std::endl;
    }
    
    // 带默认参数的构造函数
    Person(const std::string& name = "", int age = 0) {
        m_name = name;
        m_age = age;
        std::cout << "带默认参数的构造函数被调用" << std::endl;
    }
    
private:
    std::string m_name;
    int m_age;
};
```

#### 3.1.2 带参数的构造函数
带参数的构造函数用于在创建对象时初始化成员变量。

**示例：**
```cpp
class Person {
public:
    // 带参数的构造函数
    Person(const std::string& name, int age) {
        m_name = name;
        m_age = age;
    }
    
private:
    std::string m_name;
    int m_age;
};

// 使用带参数的构造函数创建对象
Person p("张三", 20);
```

#### 3.1.3 初始化列表
初始化列表是一种更高效的初始化成员变量的方式，直接在构造函数名后使用 `:` 后跟成员变量的初始化。

**语法：**
```cpp
类名(参数列表) : 成员变量1(初始值1), 成员变量2(初始值2), ... {
    // 构造函数体
}
```

**示例：**
```cpp
class Person {
public:
    // 使用初始化列表的构造函数
    Person(const std::string& name, int age) 
        : m_name(name), m_age(age) {
        // 构造函数体可以为空，或包含其他初始化逻辑
    }
    
private:
    std::string m_name;
    int m_age;
};
```

**初始化列表的优势：**
1. 效率更高：直接初始化成员变量，避免了先默认初始化再赋值的开销
2. 可以初始化 const 成员变量和引用成员变量
3. 可以初始化基类成员

### 3.2 析构函数
析构函数是一种特殊的成员函数，用于清理对象占用的资源，在对象销毁时自动调用。

**特点：**
- 函数名是在类名前加 `~`
- 没有返回类型
- 没有参数，不支持重载
- 一个类只有一个析构函数

**示例：**
```cpp
class FileHandler {
public:
    // 构造函数：打开文件
    FileHandler(const std::string& filename) {
        m_file = fopen(filename.c_str(), "r");
        if (m_file == nullptr) {
            std::cerr << "无法打开文件：" << filename << std::endl;
        }
    }
    
    // 析构函数：关闭文件
    ~FileHandler() {
        if (m_file != nullptr) {
            fclose(m_file);
            m_file = nullptr;
            std::cout << "文件已关闭" << std::endl;
        }
    }
    
private:
    FILE* m_file;
};

// 使用示例
int main() {
    {  // 作用域开始
        FileHandler fh("test.txt");  // 创建对象，打开文件
        // 使用文件...
    }  // 作用域结束，对象销毁，自动调用析构函数关闭文件
    
    return 0;
}
```

## 4. 三/五法则

三/五法则是指在 C++ 中，当一个类需要自定义以下五个特殊成员函数中的一个时，通常需要自定义全部五个：

1. **析构函数**：释放资源
2. **拷贝构造函数**：复制对象
3. **拷贝赋值运算符**：赋值对象
4. **移动构造函数**：移动对象（C++11）
5. **移动赋值运算符**：移动赋值对象（C++11）

### 4.1 拷贝构造函数
拷贝构造函数用于创建一个新对象，作为现有对象的副本。

**语法：**
```cpp
类名(const 类名& other);
```

**示例：**
```cpp
class Person {
public:
    // 默认构造函数
    Person() : m_age(0) {}
    
    // 带参数的构造函数
    Person(const std::string& name, int age) 
        : m_name(name), m_age(age) {}
    
    // 拷贝构造函数
    Person(const Person& other) 
        : m_name(other.m_name), m_age(other.m_age) {
        std::cout << "拷贝构造函数被调用" << std::endl;
    }
    
private:
    std::string m_name;
    int m_age;
};

// 使用示例
int main() {
    Person p1("张三", 20);
    Person p2 = p1;  // 调用拷贝构造函数
    Person p3(p1);   // 调用拷贝构造函数
    
    return 0;
}
```

### 4.2 拷贝赋值运算符
拷贝赋值运算符用于将一个对象的值赋给另一个已存在的对象。

**语法：**
```cpp
类名& operator=(const 类名& other);
```

**示例：**
```cpp
class Person {
public:
    // 默认构造函数
    Person() : m_age(0) {}
    
    // 带参数的构造函数
    Person(const std::string& name, int age) 
        : m_name(name), m_age(age) {}
    
    // 拷贝赋值运算符
    Person& operator=(const Person& other) {
        if (this != &other) {  // 避免自赋值
            m_name = other.m_name;
            m_age = other.m_age;
            std::cout << "拷贝赋值运算符被调用" << std::endl;
        }
        return *this;
    }
    
private:
    std::string m_name;
    int m_age;
};

// 使用示例
int main() {
    Person p1("张三", 20);
    Person p2;
    p2 = p1;  // 调用拷贝赋值运算符
    
    return 0;
}
```

### 4.3 移动构造函数（C++11）
移动构造函数用于将一个临时对象的资源转移到新对象，避免不必要的拷贝。

**语法：**
```cpp
类名(类名&& other) noexcept;
```

**示例：**
```cpp
class String {
public:
    // 默认构造函数
    String() : m_data(nullptr), m_size(0) {}
    
    // 带参数的构造函数
    String(const char* str) {
        m_size = strlen(str);
        m_data = new char[m_size + 1];
        strcpy(m_data, str);
    }
    
    // 拷贝构造函数
    String(const String& other) {
        m_size = other.m_size;
        m_data = new char[m_size + 1];
        strcpy(m_data, other.m_data);
        std::cout << "拷贝构造函数被调用" << std::endl;
    }
    
    // 移动构造函数
    String(String&& other) noexcept 
        : m_data(other.m_data), m_size(other.m_size) {
        other.m_data = nullptr;  // 避免原对象析构时释放资源
        other.m_size = 0;
        std::cout << "移动构造函数被调用" << std::endl;
    }
    
    // 析构函数
    ~String() {
        if (m_data != nullptr) {
            delete[] m_data;
            m_data = nullptr;
        }
    }
    
private:
    char* m_data;
    size_t m_size;
};

// 使用示例
int main() {
    String s1("Hello");
    String s2 = std::move(s1);  // 调用移动构造函数
    
    return 0;
}
```

### 4.4 移动赋值运算符（C++11）
移动赋值运算符用于将一个临时对象的资源转移到另一个已存在的对象。

**语法：**
```cpp
类名& operator=(类名&& other) noexcept;
```

**示例：**
```cpp
class String {
public:
    // ... 其他构造函数 ...
    
    // 拷贝赋值运算符
    String& operator=(const String& other) {
        if (this != &other) {
            delete[] m_data;
            m_size = other.m_size;
            m_data = new char[m_size + 1];
            strcpy(m_data, other.m_data);
            std::cout << "拷贝赋值运算符被调用" << std::endl;
        }
        return *this;
    }
    
    // 移动赋值运算符
    String& operator=(String&& other) noexcept {
        if (this != &other) {
            delete[] m_data;
            m_data = other.m_data;
            m_size = other.m_size;
            other.m_data = nullptr;
            other.m_size = 0;
            std::cout << "移动赋值运算符被调用" << std::endl;
        }
        return *this;
    }
    
    // ... 析构函数 ...
    
private:
    char* m_data;
    size_t m_size;
};

// 使用示例
int main() {
    String s1("Hello");
    String s2;
    s2 = std::move(s1);  // 调用移动赋值运算符
    
    return 0;
}
```

## 5. 静态成员

静态成员是属于类而不是对象的成员，所有对象共享同一个静态成员。

### 5.1 静态成员变量
静态成员变量在类中声明，在类外定义和初始化。

**示例：**
```cpp
class Counter {
public:
    // 静态成员函数
    static void increment() {
        s_count++;
    }
    
    static int getCount() {
        return s_count;
    }
    
private:
    // 静态成员变量声明
    static int s_count;
};

// 静态成员变量定义和初始化
int Counter::s_count = 0;

// 使用示例
int main() {
    Counter::increment();  // 调用静态成员函数
    Counter::increment();
    std::cout << "Count: " << Counter::getCount() << std::endl;  // 输出：Count: 2
    
    return 0;
}
```

### 5.2 静态成员函数
静态成员函数没有 `this` 指针，只能访问静态成员变量和其他静态成员函数，不能访问非静态成员。

**特点：**
- 可以直接通过类名调用，不需要创建对象
- 不能使用 `const` 修饰
- 不能是虚函数

**示例：**
```cpp
class Math {
public:
    // 静态成员函数
    static int add(int a, int b) {
        return a + b;
    }
    
    static int multiply(int a, int b) {
        return a * b;
    }
};

// 使用示例
int main() {
    int sum = Math::add(3, 4);        // 7
    int product = Math::multiply(3, 4);  // 12
    
    return 0;
}
```

## 🎯 练习：Student 类设计

**任务：** 设计一个 `Student` 类，包含姓名和成绩，使用初始化列表构造，并统计当前内存中有多少个 `Student` 对象（使用 static）。

**解决方案：**

```cpp
#include <iostream>
#include <string>

class Student {
public:
    // 默认构造函数
    Student() : m_name(""), m_score(0) {
        s_count++;
        std::cout << "Student 默认构造函数被调用，当前对象数：" << s_count << std::endl;
    }
    
    // 带参数的构造函数，使用初始化列表
    Student(const std::string& name, double score) 
        : m_name(name), m_score(score) {
        s_count++;
        std::cout << "Student 带参数构造函数被调用，当前对象数：" << s_count << std::endl;
    }
    
    // 拷贝构造函数
    Student(const Student& other) 
        : m_name(other.m_name), m_score(other.m_score) {
        s_count++;
        std::cout << "Student 拷贝构造函数被调用，当前对象数：" << s_count << std::endl;
    }
    
    // 析构函数
    ~Student() {
        s_count--;
        std::cout << "Student 析构函数被调用，当前对象数：" << s_count << std::endl;
    }
    
    // 设置姓名
    void setName(const std::string& name) {
        m_name = name;
    }
    
    // 设置成绩
    void setScore(double score) {
        m_score = score;
    }
    
    // 获取姓名
    std::string getName() const {
        return m_name;
    }
    
    // 获取成绩
    double getScore() const {
        return m_score;
    }
    
    // 静态成员函数：获取当前对象数
    static int getCount() {
        return s_count;
    }
    
private:
    std::string m_name;  // 姓名
    double m_score;      // 成绩
    
    static int s_count;  // 静态成员变量：统计对象数量
};

// 初始化静态成员变量
int Student::s_count = 0;

int main() {
    std::cout << "程序开始，当前 Student 对象数：" << Student::getCount() << std::endl;
    
    {  // 作用域开始
        Student s1("张三", 90.5);  // 创建第一个对象
        Student s2("李四", 85.0);  // 创建第二个对象
        
        std::cout << "s1: 姓名=" << s1.getName() << ", 成绩=" << s1.getScore() << std::endl;
        std::cout << "s2: 姓名=" << s2.getName() << ", 成绩=" << s2.getScore() << std::endl;
        
        Student s3 = s1;  // 拷贝构造，创建第三个对象
        
        std::cout << "作用域内，当前 Student 对象数：" << Student::getCount() << std::endl;
    }  // 作用域结束，三个对象销毁
    
    std::cout << "程序结束，当前 Student 对象数：" << Student::getCount() << std::endl;
    
    return 0;
}
```

**输出结果：**
```
程序开始，当前 Student 对象数：0
Student 带参数构造函数被调用，当前对象数：1
Student 带参数构造函数被调用，当前对象数：2
s1: 姓名=张三, 成绩=90.5
s2: 姓名=李四, 成绩=85
Student 拷贝构造函数被调用，当前对象数：3
作用域内，当前 Student 对象数：3
Student 析构函数被调用，当前对象数：2
Student 析构函数被调用，当前对象数：1
Student 析构函数被调用，当前对象数：0
程序结束，当前 Student 对象数：0
```

## 6. 类的大小

类的大小取决于其非静态成员变量的大小，不包括静态成员变量和成员函数。

**示例：**
```cpp
class Empty {
    // 空类，编译器会生成默认构造函数等，但类的大小为1字节
};

class Person {
private:
    char m_gender;  // 1字节
    int m_age;      // 4字节
    double m_height; // 8字节
    // 由于内存对齐，总大小为 16 字节
};

int main() {
    std::cout << "Empty类大小：" << sizeof(Empty) << "字节" << std::endl;  // 1字节
    std::cout << "Person类大小：" << sizeof(Person) << "字节" << std::endl;  // 16字节
    
    return 0;
}
```

## 7. 友元

友元允许类外部的函数或其他类访问该类的私有成员。友元破坏了封装性，应谨慎使用。

### 7.1 友元函数
```cpp
class Rectangle {
public:
    Rectangle(double width, double height) 
        : m_width(width), m_height(height) {}
    
    // 声明友元函数
    friend double calculateArea(const Rectangle& rect);
    
private:
    double m_width;
    double m_height;
};

// 友元函数实现，可以访问Rectangle的私有成员
double calculateArea(const Rectangle& rect) {
    return rect.m_width * rect.m_height;
}
```

### 7.2 友元类
```cpp
class A {
public:
    A(int value) : m_value(value) {}
    
    // 声明友元类
    friend class B;
    
private:
    int m_value;
};

class B {
public:
    void printAValue(const A& a) {
        // 可以访问A的私有成员
        std::cout << "A::m_value = " << a.m_value << std::endl;
    }
};
```

## 总结

- **类与对象**：类是对象的蓝图，对象是类的实例
- **构造函数**：用于初始化对象，支持默认构造、带参数构造和初始化列表
- **析构函数**：用于清理对象资源，在对象销毁时自动调用
- **三/五法则**：自定义一个特殊成员函数时，通常需要自定义全部五个
- **静态成员**：属于类而不是对象，所有对象共享同一个静态成员
- **友元**：允许外部访问类的私有成员，破坏封装性，应谨慎使用

类与对象是 C++ 面向对象编程的基础，掌握这些概念对于理解和使用 C++ 的面向对象特性至关重要。通过本章节的学习，你应该能够设计和实现简单的类，并理解其内部工作原理。