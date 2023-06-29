---
title: leetcode110-二叉树的中序遍历
date: 2023/6/29
tags: 
    - leetcode
---

# 题目描述

给定一个二叉树的根节点 `root` ，返回 *它的 **中序** 遍历* 。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,3,2]
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

- 树中节点数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

# 题目思路

- 栈
- 树
- 深度优先搜索
- 二叉树

# Java
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> valList = new ArrayList<>();
        if(root == null){
            return valList;
        }
        valList.addAll(inorderTraversal(root.left));
        valList.add(root.val);
        valList.addAll(inorderTraversal(root.right));
        return valList;
    }
}
```
