---
title: "装饰器详解"
date: 2026-08-28 21:00:00 +0800
categories: [Python, 进阶]
tags: [Python, 进阶, 装饰器]
excerpt: "装饰器是一种修改函数或类行为的语法糖，本质是「接收函数并返回函数」的高阶函数。"
comments: true
---

# 装饰器详解

## 什么是装饰器

装饰器是一种修改函数或类行为的语法糖，本质是「接收函数并返回函数」的高阶函数。

```python
def simple_decorator(func):
    def wrapper():
        print("函数执行前")
        func()
        print("函数执行后")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello!")

say_hello()
# 输出:
# 函数执行前
# Hello!
# 函数执行后
```

## 带参数的装饰器

```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(times=3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # 输出 3 次
```

## 保留原函数元信息

使用 `functools.wraps` 保留函数名、文档字符串等：

```python
import functools

def decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

## 常见应用场景

1. **日志记录**：自动记录函数调用和执行时间
2. **权限校验**：登录验证、角色检查
3. **缓存**：`@lru_cache` 记忆化计算结果
4. **重试机制**：失败自动重试
5. **计时**：统计函数执行耗时

### 示例：计时装饰器

```python
import time
import functools

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} 耗时: {end - start:.4f}s")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
```

## 类装饰器

通过实现 `__call__` 方法将类作为装饰器：

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0

    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"调用次数: {self.count}")
        return self.func(*args, **kwargs)

@CountCalls
def say_hi():
    print("Hi!")
```
