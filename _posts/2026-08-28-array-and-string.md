---
title: "数组与字符串"
date: 2026-08-28 21:00:00 +0800
categories: [算法, 数据结构]
tags: [算法, 数据结构, 数组, 字符串]
comments: true
---

# 数组与字符串

## 核心要点

- 数组：连续内存，随机访问 O(1)，插入删除 O(n)
- 字符串：Python 中不可变，修改需生成新字符串

## 常用技巧

### 双指针

```python
# 两数之和（有序数组）
def two_sum(numbers, target):
    left, right = 0, len(numbers) - 1
    while left < right:
        s = numbers[left] + numbers[right]
        if s == target:
            return [left + 1, right + 1]
        elif s < target:
            left += 1
        else:
            right -= 1
```

### 滑动窗口

```python
# 最长无重复子串
def length_of_longest_substring(s):
    char_set = set()
    left = 0
    max_len = 0
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_len = max(max_len, right - left + 1)
    return max_len
```

### 前缀和

```python
# 子数组和等于 k
def subarray_sum(nums, k):
    prefix_sum = {0: 1}
    current = 0
    count = 0
    for num in nums:
        current += num
        count += prefix_sum.get(current - k, 0)
        prefix_sum[current] = prefix_sum.get(current, 0) + 1
    return count
```

## 常见题型

- 两数之和 / 三数之和
- 移动零 / 删除重复元素
- 最大子数组和
- 合并区间
- 旋转数组
- 字符串反转 / 回文判断
