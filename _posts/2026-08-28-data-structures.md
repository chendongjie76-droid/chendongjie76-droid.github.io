---
title: "数据结构"
date: 2026-08-28 21:00:00 +0800
categories: [Python, 基础]
tags: [Python, 基础]
excerpt: "键值对集合，键必须不可变。"
comments: true
---

# 数据结构

## 列表 list

有序、可变序列。

```python
nums = [1, 2, 3, 4, 5]

# 常用操作
nums.append(6)       # 末尾添加
nums.insert(0, 0)    # 指定位置插入
nums.remove(3)        # 删除第一个匹配项
nums.pop()            # 弹出末尾元素
nums.index(2)         # 查找元素索引
nums.count(1)         # 统计出现次数
nums.sort()           # 原地排序
nums.reverse()        # 原地反转

# 切片
nums[1:3]    # [2, 3] （左闭右开）
nums[:3]     # [1, 2, 3]
nums[::2]    # [1, 3, 5] 步长为2
nums[::-1]   # 反转列表
```

## 字典 dict

键值对集合，键必须不可变。

```python
person = {"name": "Alice", "age": 25}

# 访问
person["name"]           # "Alice"
person.get("email", "N/A")  # 安全访问，带默认值

# 修改/添加
person["age"] = 26
person["email"] = "a@b.com"

# 常用方法
person.keys()     # 所有键
person.values()   # 所有值
person.items()    # 所有键值对
person.pop("age") # 删除并返回值
```

## 元组 tuple

有序、不可变序列。

```python
point = (3, 4)
x, y = point        # 解包
single = (1,)       # 单元素元组必须带逗号
```

## 集合 set

无序、不重复元素集合。

```python
s = {1, 2, 3, 3}   # {1, 2, 3} 自动去重

s.add(4)
s.remove(1)
s.union({3, 4, 5})     # 并集
s.intersection({2, 3})  # 交集
s.difference({2})       # 差集
```

## 选择建议

| 需求 | 推荐结构 |
|------|---------|
| 有序序列，需修改 | list |
| 有序序列，不可变 | tuple |
| 键值映射 | dict |
| 去重 / 集合运算 | set |
