---
title: leetcode104-二叉树的最大深度
date: 2023/6/28  
tags: 
    - leetcode
---

# 题目描述

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

# 题目思路

- 树
- 深度优先搜索
- 广度优先搜索
- 二叉树

# Java
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        if(left > right){
            return left + 1;
        }
        return right + 1;
    }
}
```
