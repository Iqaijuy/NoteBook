[[用户自定义类型IO]]
在 C++ 中，`get` 和 `getline` 是两个用于从输入流中读取字符串的函数，但它们有一些关键的区别
### get函数

`get` 函数用于从输入流中获取一行或特定数量的字符。其基本形式如下：
```cpp
istream& get(char* s, streamsize n, char delim = '\n');
```

- `s`：指向字符数组的指针，用于存储读取的字符序列。
- `n`：最多读取的字符数量。
- `delim`：可选参数，表示终止字符，默认为换行符 `\n`。

`get` 从输入流中读取字符，直到达到指定的字符数量 `n` 或者遇到终止字符 `delim`（如果指定）。读取的字符包括终止字符，但不会将终止字符存储到字符数组中

```cpp
#include <iostream>

int main() {
    char buffer[20];

    // 从标准输入流中获取一行，最多读取 19 个字符
    std::cin.get(buffer, 19);

    // 输出读取的字符串
    std::cout << "You entered: " << buffer << std::endl;

    return 0;
}
```

---
### getline函数

`getline` 函数用于从输入流中获取一行字符。其基本形式如下：
```cpp
istream& getline(char* s, streamsize n, char delim = '\n');
```

参数和用法与 `get` 类似，但有一个关键的区别：`getline` 会在读取到终止字符 `delim` 之后停止读取，并且不将终止字符存储到字符数组中

```cpp
#include <iostream>

int main() {
    char buffer[20];

    // 从标准输入流中获取一行，最多读取 19 个字符，遇到换行符停止
    std::cin.getline(buffer, 19);

    // 输出读取的字符串
    std::cout << "You entered: " << buffer << std::endl;

    return 0;
}
```

---
### 区别

1. **终止字符处理：**
    - `get`：终止字符被读取并存储在字符数组中。
    - `getline`：终止字符不被存储在字符数组中。
2. **停止条件：**
    - `get`：读取指定数量的字符或遇到终止字符。
    - `getline`：遇到终止字符（默认是换行符 `\n`）时停止读取。

根据具体的需求，选择使用 `get` 还是 `getline`，以便满足字符串读取的不同要求

