
  
Lambda 表达式的捕获列表（capture list）用于指定在 Lambda 函数体中访问的外部变量。捕获列表允许你在 Lambda 表达式中使用在 Lambda 表达式外部定义的变量。

Lambda 捕获列表有两种基本形式：按值捕获和按引用捕获。

### 按值捕获：

```cpp
#include <iostream>

int main() {
    int x = 42;

    // 使用按值捕获列表，捕获 x
    auto lambda = [x]() {
        std::cout << "Captured value: " << x << std::endl;
    };

    // 调用 Lambda 表达式
    lambda();

    return 0;
}
```

在这个例子中，Lambda 表达式 `[x]() {...}` 按值捕获了变量 `x`。Lambda 表达式中的 `x` 将会拷贝自外部的 `x`。如果在 Lambda 表达式内修改 `x` 的值，不会影响外部的 `x`。

### 按引用捕获：

```cpp
#include <iostream>

int main() {
    int x = 42;

    // 使用按引用捕获列表，捕获 x
    auto lambda = [&x]() {
        std::cout << "Captured by reference: " << x << std::endl;
    };

    // 调用 Lambda 表达式
    lambda();

    return 0;
}
```

在这个例子中，Lambda 表达式 `[&x]() {...}` 按引用捕获了变量 `x`。Lambda 表达式中的 `x` 是对外部 `x` 的引用，因此在 Lambda 表达式中修改 `x` 的值会影响到外部的 `x`。

需要注意的是，按引用捕获可能导致悬垂引用（dangling reference）的问题，尤其在 Lambda 表达式的生命周期超过了捕获变量的生命周期时。为了避免这个问题，可以使用 `std::ref` 或 `std::cref` 进行引用封装，或者选择按值捕获