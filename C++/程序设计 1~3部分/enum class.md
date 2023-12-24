
`enum class` 是 C++11 引入的一种枚举类型的新形式，也称为枚举类。相比传统的枚举类型，`enum class` 提供了更加严格的作用域和类型安全。

以下是 `enum class` 的基本用法：

```cpp
#include <iostream>

// 定义一个枚举类
enum class Color {
    Red,
    Green,
    Blue
};

int main() {
    // 声明一个枚举类变量
    Color myColor = Color::Green;

    // 使用枚举类变量
    switch (myColor) {
        case Color::Red:
            std::cout << "The color is Red." << std::endl;
            break;
        case Color::Green:
            std::cout << "The color is Green." << std::endl;
            break;
        case Color::Blue:
            std::cout << "The color is Blue." << std::endl;
            break;
    }

    return 0;
}
```

`enum class` 的主要特点包括：

1. **作用域限制：** 枚举类的成员在枚举类的作用域内，不会污染全局命名空间
2. **类型安全：** 枚举类的类型是显式指定的，不会隐式转换为整数类型。这可以避免一些潜在的错误
3. **前置声明：** 在使用 `enum class` 时，不需要提前声明枚举成员，可以在需要的地方直接使用

```cpp
enum class Status;  // 不需要提前声明枚举成员

// 使用枚举类
Status myStatus = Status::OK;
```

4. **底层类型：** 可以指定底层类型（enum underlying type），使得枚举类的大小和性能更可控
```cpp
enum class Status : std::uint8_t {
    OK,
    Error,
    Warning
};
```

使用 `enum class` 可以提高代码的可读性和安全性，特别是在大型项目中，避免了传统枚举类型可能引起的潜在问题