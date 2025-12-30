# C++ 继承与多态

## 1. 继承的概念

继承（Inheritance）是面向对象编程的三大特性之一，它允许创建新类（子类/派生类），继承现有类（父类/基类）的属性和方法，实现代码复用和扩展。

### 1.1 继承的优势

1. **代码复用**：子类可以继承父类的成员变量和成员函数，避免重复编写相同代码
2. **扩展性**：可以在父类基础上扩展新的功能
3. **层次结构**：建立类之间的层次关系，使代码结构更清晰
4. **多态基础**：为实现多态提供了基础

## 2. 继承的基本语法

### 2.1 继承的定义

**语法：**
```cpp
class 子类名 : 继承方式 父类名 {
    // 子类的成员
};
```

**继承方式：**
- `public`：公共继承
- `protected`：保护继承
- `private`：私有继承

### 2.2 公共继承（public）

公共继承是最常用的继承方式，它保持了父类成员的访问权限。

**访问权限变化：**
- 父类的`public`成员 → 子类的`public`成员
- 父类的`protected`成员 → 子类的`protected`成员
- 父类的`private`成员 → 子类不可访问（可通过父类的public/protected方法访问）

**示例：**
```cpp
class Animal {
public:
    Animal(const std::string& name) : m_name(name) {}
    
    void eat() {
        std::cout << m_name << " is eating." << std::endl;
    }
    
protected:
    std::string m_name;
};

// 公共继承
class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {}
    
    void bark() {
        std::cout << m_name << " is barking." << std::endl;
    }
};

int main() {
    Dog dog("旺财");
    dog.eat();  // 继承自Animal
    dog.bark();  // Dog自己的方法
    
    return 0;
}
```

### 2.3 保护继承（protected）

保护继承将父类的public和protected成员都变为子类的protected成员。

**访问权限变化：**
- 父类的`public`成员 → 子类的`protected`成员
- 父类的`protected`成员 → 子类的`protected`成员
- 父类的`private`成员 → 子类不可访问

### 2.4 私有继承（private）

私有继承将父类的public和protected成员都变为子类的private成员。

**访问权限变化：**
- 父类的`public`成员 → 子类的`private`成员
- 父类的`protected`成员 → 子类的`private`成员
- 父类的`private`成员 → 子类不可访问

## 3. 派生类的构造与析构

### 3.1 派生类的构造函数

派生类的构造函数需要初始化自己的成员变量和父类的成员变量。

**语法：**
```cpp
子类名(参数列表) : 父类名(父类构造参数), 子类成员变量1(初始值1), 子类成员变量2(初始值2), ... {
    // 子类构造函数体
}
```

**示例：**
```cpp
class Person {
public:
    Person(const std::string& name, int age) : m_name(name), m_age(age) {
        std::cout << "Person构造函数被调用" << std::endl;
    }
    
private:
    std::string m_name;
    int m_age;
};

class Student : public Person {
public:
    // 派生类构造函数：先调用父类构造函数，再初始化自己的成员
    Student(const std::string& name, int age, int studentId)
        : Person(name, age), m_studentId(studentId) {
        std::cout << "Student构造函数被调用" << std::endl;
    }
    
private:
    int m_studentId;
};
```

### 3.2 派生类的析构函数

派生类的析构函数会自动调用父类的析构函数，顺序与构造函数相反。

**调用顺序：**
1. 子类析构函数体
2. 子类成员变量析构
3. 父类析构函数体

**示例：**
```cpp
class Person {
public:
    ~Person() {
        std::cout << "Person析构函数被调用" << std::endl;
    }
};

class Student : public Person {
public:
    ~Student() {
        std::cout << "Student析构函数被调用" << std::endl;
    }
};

int main() {
    Student s;
    // 输出顺序：
    // Student析构函数被调用
    // Person析构函数被调用
    
    return 0;
}
```

## 4. 多态的概念

多态（Polymorphism）是面向对象编程的三大特性之一，它允许不同类的对象对同一消息做出不同响应。

### 4.1 多态的类型

1. **编译时多态**：通过函数重载和运算符重载实现，在编译时确定调用哪个函数
2. **运行时多态**：通过虚函数和继承实现，在运行时根据对象的实际类型确定调用哪个函数

## 5. 虚函数

虚函数（Virtual Function）是实现运行时多态的核心机制，它允许子类重写父类的方法。

### 5.1 虚函数的定义

在父类中使用`virtual`关键字声明的函数称为虚函数。

**语法：**
```cpp
class 父类名 {
public:
    virtual 返回类型 函数名(参数列表) {
        // 函数体
    }
};
```

### 5.2 虚函数的重写

子类可以重写父类的虚函数，使用相同的函数签名（函数名、参数列表、返回类型）。

**示例：**
```cpp
class Animal {
public:
    Animal(const std::string& name) : m_name(name) {}
    
    // 虚函数
    virtual void makeSound() const {
        std::cout << m_name << " makes a sound." << std::endl;
    }
    
protected:
    std::string m_name;
};

class Dog : public Animal {
public:
    Dog(const std::string& name) : Animal(name) {}
    
    // 重写父类的虚函数
    void makeSound() const override {
        std::cout << m_name << " barks." << std::endl;
    }
};

class Cat : public Animal {
public:
    Cat(const std::string& name) : Animal(name) {}
    
    // 重写父类的虚函数
    void makeSound() const override {
        std::cout << m_name << " meows." << std::endl;
    }
};
```

### 5.3 虚函数的调用

通过父类指针或引用调用虚函数时，会根据对象的实际类型调用相应的函数。

**示例：**
```cpp
int main() {
    Animal* animals[3];
    animals[0] = new Animal("Generic Animal");
    animals[1] = new Dog("旺财");
    animals[2] = new Cat("咪咪");
    
    // 多态调用：根据对象实际类型调用相应的makeSound方法
    for (int i = 0; i < 3; i++) {
        animals[i]->makeSound();
    }
    
    // 释放内存
    for (int i = 0; i < 3; i++) {
        delete animals[i];
    }
    
    return 0;
}
```

**输出：**
```
Generic Animal makes a sound.
旺财 barks.
咪咪 meows.
```

### 5.4 虚函数表（vtable）原理

虚函数的实现依赖于虚函数表（vtable）和虚指针（vptr）：

1. **虚函数表**：每个包含虚函数的类都有一个虚函数表，存储该类所有虚函数的地址
2. **虚指针**：每个对象都有一个虚指针，指向所属类的虚函数表
3. **调用过程**：当通过父类指针调用虚函数时，先通过虚指针找到虚函数表，再根据函数索引找到对应的函数地址，最后调用该函数

## 6. override 与 final 关键字（C++11）

### 6.1 override 关键字

`override`关键字用于显式标记子类重写了父类的虚函数，提高代码可读性和安全性。

**作用：**
- 确保子类确实重写了父类的虚函数
- 如果父类没有对应的虚函数，编译器会报错

**示例：**
```cpp
class Animal {
public:
    virtual void makeSound() const;
};

class Dog : public Animal {
public:
    // 显式标记重写
    void makeSound() const override;
    
    // 错误：父类没有名为eat的虚函数
    // void eat() const override;
};
```

### 6.2 final 关键字

`final`关键字用于禁止子类重写特定的虚函数，或禁止类被继承。

**用法：**
1. 禁止重写虚函数：在虚函数声明后加`final`
2. 禁止类被继承：在类名后加`final`

**示例：**
```cpp
class Animal {
public:
    // 禁止子类重写此虚函数
    virtual void makeSound() const final {
        std::cout << "Animal makes a sound." << std::endl;
    }
};

class Dog : public Animal {
public:
    // 错误：无法重写final虚函数
    // void makeSound() const override;
};

// 禁止被继承的类
class FinalClass final {
    // 类成员
};

// 错误：无法继承final类
// class SubClass : public FinalClass {
// };
```

## 7. 纯虚函数与抽象类

### 7.1 纯虚函数

纯虚函数是没有实现的虚函数，用于定义接口。

**语法：**
```cpp
class 类名 {
public:
    virtual 返回类型 函数名(参数列表) = 0;
};
```

### 7.2 抽象类

包含纯虚函数的类称为抽象类，它不能被实例化，只能作为基类使用。

**特点：**
- 不能创建对象
- 可以包含普通成员变量和成员函数
- 子类必须重写所有纯虚函数，否则子类也是抽象类

**示例：**
```cpp
// 抽象类
class Shape {
public:
    virtual ~Shape() {}  // 虚析构函数
    
    // 纯虚函数
    virtual double area() const = 0;
    virtual double perimeter() const = 0;
    virtual void display() const = 0;
};

// 具体类：实现了所有纯虚函数
class Rectangle : public Shape {
public:
    Rectangle(double width, double height) : m_width(width), m_height(height) {}
    
    double area() const override {
        return m_width * m_height;
    }
    
    double perimeter() const override {
        return 2 * (m_width + m_height);
    }
    
    void display() const override {
        std::cout << "矩形：宽度=" << m_width << ", 高度=" << m_height << std::endl;
    }
    
private:
    double m_width;
    double m_height;
};
```

## 8. 虚析构函数

虚析构函数是为了防止删除基类指针时子类资源泄漏。

### 8.1 为什么需要虚析构函数？

如果父类的析构函数不是虚函数，当通过父类指针删除子类对象时，只会调用父类的析构函数，子类的析构函数不会被调用，导致子类的资源泄漏。

**示例：**
```cpp
class Base {
public:
    Base() {
        m_data = new int[100];
    }
    
    // 非虚析构函数
    ~Base() {
        delete[] m_data;
        std::cout << "Base析构函数被调用" << std::endl;
    }
    
private:
    int* m_data;
};

class Derived : public Base {
public:
    Derived() {
        m_array = new double[100];
    }
    
    ~Derived() {
        delete[] m_array;
        std::cout << "Derived析构函数被调用" << std::endl;
    }
    
private:
    double* m_array;
};

int main() {
    Base* ptr = new Derived();
    delete ptr;  // 只调用Base析构函数，Derived析构函数不被调用，导致m_array泄漏
    
    return 0;
}
```

### 8.2 虚析构函数的定义

在父类的析构函数前加`virtual`关键字，即可将其声明为虚析构函数。

**示例：**
```cpp
class Base {
public:
    Base() {
        m_data = new int[100];
    }
    
    // 虚析构函数
    virtual ~Base() {
        delete[] m_data;
        std::cout << "Base析构函数被调用" << std::endl;
    }
    
private:
    int* m_data;
};

class Derived : public Base {
public:
    Derived() {
        m_array = new double[100];
    }
    
    ~Derived() {
        delete[] m_array;
        std::cout << "Derived析构函数被调用" << std::endl;
    }
    
private:
    double* m_array;
};

int main() {
    Base* ptr = new Derived();
    delete ptr;  // 先调用Derived析构函数，再调用Base析构函数，无泄漏
    
    return 0;
}
```

**输出：**
```
Derived析构函数被调用
Base析构函数被调用
```

## 9. 继承与多态的最佳实践

1. **优先使用公共继承**：保持接口的清晰性和一致性
2. **使用虚析构函数**：防止删除基类指针时子类资源泄漏
3. **使用 override 关键字**：显式标记重写，提高代码安全性
4. **使用抽象类定义接口**：实现代码解耦
5. **优先使用组合而非继承**：降低类之间的耦合度
6. **避免深度继承**：继承层次不宜过深，建议不超过3-4层

## 🎯 练习：Shape 抽象类实现

**任务：** 实现 `Shape` 抽象类（含纯虚函数 `area()`），派生出 `Circle` 和 `Rectangle`，用 `Shape*` 指针数组循环计算总面积。

**解决方案：**

```cpp
#include <iostream>
#include <cmath>

// 抽象类：Shape
class Shape {
public:
    // 虚析构函数
    virtual ~Shape() {}
    
    // 纯虚函数：计算面积
    virtual double area() const = 0;
    
    // 纯虚函数：显示形状信息
    virtual void display() const = 0;
};

// 具体类：Circle
class Circle : public Shape {
public:
    // 构造函数
    Circle(double radius) : m_radius(radius) {
        if (radius <= 0) {
            m_radius = 0;
        }
    }
    
    // 实现纯虚函数：计算圆的面积
    double area() const override {
        return M_PI * m_radius * m_radius;
    }
    
    // 实现纯虚函数：显示圆的信息
    void display() const override {
        std::cout << "圆形：半径=" << m_radius << std::endl;
    }
    
private:
    double m_radius;  // 半径
};

// 具体类：Rectangle
class Rectangle : public Shape {
public:
    // 构造函数
    Rectangle(double width, double height) : m_width(width), m_height(height) {
        if (width <= 0) m_width = 0;
        if (height <= 0) m_height = 0;
    }
    
    // 实现纯虚函数：计算矩形的面积
    double area() const override {
        return m_width * m_height;
    }
    
    // 实现纯虚函数：显示矩形的信息
    void display() const override {
        std::cout << "矩形：宽度=" << m_width << ", 高度=" << m_height << std::endl;
    }
    
private:
    double m_width;   // 宽度
    double m_height;  // 高度
};

int main() {
    // 创建形状数组
    const int num_shapes = 3;
    Shape* shapes[num_shapes];
    
    // 初始化形状数组
    shapes[0] = new Circle(5.0);
    shapes[1] = new Rectangle(4.0, 6.0);
    shapes[2] = new Circle(3.0);
    
    // 显示所有形状信息并计算总面积
    double total_area = 0.0;
    for (int i = 0; i < num_shapes; i++) {
        shapes[i]->display();
        double shape_area = shapes[i]->area();
        std::cout << "面积：" << shape_area << std::endl;
        total_area += shape_area;
        std::cout << "------------------------" << std::endl;
    }
    
    // 显示总面积
    std::cout << "所有形状的总面积：" << total_area << std::endl;
    
    // 释放内存
    for (int i = 0; i < num_shapes; i++) {
        delete shapes[i];
    }
    
    return 0;
}
```

**输出结果：**
```
圆形：半径=5
面积：78.5398
------------------------
矩形：宽度=4, 高度=6
面积：24
------------------------
圆形：半径=3
面积：28.2743
------------------------
所有形状的总面积：130.814
```

## 🎯 进阶练习：动物多态系统

**任务：** 设计一个动物多态系统，包含：
1. 抽象基类 `Animal`，包含纯虚函数 `makeSound()` 和 `move()`
2. 派生类 `Bird`、`Fish` 和 `Mammal`，分别实现基类的纯虚函数
3. `Mammal` 再派生出 `Dog` 和 `Cat`，重写 `makeSound()` 方法
4. 创建动物数组，演示多态行为

**解决方案：**

```cpp
#include <iostream>
#include <string>

// 抽象基类：Animal
class Animal {
public:
    Animal(const std::string& name) : m_name(name) {}
    
    virtual ~Animal() {}
    
    // 纯虚函数：发出声音
    virtual void makeSound() const = 0;
    
    // 纯虚函数：移动方式
    virtual void move() const = 0;
    
    // 普通成员函数：获取名称
    std::string getName() const {
        return m_name;
    }
    
protected:
    std::string m_name;  // 动物名称
};

// 派生类：Bird
class Bird : public Animal {
public:
    Bird(const std::string& name) : Animal(name) {}
    
    void makeSound() const override {
        std::cout << m_name << " 叽叽喳喳！" << std::endl;
    }
    
    void move() const override {
        std::cout << m_name << " 在天空中飞翔。" << std::endl;
    }
};

// 派生类：Fish
class Fish : public Animal {
public:
    Fish(const std::string& name) : Animal(name) {}
    
    void makeSound() const override {
        std::cout << m_name << " 咕嘟咕嘟！" << std::endl;
    }
    
    void move() const override {
        std::cout << m_name << " 在水中游泳。" << std::endl;
    }
};

// 派生类：Mammal
class Mammal : public Animal {
public:
    Mammal(const std::string& name) : Animal(name) {}
    
    // Mammal类的move方法实现
    void move() const override {
        std::cout << m_name << " 在陆地上行走。" << std::endl;
    }
};

// 派生类：Dog（继承自Mammal）
class Dog : public Mammal {
public:
    Dog(const std::string& name) : Mammal(name) {}
    
    void makeSound() const override {
        std::cout << m_name << " 汪汪汪！" << std::endl;
    }
};

// 派生类：Cat（继承自Mammal）
class Cat : public Mammal {
public:
    Cat(const std::string& name) : Mammal(name) {}
    
    void makeSound() const override {
        std::cout << m_name << " 喵喵喵！" << std::endl;
    }
};

int main() {
    // 创建动物数组
    const int num_animals = 5;
    Animal* animals[num_animals];
    
    // 初始化动物数组
    animals[0] = new Bird("麻雀");
    animals[1] = new Fish("金鱼");
    animals[2] = new Dog("旺财");
    animals[3] = new Cat("咪咪");
    animals[4] = new Mammal("大象");
    
    // 演示多态行为
    for (int i = 0; i < num_animals; i++) {
        std::cout << "------------------------" << std::endl;
        animals[i]->makeSound();
        animals[i]->move();
    }
    
    // 释放内存
    std::cout << "------------------------" << std::endl;
    for (int i = 0; i < num_animals; i++) {
        delete animals[i];
    }
    
    return 0;
}
```

**输出结果：**
```
------------------------
麻雀 叽叽喳喳！
麻雀 在天空中飞翔。
------------------------
金鱼 咕嘟咕嘟！
金鱼 在水中游泳。
------------------------
旺财 汪汪汪！
旺财 在陆地上行走。
------------------------
咪咪 喵喵喵！
咪咪 在陆地上行走。
------------------------
大象  在陆地上行走。
------------------------
```

## 总结

- **继承**：允许子类继承父类的成员，实现代码复用
- **继承方式**：public、protected、private，其中public最常用
- **多态**：允许不同类的对象对同一消息做出不同响应
- **虚函数**：实现运行时多态的核心机制，允许子类重写父类方法
- **override**：显式标记重写，提高代码安全性
- **final**：禁止重写或禁止继承
- **纯虚函数**：没有实现的虚函数，用于定义接口
- **抽象类**：包含纯虚函数的类，不能被实例化
- **虚析构函数**：防止删除基类指针时子类资源泄漏

继承与多态是C++面向对象编程的核心概念，它们使得代码更加灵活、可扩展和可维护。通过合理使用继承与多态，可以设计出更加优雅和高效的面向对象系统。