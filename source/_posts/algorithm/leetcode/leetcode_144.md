---
title: leetcode144-二叉树的前序遍历
date: 2023/6/30
tags: 
    - leetcode
---

# 题目描述

给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,2,3]
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

**示例 4：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

```
输入：root = [1,2]
输出：[1,2]
```

**示例 5：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

```
输入：root = [1,null,2]
输出：[1,2]
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> valList = new ArrayList<>();
        if(root == null){
            return valList;
        }
        valList.add(root.val);
        valList.addAll(preorderTraversal(root.left));
        valList.addAll(preorderTraversal(root.right));
        return valList;
    }
}
```
