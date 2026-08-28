---
title: "双指针"
date: 2026-08-28 21:00:00 +0800
categories: [算法, 算法思想]
tags: [算法, 算法思想, 双指针]
excerpt: "通过两个指针在数组/链表上移动，将 O(n²) 的暴力解法优化到 O(n)。"
comments: true
---

# 双指针

## 核心思想

通过两个指针在数组/链表上移动，将 O(n²) 的暴力解法优化到 O(n)。

## 常见类型

### 1. 对撞指针（左右指针）

两端向中间移动，适用于有序数组。

```python
def two_sum_sorted(numbers, target):
    left, right = 0, len(numbers) - 1
    while left < right:
        s = numbers[left] + numbers[right]
        if s == target:
            return [left, right]
        elif s < target:
            left += 1
        else:
            right -= 1
```

**适用场景**：两数之和、三数之和、回文判断、盛最多水的容器

### 2. 快慢指针

同方向不同速度，适用于链表和数组。

```python
# 移除有序数组重复项
def remove_duplicates(nums):
    if not nums:
        return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```

**适用场景**：链表找环/中点、数组去重、原地修改数组

### 3. 滑动窗口（快慢指针变体）

维护一个窗口，右指针扩大，左指针收缩。

```python
# 最小覆盖子串模板
def min_window(s, t):
    from collections import Counter
    need = Counter(t)
    missing = len(t)
    left = start = end = 0
    for right, char in enumerate(s, 1):
        if need[char] > 0:
            missing -= 1
        need[char] -= 1
        if missing == 0:
            while left < right and need[s[left]] < 0:
                need[s[left]] += 1
                left += 1
            if end == 0 or right - left <= end - start:
                start, end = left, right
            need[s[left]] += 1
            missing += 1
            left += 1
    return s[start:end]
```

**适用场景**：最长/最短子串、子数组、固定窗口大小问题

## 解题模板

1. 初始化指针位置（left=0, right=0 或两端）
2. 确定移动条件（什么时候移动左/右指针）
3. 在移动过程中更新答案
4. 确定终止条件
