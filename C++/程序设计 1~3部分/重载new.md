
在 C++ 中，可以重载 `new` 和 `delete` 运算符以自定义内存的分配和释放行为。这对于特殊需求、性能优化或者对内存管理的更多控制是有用的。重载 `new` 运算符通常是与 `delete` 运算符一起使用的。

下面是一个简单的例子，演示如何重载 `new` 和 `delete` 运算符：

```cpp
#include <iostream>
#include <cstdlib>

// 重载 new 运算符
void* operator new(std::size_t size) {
    std::cout << "Custom new called, size: " << size << " bytes" << std::endl;
    void* ptr = std::malloc(size);
    return ptr;
}

// 重载 delete 运算符
void operator delete(void* ptr) noexcept {
    std::cout << "Custom delete called" << std::endl;
    std::free(ptr);
}

class MyClass {
public:
    MyClass() {
        std::cout << "MyClass Constructor" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass Destructor" << std::endl;
    }
};

int main() {
    // 使用重载的 new 运算符分配内存
    MyClass* obj = new MyClass();

    // 使用重载的 delete 运算符释放内存
    delete obj;

    return 0;
}
```

在这个例子中，`operator new` 和 `operator delete` 被重载以自定义内存的分配和释放行为。`operator new` 用于分配内存，而 `operator delete` 用于释放内存。在 `main` 函数中，通过 `new` 运算符分配了一个 `MyClass` 对象，然后通过 `delete` 运算符释放了内存。

需要注意的是，如果你重载了 `new` 和 `delete` 运算符，通常也需要同时重载 `new[]` 和 `delete[]` 运算符，以处理数组的内存分配和释放。此外，确保重载运算符的实现是线程安全的，尽量避免内存泄漏和悬挂指针等问题