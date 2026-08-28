---
title: "生成器与迭代器"
date: 2026-08-28 21:00:00 +0800
categories: [Python, 进阶]
tags: [Python, 进阶, 生成器, 迭代器]
excerpt: "实现了 iter() 和 next() 方法的对象。"
comments: true
---

# 生成器与迭代器

## 迭代器 Iterator

实现了 `__iter__()` 和 `__next__()` 方法的对象。

```python
class CountDown:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1

for num in CountDown(3):
    print(num)  # 3, 2, 1
```

## 生成器 Generator

使用 `yield` 关键字的函数，返回生成器对象，惰性求值。

```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

for num in fibonacci(10):
    print(num)
```

### 生成器表达式

```python
# 列表推导式（立即计算，占用内存）
squares_list = [x**2 for x in range(1000000)]

# 生成器表达式（惰性计算，省内存）
squares_gen = (x**2 for x in range(1000000))
```

## yield from

委托给子生成器：

```python
def flatten(nested):
    for sublist in nested:
        yield from sublist

list(flatten([[1, 2], [3, 4], [5]]))  # [1, 2, 3, 4, 5]
```

## 生成器的优势

1. **内存高效**：按需生成，不一次性加载所有数据
2. **惰性求值**：只在需要时计算
3. **表示无限序列**：如无限斐波那契数列
4. **管道式处理**：多个生成器串联处理数据流

```python
# 管道示例：读取大文件 → 过滤 → 处理
def read_lines(filename):
    with open(filename) as f:
        for line in f:
            yield line.strip()

def filter_non_empty(lines):
    return (line for line in lines if line)

def uppercase(lines):
    return (line.upper() for line in lines)

# 串联使用，内存占用恒定
lines = read_lines("big_file.txt")
lines = filter_non_empty(lines)
lines = uppercase(lines)
for line in lines:
    print(line)
```
