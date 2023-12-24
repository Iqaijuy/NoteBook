
Lambda 表达式是 C++11 引入的一项功能，允许在代码中定义匿名函数。Lambda 表达式的语法简洁，能够方便地在需要函数对象的地方进行使用。

Lambda 表达式的基本形式如下：

```cpp
[capture](parameters) -> return_type {
    // 函数体
}
```

其中：

- `capture` 是一个捕获列表，用于捕获外部变量。
- `parameters` 是参数列表，类似于函数的参数列表。
- `return_type` 是返回类型，用 `->` 指定。
- `{}` 内是函数体。

下面是一个简单的 Lambda 表达式的例子：

```cpp
#include <iostream>

int main() {
    // Lambda 表达式，无捕获，无参数
    auto sayHello = []() {
        std::cout << "Hello, Lambda!" << std::endl;
    };

    // 调用 Lambda 表达式
    sayHello();

    // Lambda 表达式，有捕获，有参数
    int x = 10;
    auto addX = [x](int value) -> int {
        return x + value;
    };

    // 调用 Lambda 表达式
    std::cout << "Result: " << addX(5) << std::endl;

    return 0;
}
```

在这个例子中，第一个 Lambda 表达式 `sayHello` 没有捕获任何外部变量，也没有参数，直接输出 "Hello, Lambda!"。第二个 Lambda 表达式 `addX` 捕获了外部变量 `x`，并接受一个参数，返回 `x + value` 的结果。

Lambda 表达式的使用使得在需要简单的函数对象时更加方便，避免了定义传统函数对象或函数指针的繁琐过程