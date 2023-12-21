
在 C++ 中，你可以为用户自定义的类型（User-Defined Types）提供自定义的输入和输出操作，以便在标准输入输出流中使用。这通常涉及到在你的类型上重载输入运算符 `>>` 和输出运算符 `<<`

以下是一个简单的例子，演示了如何为自定义类型 `Person` 实现输入和输出运算符：

```cpp
#include <iostream>
#include <string>

class Person {
public:
    Person() = default;
    Person(const std::string& name, int age) : name(name), age(age) {}

    // 重载输入运算符
    friend std::istream& operator>>(std::istream& input, Person& person) {
        std::cout << "Enter name: ";
        input >> person.name;

        std::cout << "Enter age: ";
        input >> person.age;

        return input;
    }

    // 重载输出运算符
    friend std::ostream& operator<<(std::ostream& output, const Person& person) {
        output << "Name: " << person.name << ", Age: " << person.age;
        return output;
    }

private:
    std::string name;
    int age;
};

int main() {
    Person person;

    // 从标准输入流中读取用户输入
    std::cin >> person;

    // 输出到标准输出流
    std::cout << "You entered: " << person << std::endl;

    return 0;
}
```

在这个例子中，`Person` 类中重载了输入运算符 `>>` 和输出运算符 `<<`。`std::istream` 和 `std::ostream` 类分别表示输入流和输出流。`friend` 关键字使得这两个函数可以访问 `Person` 类的私有成员。

通过这种方式，你可以在标准输入输出流中以类似内置类型的方式使用你自定义的类型。当你输入数据时，`std::cin >> person;` 会调用重载的输入运算符，而 `std::cout << person;` 会调用重载的输出运算符

### 为什么返回值是std::ostream&

重载输出运算符 `<<` 的返回类型是 `std::ostream&`，这是为了支持连续的输出操作，即使用户在链式表达式中多次使用 `<<`。

具体来说，返回类型是 `std::ostream&` 的主要原因有两个：

1. **支持链式调用：** 在 C++ 中，输出运算符的惯用法是返回输出流对象的引用，以支持链式调用。这使得用户可以像下面这样一直串联多个输出操作：
```cpp
std::cout << "First output" << person << "Second output" << std::endl;
```
如果输出运算符返回的不是 `std::ostream&`，那么上述链式调用就不会生效

2. **允许检测输出是否成功：** 返回输出流对象的引用允许用户检测输出是否成功。在标准 C++ 惯例中，当输出成功时，`std::ostream` 对象会被转换为 `true`，否则转换为 `false`。因此，通过返回 `std::ostream&`，用户可以在链式调用中检测整个输出操作是否成功：
```cpp
if (std::cout << person) {
    std::cout << "Output successful" << std::endl;
} else {
    std::cout << "Output failed" << std::endl;
}
```

综上所述，返回类型为 `std::ostream&` 是符合 C++ 的输出运算符的一般惯例，支持链式调用，并允许检测输出是否成功


---
### friend

在 C++ 中，`friend` 关键字用于声明一个函数或类是当前类的友元（friend）。友元函数或友元类可以访问当前类的私有成员，即使这些成员在普通情况下是不可访问的。

**使用 `friend` 关键字的情况有两种：**

1. **友元函数：** 可以声明一个函数是当前类的友元，使得这个函数能够访问当前类的私有成员
```cpp
class MyClass {
private:
    int privateMember;

    // 友元函数声明
    friend void friendFunction(const MyClass& obj);

public:
    MyClass(int value) : privateMember(value) {}
};

// 友元函数定义
void friendFunction(const MyClass& obj) {
    std::cout << "Friend function can access private member: " << obj.privateMember << std::endl;
}
```

2. **友元类：** 可以声明一个类是当前类的友元，使得这个类的成员函数能够访问当前类的私有成员
```cpp
class FriendClass {
public:
    void printPrivateMember(const MyClass& obj) {
        std::cout << "Friend class can access private member: " << obj.privateMember << std::endl;
    }
};

class MyClass {
private:
    int privateMember;

    // 友元类声明
    friend class FriendClass;

public:
    MyClass(int value) : privateMember(value) {}
};
```

**需要注意的是：**

- 友元关系是单向的，即如果类 A 是类 B 的友元，不意味着类 B 也是类 A 的友元。
- 友元关系破坏了封装性，因此应当慎重使用。友元的存在通常是为了在一些特定情况下提供更灵活的访问权限，而不是推荐的面向对象设计方式。
- 尽量避免过度使用友元，因为过度使用可能导致代码的耦合性增加，降低代码的可维护性