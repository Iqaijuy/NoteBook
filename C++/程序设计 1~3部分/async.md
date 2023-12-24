
  
在C++中，`async` 是一个关键字，通常与 `std::future`、`std::promise`、`std::packaged_task` 和异步任务一起使用，用于支持异步编程。异步编程是一种并发编程的方式，可以在执行其他任务时等待长时间运行的操作完成，而无需阻塞整个程序

```cpp
#include <iostream>
#include <future>
#include <chrono>

// 异步任务函数
int add(int a, int b) {
    std::this_thread::sleep_for(std::chrono::seconds(3)); // 模拟耗时操作
    return a + b;
}

int main() {
    // 使用 async 启动异步任务
    std::future<int> result = std::async(add, 2, 3);

    // 执行其他任务
    std::cout << "Performing other tasks..." << std::endl;

    // 等待异步任务完成并获取结果
    int sum = result.get();

    std::cout << "Result: " << sum << std::endl;

    return 0;
}
```

在这个例子中，`std::async` 函数启动了一个异步任务，该任务是调用 `add` 函数计算两个数字的和。在 `main` 函数中，我们可以执行其他任务，而异步任务在后台执行。使用 `result.get()` 可以等待异步任务完成并获取结果。

值得注意的是，`std::async` 函数的默认策略是异步执行，但具体的执行策略可能依赖于实现。可以通过指定 `std::launch` 标志来明确指定执行策略。例如：
```cpp
std::future<int> result = std::async(std::launch::async, add, 2, 3);
```

此外，`std::async` 也可以使用 `std::launch::deferred` 标志，表示任务将在调用 `result.get()` 时同步执行，而不是在 `std::async` 调用时异步执行