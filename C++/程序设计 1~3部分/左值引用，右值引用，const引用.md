
在 C++ 中，引用可以分为左值引用（lvalue reference）、右值引用（rvalue reference）和常量引用（const reference）。这些引用类型在使用时有不同的语法和语义

### 1. 左值引用（Lvalue Reference）:

左值引用主要用于引用左值（通常是具名变量），并且可以通过左值引用修改被引用的值

```cpp
#include <iostream>

int main() {
    int x = 42;

    // 左值引用
    int& lvalueRef = x;

    std::cout << "Original Value: " << x << std::endl;
    
    // 通过左值引用修改值
    lvalueRef = 55;

    std::cout << "Modified Value: " << x << std::endl;

    return 0;
}
```

### 2. 右值引用（Rvalue Reference）:

右值引用主要用于引用右值（通常是临时对象或表达式的结果），并且可以通过右值引用实现移动语义

```cpp
#include <iostream>

class MyObject {
public:
    MyObject() { std::cout << "Constructor" << std::endl; }
    ~MyObject() { std::cout << "Destructor" << std::endl; }
};

// 返回右值引用
MyObject&& createObject() {
    return MyObject();
}

int main() {
    // 右值引用
    MyObject&& rvalueRef = createObject();

    return 0;
}
```

### 3. 常量引用（Const Reference）:

常量引用用于引用对象，但不允许通过引用修改对象的值

```cpp
#include <iostream>

int main() {
    int x = 42;

    // 常量引用
    const int& constRef = x;

    std::cout << "Original Value: " << x << std::endl;
    
    // 编译错误，不能通过常量引用修改值
    // constRef = 55;

    return 0;
}
```

常量引用通常用于函数参数，以确保函数不会修改传递的参数。

这些引用类型在 C++ 中有着不同的用途，左值引用和常量引用常用于传递参数或返回值，而右值引用则更多地与移动语义和完美转发相关