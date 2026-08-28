---
title: "链表"
date: 2026-08-28 21:00:00 +0800
categories: [算法, 数据结构]
tags: [算法, 数据结构, 链表]
comments: true
---

# 链表

## 链表节点定义

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

## 核心操作

### 反转链表

```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    return prev
```

### 快慢指针

```python
# 找链表中点
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow

# 判断环
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

### 合并两个有序链表

```python
def merge_two_lists(l1, l2):
    dummy = ListNode()
    curr = dummy
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next
```

## 常用技巧

- **哑节点（dummy）**：处理头节点可能变化的情况，避免特殊判断
- **双指针**：快慢指针找环/中点，前后指针找倒数第 k 个
- **递归**：反转链表、合并链表等可用递归简洁实现
- **画图**：链表题建议画图理清指针指向

## 常见题型

- 反转链表（局部反转 / K 个一组反转）
- 环形链表（判断环 / 找环入口）
- 合并 K 个有序链表
- 相交链表
- 回文链表
- 删除链表倒数第 N 个节点
