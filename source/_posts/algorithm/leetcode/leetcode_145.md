---
title: leetcode144-二叉树的后序遍历
date: 2023/6/30
tags: 
    - leetcode
---

# 题目描述

给你一棵二叉树的根节点 `root` ，返回其节点值的 **后序遍历** 。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg)

```
输入：root = [1,null,2,3]
输出：[3,2,1]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [1]
输出：[1]
```



**提示：**

- 树中节点的数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

# 题目思路

- 栈
- 树
- 深度优先搜索
- 二叉树

# Java
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> valList = new ArrayList<>();
        if(root == null){
            return valList;
        }
        valList.addAll(postorderTraversal(root.left));
        valList.addAll(postorderTraversal(root.right));
        valList.add(root.val);
        return valList;
    }
}
```
