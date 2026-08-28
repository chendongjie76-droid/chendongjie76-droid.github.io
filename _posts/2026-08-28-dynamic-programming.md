---
title: "动态规划"
date: 2026-08-28 21:00:00 +0800
categories: [算法, 算法思想]
tags: [算法, 算法思想, 动态规划]
excerpt: "将复杂问题分解为子问题，存储子问题的解避免重复计算。"
comments: true
---

# 动态规划

## 核心思想

将复杂问题分解为子问题，存储子问题的解避免重复计算。

## 解题步骤

1. **定义状态**：dp[i] 或 dp[i][j] 表示什么
2. **状态转移方程**：当前状态如何由之前的状态得到
3. **初始条件**：dp[0]、dp[0][0] 等边界值
4. **遍历顺序**：确保计算当前状态时所需状态已计算
5. **返回结果**：dp[n] 或 dp[m][n] 等

## 经典题型

### 1. 爬楼梯（一维 DP）

```python
def climb_stairs(n):
    if n <= 2:
        return n
    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2
    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# 空间优化
def climb_stairs_o1(n):
    if n <= 2:
        return n
    prev2, prev1 = 1, 2
    for _ in range(3, n + 1):
        prev2, prev1 = prev1, prev1 + prev2
    return prev1
```

### 2. 最长递增子序列（LIS）

```python
def length_of_lis(nums):
    if not nums:
        return 0
    dp = [1] * len(nums)
    for i in range(len(nums)):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)
```

### 3. 0-1 背包（二维 DP）

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    for i in range(1, n + 1):
        for w in range(capacity + 1):
            dp[i][w] = dp[i-1][w]  # 不选第 i 个物品
            if w >= weights[i-1]:   # 选第 i 个物品
                dp[i][w] = max(dp[i][w], dp[i-1][w-weights[i-1]] + values[i-1])
    return dp[n][capacity]
```

### 4. 编辑距离

```python
def min_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j],    # 删除
                                    dp[i][j-1],    # 插入
                                    dp[i-1][j-1])  # 替换
    return dp[m][n]
```

## DP 分类

| 类型 | 特点 | 例题 |
|------|------|------|
| 线性 DP | 一维状态转移 | 爬楼梯、打家劫舍 |
| 区间 DP | dp[i][j] 表示区间 | 最长回文子串、矩阵链乘 |
| 背包 DP | 物品+容量二维 | 0-1 背包、完全背包 |
| 树形 DP | 在树上做 DP | 二叉树最大路径和 |
| 状态压缩 DP | 用 bitmask 表示状态 | 旅行商问题、棋盘问题 |

## 优化技巧

- **空间优化**：只依赖前一行/前一个状态时，用滚动数组
- **二分优化**：LIS 可用贪心+二分降到 O(n log n)
- **单调队列优化**：滑动窗口最大值类 DP
