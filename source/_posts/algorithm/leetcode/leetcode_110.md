---
title: leetcode110-平衡二叉树
date: 2023/6/29
tags: 
    - leetcode
---

# 题目描述

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

```
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

**示例 3：**

```
输入：root = []
输出：true
```



**提示：**

- 树中的节点数在范围 `[0, 5000]` 内
- `-104 <= Node.val <= 104`

# 题目思路

- 树
- 深度优先搜索
- 二叉树

# Java
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (maxDepth(root) == -1) {
            return false;
        }
        return true;
    }

    // 返回的是高度差，-1的情况是高度差大于1的
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        if (left == -1 || right == -1 || left - right > 1 || right - left > 1) {
            return -1;
        }
        if (left > right) {
            return left + 1;
        }
        return right + 1;
    }
}
```
