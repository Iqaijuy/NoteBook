` =delete ` 是C++11引入的一种用法，用于显式删除某个函数或特定的函数重载。它的作用是告诉编译器不允许使用被删除的函数。

这主要用于以下情况：

1. **阻止使用默认生成的函数**：
- 当你希望禁止某个特定的函数被默认生成时，可以使用 ` =delete `。例如，阻止默认生成的拷贝构造函数和赋值运算符：
```cpp
class NoCopy {
public:
    // 显式删除拷贝构造函数和赋值运算符
    NoCopy(const NoCopy&) = delete;
    NoCopy& operator=(const NoCopy&) = delete;
};
```

2. **禁止某些函数的使用**：
- 在某些情况下，你可能不希望类的对象被复制或移动。通过将拷贝构造函数和移动构造函数删除，可以防止对象的复制和移动
```cpp
class NoCopyOrMove {
public:
    // 显式删除拷贝构造函数和移动构造函数
    NoCopyOrMove(const NoCopyOrMove&) = delete;
    NoCopyOrMove(NoCopyOrMove&&) = delete;
};
```

3. **禁止某个函数的特定重载**：
- 有时，你可能希望在类中某个函数的特定重载上使用 ` =delete `。这通常用于防止不希望的类型转换或特定参数的调用
```cpp
class MyClass {
public:
    void process(int value);

    // 显式删除对 process 函数的某个特定重载的调用
    void process(double) = delete;
};
```

使用 ` =delete ` 的关键点在于，它提供了一种更明确、更安全的方式来指定某些函数不可用，从而避免了一些可能导致问题的隐式操作

---
当一个被标记成=delete的函数被子类继承并重写时，子类的该函数是否有效

  
当一个基类的函数被标记为 ` =delete `（删除）时，它表明该函数在基类中是被显式禁止的，不可使用的。在这种情况下，子类不会继承该函数的删除状态。子类可以选择重写该函数，但在这种情况下，子类的该函数并不是继承了基类的 ` =delete ` 特性，而是成为了一个正常的可用函数。

考虑以下示例：
```cpp
class Base {
public:
    void foo() = delete;
};

class Derived : public Base {
public:
    // 尝试重写被删除的函数
    void foo() {
        // 实现子类的版本
    }
};

int main() {
    Derived derivedObj;
    // 调用子类的 foo 函数
    derivedObj.foo();
    
    return 0;
}
```

在这个例子中，基类 `Base` 中的 `foo` 函数被标记为 `=delete`。然而，子类 `Derived` 可以尝试重新定义 `foo` 函数。这样做不会导致编译错误，因为子类的函数并不继承基类函数的 `=delete` 特性，而是成为了一个新的函数。

需要注意的是，子类重写的函数并不是基类被删除函数的同一版本，而是一个全新的函数。在使用继承和重写时，程序员需要注意继承关系和函数重写的语义，以确保程序行为的正确性

---
在父类使用=delete函数会发生什么事情，是否允许该函数执行

在父类中使用 ` =delete ` 标记一个函数，意味着在该类中禁止使用该函数。如果在父类中的某个函数被标记为 `=delete`，那么在父类的对象上调用该函数将导致编译错误。

考虑以下示例：
```cpp
class Parent {
public:
    // 使用 =delete 标记函数
    void foo() = delete;
};

int main() {
    Parent parentObj;

    // 尝试调用被标记为 =delete 的函数
    parentObj.foo();  // 编译错误

    return 0;
}
```

在这个例子中，`Parent` 类中的 `foo` 函数被标记为 ` =delete `，因此在 `main` 函数中尝试调用 `foo` 函数将导致编译错误。

` =delete ` 的主要用途之一是在设计接口时明确禁用某些函数。这可以帮助防止一些可能导致问题的操作，或者明确表示某些函数不应该被调用。

需要注意的是，子类可以尝试重新定义（override）被父类 ` =delete ` 的函数。在这种情况下，子类的版本并不继承父类函数的 ` =delete ` 特性，而是成为一个新的函数。这样的设计可能会引起一些意外行为，因此在使用 `=delete` 时，应谨慎考虑其影响

---
