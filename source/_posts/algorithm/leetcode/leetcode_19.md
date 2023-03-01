---
title: leetcode19-删除链表的倒数第N个结点
date: 2023/3/1
tags: 
    - leetcode
---

# 题目描述

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```



**提示：**

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

# 题目思路

- 双指标

# Java
```java
import javax.swing.*;
import java.util.List;

/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode start = head;
        ListNode end = head;
        if (head.next == null && n == 1) {
            return null;
        }
        int i = 0;
        for (; i < n; i++) {
            if (end != null) {
                end = end.next;
            }
        }
        if (end == null) {
            if (n - i > 1) {
                return start;
            }
            return start.next;
        }
        while (end.next != null) {
            start = start.next;
            end = end.next;
        }
        start.next = start.next.next;
        return head;
    }
}
```