
`decltype` 是C++11引入的关键字，用于获取表达式的类型。`decltype` 推断表达式的类型，并在编译时获得该类型，而不需要实际执行表达式

`decltype` 的基本语法如下：
```cpp
decltype(expression)
```

其中，`expression` 是一个表达式，`decltype` 返回该表达式的类型。

以下是一些使用 `decltype` 的示例：
```cpp
#include <iostream>

int main() {
    int x = 42;
    const double y = 3.14;

    // 使用 decltype 推断变量的类型
    decltype(x) a = x;        // a 的类型是 int
    decltype(x + y) b = x + y; // b 的类型是 double

    // 使用 decltype 推断函数返回值的类型
    auto add = [](int a, int b) -> decltype(a + b) {
        return a + b;
    };

    std::cout << "a: " << a << std::endl;
    std::cout << "b: " << b << std::endl;
    std::cout << "add(2, 3): " << add(2, 3) << std::endl;

    return 0;
}
```

在这个示例中，`decltype(x)` 推断出变量 `a` 的类型是 `int`，而 `decltype(x + y)` 推断出变量 `b` 的类型是 `double`。在 lambda 表达式中，`decltype(a + b)` 用于推断函数返回值的类型。

`decltype` 在泛型编程、模板元编程等场景中经常用于获取表达式的准确类型，提高代码的灵活性和可维护性
