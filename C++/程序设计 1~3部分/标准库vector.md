
`std::vector` 是 C++ 标准库中提供的一个动态数组容器，它可以在运行时动态调整大小。`std::vector` 提供了一系列的方法来方便地管理和操作数组

以下是一个简单的示例演示如何使用 `std::vector`：
```cpp
#include <iostream>
#include <vector>

int main() {
    // 声明一个存储整数的 vector
    std::vector<int> myVector;

    // 添加元素到 vector
    myVector.push_back(1);
    myVector.push_back(2);
    myVector.push_back(3);

    // 遍历 vector 中的元素
    std::cout << "Elements in myVector: ";
    for (int value : myVector) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    // 使用下标访问 vector 中的元素
    std::cout << "Element at index 1: " << myVector[1] << std::endl;

    // 获取 vector 的大小
    std::cout << "Size of myVector: " << myVector.size() << std::endl;

    return 0;
}
```

在这个例子中，`std::vector<int>` 创建了一个存储整数的 vector，然后使用 `push_back` 方法添加了一些元素。通过使用范围-based for 循环和下标运算符，可以遍历和访问 vector 中的元素。`size()` 方法返回 vector 的大小。

`std::vector` 具有动态调整大小的能力，可以方便地适应不同的需求，是 C++ 中常用的容器之一

---
#### std::array

`std::array` 是 C++ 标准库提供的另一个数组容器，相较于 `std::vector`，`std::array` 具有固定大小，大小在编译时确定。它提供了数组的基本功能，同时具备一些容器的特性，例如可以使用范围-based for 循环、可以通过 `at()` 方法进行边界检查等。

以下是一个简单的示例演示如何使用 `std::array`：

```cpp
#include <iostream>
#include <array>

int main() {
    // 声明一个包含5个整数的 std::array
    std::array<int, 5> myArray = {1, 2, 3, 4, 5};

    // 使用范围-based for 循环遍历数组
    std::cout << "Elements in myArray: ";
    for (int value : myArray) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    // 使用 at() 方法进行边界检查
    try {
        int element = myArray.at(2);
        std::cout << "Element at index 2: " << element << std::endl;
    } catch (const std::out_of_range& e) {
        std::cerr << "Exception: " << e.what() << std::endl;
    }

    // 获取数组的大小
    std::cout << "Size of myArray: " << myArray.size() << std::endl;

    return 0;
}
```

在这个例子中，`std::array<int, 5>` 创建了一个包含5个整数的 `std::array`，通过初始化列表赋值了一些元素。可以使用范围-based for 循环遍历数组，也可以使用 `at()` 方法进行边界检查。

`std::array` 是一个在编译时确定大小的数组容器，提供了一些安全和方便的操作方法

