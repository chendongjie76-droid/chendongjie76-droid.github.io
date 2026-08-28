---
title: "变量与数据类型"
date: 2026-08-28 21:00:00 +0800
categories: [Python, 基础]
tags: [Python, 基础]
excerpt: "Python 是动态类型语言，变量无需声明类型："
comments: true
---

# 变量与数据类型

## 变量

Python 是动态类型语言，变量无需声明类型：

```python
name = "Python"      # 字符串
age = 30              # 整数
price = 99.9          # 浮点数
is_valid = True       # 布尔值
```

### 命名规则

- 字母、数字、下划线组成，不能以数字开头
- 区分大小写
- 不能使用关键字（if, for, class 等）
- 推荐：小写字母 + 下划线（snake_case）

## 基本数据类型

| 类型 | 示例 | 说明 |
|------|------|------|
| int | `42`, `-10` | 整数，无大小限制 |
| float | `3.14`, `1.0` | 浮点数，双精度 |
| str | `"hello"`, `'world'` | 字符串，不可变 |
| bool | `True`, `False` | 布尔值 |
| NoneType | `None` | 空值 |

## 类型转换

```python
int("123")       # 123
str(456)         # "456"
float(10)        # 10.0
bool(0)          # False
bool("non-empty") # True
```

## 类型检查

```python
type(42)                    # <class 'int'>
isinstance(42, int)         # True
isinstance("a", (int, str)) # True（多个类型之一）
```
