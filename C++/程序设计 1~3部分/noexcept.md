[[右值引用]]
`noexcept` 是C++11引入的关键字，用于指示函数是否可能引发异常。它可以用来标记函数是否会抛出异常，并且可以帮助编译器进行一些优化

`noexcept` 关键字有两种用法：

1. **指定函数不会抛出异常**：
- 如果在函数声明或定义的末尾使用 `noexcept` 关键字且不跟随任何条件，表示该函数不会引发任何异常
```cpp
void myFunction() noexcept {
    // 函数体不会抛出异常
}
```

2. **指定函数可能会抛出异常**：
- 如果不使用 `noexcept` 关键字或使用 `noexcept(expression)` 指定了条件，表示函数可能会引发异常。例如，使用了可能会抛出异常的操作，那么函数就可能引发异常
```cpp
void myFunction() noexcept(false) {
    // 可能会抛出异常
}

void anotherFunction() noexcept(sizeof(int) > 4) {
    // 可能会抛出异常，取决于条件
}
```

`noexcept` 的使用有助于编译器进行一些优化，尤其是在涉及异常处理的情况下。如果声明了 `noexcept`，并且程序在 `noexcept` 函数中抛出了异常，程序将会调用 `std::terminate()` 终止。

需要注意的是，使用 `noexcept` 应谨慎。对于确保不会抛出异常的函数，使用 `noexcept` 可以提高代码的可靠性和性能。但是在一些情况下，错误地标记函数为 `noexcept` 可能导致程序的不确定行为