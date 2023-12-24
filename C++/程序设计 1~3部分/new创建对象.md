
`new` 运算符用于在堆上动态分配内存，并返回指向分配内存的指针。你可以使用 `new` 运算符来创建对象，并得到指向该对象的指针。在这种情况下，对象的生存期由程序员负责，需要使用 `delete` 运算符手动释放分配的内存，以防止内存泄漏。

以下是一个简单的示例，演示如何使用 `new` 在堆上创建对象：

```cpp
#include <iostream>

class MyClass {
public:
    MyClass() {
        std::cout << "MyClass Constructor" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass Destructor" << std::endl;
    }

    void doSomething() {
        std::cout << "Doing something..." << std::endl;
    }
};

int main() {
    // 使用 new 在堆上创建 MyClass 对象
    MyClass* myObject = new MyClass();

    // 调用对象的成员函数
    myObject->doSomething();

    // 手动释放堆上分配的内存
    delete myObject;

    return 0;
}
```

在这个例子中，`new MyClass()` 返回一个指向 `MyClass` 对象的指针。该对象在堆上动态分配，而不是在栈上创建。在使用完对象后，需要使用 `delete` 运算符手动释放分配的内存。

值得注意的是，在现代 C++ 中，推荐使用智能指针（如 `std::unique_ptr` 或 `std::shared_ptr`）来管理动态分配的内存，以减少手动管理内存的复杂性和风险。智能指针可以提供自动的内存管理，减少内存泄漏和悬挂指针的风险

