
  
Lambda 表达式是C++11引入的一种新特性，允许你在代码中定义匿名函数。Lambda 表达式的语法形式如下：

```cpp
[capture](parameters) -> return_type {
    // 函数体
}
```

其中：

- `capture`：捕获列表，用于捕获外部变量，可以是空，或者包含一个或多个外部变量。
- `parameters`：参数列表，与普通函数的参数列表类似。
- `return_type`：返回类型，可以省略，编译器可以自动推导。
- `{}`：函数体，与普通函数一样。

以下是一些 Lambda 表达式的示例：

```cpp
#include <iostream>

int main() {
    // 示例1：不捕获任何变量
    auto func1 = []() {
        std::cout << "Hello, Lambda!" << std::endl;
    };
    func1();  // 调用 Lambda 函数

    // 示例2：捕获外部变量
    int x = 10;
    auto func2 = [x]() {
        std::cout << "Value of x: " << x << std::endl;
    };
    func2();  // 调用 Lambda 函数

    // 示例3：带参数和返回值的 Lambda
    auto add = [](int a, int b) -> int {
        return a + b;
    };
    std::cout << "Sum: " << add(5, 7) << std::endl;

    return 0;
}
```

Lambda 表达式的特点是可以在需要的地方直接定义函数，而不需要专门为一些简单的任务编写独立的函数。在某些情况下，Lambda 表达式可以使代码更为简洁和可读

