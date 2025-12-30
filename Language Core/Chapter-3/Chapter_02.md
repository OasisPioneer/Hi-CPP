# C++ 封装与访问控制

## 1. 封装的概念

封装（Encapsulation）是面向对象编程的三大特性之一，它指的是将数据（成员变量）和操作数据的方法（成员函数）封装在一起，形成一个独立的单元（类），并对外部隐藏对象的内部实现细节，只暴露必要的公共接口。

### 1.1 封装的优势

1. **隐藏实现细节**：外部代码只需要知道类提供的公共接口，不需要知道内部实现
2. **保护数据安全**：防止外部代码意外修改对象的内部状态
3. **提高代码可维护性**：可以在不影响外部代码的情况下修改内部实现
4. **简化接口**：只暴露必要的方法，使类的使用更加简单
5. **实现信息隐藏**：遵循"最少知识原则"，减少类之间的耦合

## 2. 访问控制符

C++提供了三种访问控制符来控制类成员的访问权限：`public`、`private`和`protected`。

### 2.1 public 访问权限

`public`成员可以被任何外部代码访问，包括类的实例、其他类和全局函数。通常将类的接口（对外提供的方法）声明为`public`。

**示例：**
```cpp
class Person {
public:
    // 公共成员函数（接口）
    void setName(const std::string& name) {
        m_name = name;
    }
    
    std::string getName() const {
        return m_name;
    }
    
private:
    std::string m_name;  // 私有成员变量
};

// 外部代码可以访问公共成员
int main() {
    Person p;
    p.setName("张三");  // 合法，setName是public
    std::string name = p.getName();  // 合法，getName是public
    // p.m_name = "李四";  // 错误，m_name是private
    
    return 0;
}
```

### 2.2 private 访问权限

`private`成员只能被类的内部成员函数和友元访问，外部代码无法直接访问。通常将类的数据（成员变量）和内部辅助方法声明为`private`。

**示例：**
```cpp
class Calculator {
public:
    // 公共接口：计算两个数的和
    int add(int a, int b) {
        return a + b;
    }
    
    // 公共接口：计算阶乘
    int factorial(int n) {
        if (n < 0) {
            return -1;  // 错误处理
        }
        return calculateFactorial(n);  // 调用私有辅助方法
    }
    
private:
    // 私有辅助方法：实际计算阶乘
    int calculateFactorial(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        return n * calculateFactorial(n - 1);
    }
};
```

### 2.3 protected 访问权限

`protected`成员可以被类的内部成员函数、友元和子类访问，但外部代码无法直接访问。通常将需要被子类继承的成员声明为`protected`。

**示例：**
```cpp
class Animal {
protected:
    std::string m_name;  // 保护成员，子类可以访问
    
public:
    Animal(const std::string& name) : m_name(name) {}
    
    virtual void makeSound() const = 0;  // 纯虚函数
};

class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {}
    
    void makeSound() const override {
        std::cout << m_name << " 汪汪汪！" << std::endl;  // 子类可以访问父类的protected成员
    }
};

int main() {
    Dog dog("旺财");
    dog.makeSound();  // 输出：旺财 汪汪汪！
    // std::cout << dog.m_name << std::endl;  // 错误，m_name是protected
    
    return 0;
}
```

### 2.4 访问控制的默认规则

- **类（class）**：默认访问权限是`private`
- **结构体（struct）**：默认访问权限是`public`

**示例：**
```cpp
class DefaultClass {
    int x;  // 默认private
public:
    int y;  // public
};

struct DefaultStruct {
    int x;  // 默认public
private:
    int y;  // private
};
```

## 3. 访问控制符的使用建议

1. **成员变量**：通常声明为`private`，通过`public`的访问器（getter）和修改器（setter）方法来访问和修改
2. **成员函数**：
   - 对外提供的接口声明为`public`
   - 内部辅助方法声明为`private`
   - 需要被子类访问的方法声明为`protected`
3. **遵循"最小权限原则"**：只授予必要的访问权限，避免过度暴露

## 4. const 成员函数

`const`成员函数是指在函数声明的末尾加上`const`关键字的成员函数，它承诺不会修改对象的状态（即不会修改任何非`mutable`成员变量）。

### 4.1 const 成员函数的语法

**语法：**
```cpp
返回类型 函数名(参数列表) const;
```

**示例：**
```cpp
class Person {
public:
    Person(const std::string& name, int age) : m_name(name), m_age(age) {}
    
    // const成员函数：不会修改对象状态
    std::string getName() const {
        return m_name;
    }
    
    int getAge() const {
        return m_age;
    }
    
    // 非const成员函数：可以修改对象状态
    void setName(const std::string& name) {
        m_name = name;
    }
    
    void setAge(int age) {
        if (age >= 0) {
            m_age = age;
        }
    }
    
private:
    std::string m_name;
    int m_age;
};
```

### 4.2 const 成员函数的特点

1. **不能修改非`mutable`成员变量**
2. **只能调用其他`const`成员函数**
3. **可以被`const`对象和非`const`对象调用**
4. **非`const`成员函数只能被非`const`对象调用**

**示例：**
```cpp
int main() {
    Person p1("张三", 20);  // 非const对象
    const Person p2("李四", 25);  // const对象
    
    // 非const对象可以调用const和非const成员函数
    p1.getName();  // 合法
    p1.setName("王五");  // 合法
    
    // const对象只能调用const成员函数
    p2.getName();  // 合法
    // p2.setName("赵六");  // 错误，const对象不能调用非const成员函数
    
    return 0;
}
```

### 4.3 const 成员函数与重载

`const`关键字可以用于函数重载，即可以定义两个同名函数，一个是`const`版本，一个是非`const`版本。

**示例：**
```cpp
class String {
public:
    // 非const版本：返回非const引用，可以修改
    char& operator[](size_t index) {
        return m_data[index];
    }
    
    // const版本：返回const引用，不能修改
    const char& operator[](size_t index) const {
        return m_data[index];
    }
    
private:
    char m_data[100];
};

int main() {
    String s1;  // 非const对象
    s1[0] = 'H';  // 调用非const版本，可以修改
    
    const String s2;  // const对象
    char c = s2[0];  // 调用const版本，只能读取
    // s2[0] = 'H';  // 错误，const版本返回const引用
    
    return 0;
}
```

## 5. mutable 关键字

`mutable`关键字用于修饰成员变量，表示该变量可以在`const`成员函数中被修改。

**用途：**
- 用于记录对象的使用次数或缓存计算结果
- 用于实现懒加载（lazy loading）
- 用于线程同步的互斥量

**示例：**
```cpp
class Person {
public:
    Person(const std::string& name) : m_name(name), m_accessCount(0) {}
    
    // const成员函数，但可以修改mutable成员变量
    std::string getName() const {
        m_accessCount++;  // 合法，m_accessCount是mutable
        return m_name;
    }
    
    int getAccessCount() const {
        return m_accessCount;
    }
    
private:
    std::string m_name;
    mutable int m_accessCount;  // mutable成员，可以在const函数中修改
};

int main() {
    const Person p("张三");
    std::cout << p.getName() << std::endl;  // 访问一次
    std::cout << p.getName() << std::endl;  // 访问两次
    std::cout << "访问次数：" << p.getAccessCount() << std::endl;  // 输出：2
    
    return 0;
}
```

## 6. 访问器（Getter）和修改器（Setter）

访问器（Getter）和修改器（Setter）是用于访问和修改私有成员变量的公共方法，它们是实现封装的重要手段。

### 6.1 访问器（Getter）

访问器用于获取私有成员变量的值，通常是`const`成员函数。

**命名约定：**
- 对于布尔类型，通常以`is`或`has`开头
- 对于其他类型，通常以`get`开头

**示例：**
```cpp
class Circle {
public:
    Circle(double radius) : m_radius(radius) {}
    
    // 访问器：获取半径
    double getRadius() const {
        return m_radius;
    }
    
    // 访问器：获取面积
    double getArea() const {
        return 3.14159 * m_radius * m_radius;
    }
    
    // 访问器：判断是否是单位圆
    bool isUnitCircle() const {
        return m_radius == 1.0;
    }
    
private:
    double m_radius;
};
```

### 6.2 修改器（Setter）

修改器用于修改私有成员变量的值，通常包含参数验证逻辑。

**命名约定：**
- 通常以`set`开头

**示例：**
```cpp
class Student {
public:
    Student() : m_age(0), m_score(0.0) {}
    
    // 修改器：设置姓名
    void setName(const std::string& name) {
        m_name = name;
    }
    
    // 修改器：设置年龄，包含验证
    void setAge(int age) {
        if (age >= 0 && age <= 150) {
            m_age = age;
        }
    }
    
    // 修改器：设置成绩，包含验证
    void setScore(double score) {
        if (score >= 0.0 && score <= 100.0) {
            m_score = score;
        }
    }
    
private:
    std::string m_name;
    int m_age;
    double m_score;
};
```

## 7. 友元

友元（Friend）允许类外部的函数或其他类访问该类的私有成员。友元破坏了封装性，应谨慎使用。

### 7.1 友元函数

友元函数是指在类中声明为友元的非成员函数，它可以访问类的私有成员。

**示例：**
```cpp
class Point {
public:
    Point(double x, double y) : m_x(x), m_y(y) {}
    
    // 声明友元函数
    friend double distance(const Point& p1, const Point& p2);
    
private:
    double m_x;
    double m_y;
};

// 友元函数实现：计算两点之间的距离
double distance(const Point& p1, const Point& p2) {
    double dx = p1.m_x - p2.m_x;  // 可以访问私有成员
    double dy = p1.m_y - p2.m_y;  // 可以访问私有成员
    return std::sqrt(dx * dx + dy * dy);
}
```

### 7.2 友元类

友元类是指在类中声明为友元的其他类，它的所有成员函数都可以访问该类的私有成员。

**示例：**
```cpp
class Engine {
private:
    int m_horsepower;
    
    // 声明友元类
    friend class Car;
    
public:
    Engine(int horsepower) : m_horsepower(horsepower) {}
};

class Car {
public:
    Car(Engine& engine) : m_engine(engine) {}
    
    void printEngineInfo() {
        // 可以访问Engine的私有成员
        std::cout << "发动机马力：" << m_engine.m_horsepower << std::endl;
    }
    
private:
    Engine& m_engine;
};
```

## 🎯 练习：BankAccount 类设计

**任务：** 创建一个 `BankAccount` 类，余额为 private，提供 `deposit` 和 `withdraw` 方法，确保余额不能为负数。

**解决方案：**

```cpp
#include <iostream>
#include <string>

class BankAccount {
public:
    // 构造函数：初始化账户
    BankAccount(const std::string& accountNumber, const std::string& ownerName, double initialBalance = 0.0)
        : m_accountNumber(accountNumber), m_ownerName(ownerName), m_balance(initialBalance) {
        // 确保初始余额非负
        if (m_balance < 0.0) {
            m_balance = 0.0;
        }
    }
    
    // 存款方法
    void deposit(double amount) {
        if (amount > 0.0) {
            m_balance += amount;
            std::cout << "成功存入：" << amount << " 元" << std::endl;
        } else {
            std::cout << "存款金额必须大于0" << std::endl;
        }
    }
    
    // 取款方法
    bool withdraw(double amount) {
        if (amount <= 0.0) {
            std::cout << "取款金额必须大于0" << std::endl;
            return false;
        }
        
        if (m_balance >= amount) {
            m_balance -= amount;
            std::cout << "成功取出：" << amount << " 元" << std::endl;
            return true;
        } else {
            std::cout << "余额不足，无法取出：" << amount << " 元" << std::endl;
            return false;
        }
    }
    
    // 显示账户信息
    void displayInfo() const {
        std::cout << "------------------------" << std::endl;
        std::cout << "账户号码：" << m_accountNumber << std::endl;
        std::cout << "账户所有者：" << m_ownerName << std::endl;
        std::cout << "当前余额：" << m_balance << " 元" << std::endl;
        std::cout << "------------------------" << std::endl;
    }
    
    // 访问器：获取账户号码
    std::string getAccountNumber() const {
        return m_accountNumber;
    }
    
    // 访问器：获取账户所有者
    std::string getOwnerName() const {
        return m_ownerName;
    }
    
    // 访问器：获取当前余额
    double getBalance() const {
        return m_balance;
    }
    
private:
    std::string m_accountNumber;  // 账户号码
    std::string m_ownerName;      // 账户所有者
    double m_balance;             // 账户余额（私有，只能通过方法访问）
};

int main() {
    // 创建银行账户
    BankAccount account("123456789", "张三", 1000.0);
    
    // 显示初始信息
    account.displayInfo();
    
    // 存款操作
    account.deposit(500.0);
    account.displayInfo();
    
    // 取款操作
    account.withdraw(300.0);
    account.displayInfo();
    
    // 尝试超额取款
    account.withdraw(2000.0);
    account.displayInfo();
    
    // 尝试存入负数
    account.deposit(-100.0);
    account.displayInfo();
    
    return 0;
}
```

**输出结果：**
```
------------------------
账户号码：123456789
账户所有者：张三
当前余额：1000 元
------------------------
成功存入：500 元
------------------------
账户号码：123456789
账户所有者：张三
当前余额：1500 元
------------------------
成功取出：300 元
------------------------
账户号码：123456789
账户所有者：张三
当前余额：1200 元
------------------------
余额不足，无法取出：2000 元
------------------------
账户号码：123456789
账户所有者：张三
当前余额：1200 元
------------------------
存款金额必须大于0
------------------------
账户号码：123456789
账户所有者：张三
当前余额：1200 元
------------------------
```

## 🎯 进阶练习：Employee 类设计

**任务：** 设计一个 `Employee` 类，包含以下成员：
1. 私有成员变量：姓名、工号、月薪、奖金
2. 公共方法：
   - 构造函数：初始化所有成员变量
   - 访问器：获取所有成员变量的值
   - 修改器：设置月薪和奖金（包含验证）
   - 计算年薪的方法（月薪×12 + 奖金）
   - 显示员工信息的方法

**解决方案：**

```cpp
#include <iostream>
#include <string>

class Employee {
public:
    // 构造函数
    Employee(const std::string& name, const std::string& id, double monthlySalary, double bonus)
        : m_name(name), m_id(id), m_monthlySalary(0.0), m_bonus(0.0) {
        // 使用修改器设置月薪和奖金，确保合法性
        setMonthlySalary(monthlySalary);
        setBonus(bonus);
    }
    
    // 访问器：获取姓名
    std::string getName() const {
        return m_name;
    }
    
    // 访问器：获取工号
    std::string getId() const {
        return m_id;
    }
    
    // 访问器：获取月薪
    double getMonthlySalary() const {
        return m_monthlySalary;
    }
    
    // 访问器：获取奖金
    double getBonus() const {
        return m_bonus;
    }
    
    // 修改器：设置月薪
    void setMonthlySalary(double salary) {
        if (salary >= 0.0) {
            m_monthlySalary = salary;
        } else {
            std::cout << "月薪不能为负数" << std::endl;
        }
    }
    
    // 修改器：设置奖金
    void setBonus(double bonus) {
        if (bonus >= 0.0) {
            m_bonus = bonus;
        } else {
            std::cout << "奖金不能为负数" << std::endl;
        }
    }
    
    // 计算年薪
    double calculateAnnualSalary() const {
        return m_monthlySalary * 12 + m_bonus;
    }
    
    // 显示员工信息
    void displayInfo() const {
        std::cout << "------------------------" << std::endl;
        std::cout << "员工姓名：" << m_name << std::endl;
        std::cout << "员工工号：" << m_id << std::endl;
        std::cout << "月薪：" << m_monthlySalary << " 元" << std::endl;
        std::cout << "奖金：" << m_bonus << " 元" << std::endl;
        std::cout << "年薪：" << calculateAnnualSalary() << " 元" << std::endl;
        std::cout << "------------------------" << std::endl;
    }
    
private:
    std::string m_name;       // 姓名
    std::string m_id;         // 工号
    double m_monthlySalary;   // 月薪
    double m_bonus;           // 奖金
};

int main() {
    // 创建员工对象
    Employee emp("李四", "EMP001", 8000.0, 20000.0);
    
    // 显示初始信息
    emp.displayInfo();
    
    // 修改月薪和奖金
    emp.setMonthlySalary(9000.0);
    emp.setBonus(25000.0);
    
    // 显示修改后的信息
    emp.displayInfo();
    
    // 尝试设置负数月薪
    emp.setMonthlySalary(-1000.0);
    
    return 0;
}
```

**输出结果：**
```
------------------------
员工姓名：李四
员工工号：EMP001
月薪：8000 元
奖金：20000 元
年薪：116000 元
------------------------
------------------------
员工姓名：李四
员工工号：EMP001
月薪：9000 元
奖金：25000 元
年薪：133000 元
------------------------
月薪不能为负数
```

## 总结

- **封装**是将数据和方法封装在一起，隐藏内部实现，只暴露公共接口
- **访问控制符**：
  - `public`：对外接口，可被任何代码访问
  - `private`：内部实现，只能被类自身和友元访问
  - `protected`：可被类自身、友元和子类访问
- **const 成员函数**：承诺不修改对象状态，只能调用其他 const 成员函数
- **mutable 关键字**：允许在 const 成员函数中修改的成员变量
- **访问器和修改器**：用于安全地访问和修改私有成员变量
- **友元**：破坏封装性，允许外部代码访问私有成员，应谨慎使用

封装是面向对象编程的重要特性，它可以提高代码的安全性、可维护性和可扩展性。在设计类时，应遵循"最小权限原则"，只暴露必要的接口，隐藏内部实现细节。