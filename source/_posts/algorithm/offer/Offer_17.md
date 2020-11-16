---
title: 17 树的子结构
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）。
<!-- more -->

### 思路
- 难点在于树的整体怎么判断，左右子树的遍历也要去比较。
### Java 1.8

```
public class Solution {
    public class TreeNode {
        int val = 0;
        TreeNode left = null;
        TreeNode right = null;
        public TreeNode(int val) {
            this.val = val;

        }
    }
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        if(root1 == null || root2==null){
            return false;
        }
        if(compareTree(root1,root2))
            return true;
        if(root1.left!=null){
            return HasSubtree(root1.left,root2);
        }
        if(root1.right!=null){
            return HasSubtree(root1.right,root2);
        }
        return false;
    }
    public boolean compareTree(TreeNode root1,TreeNode root2) {
        if(root1.val == root2.val){
            if(root2.left!=null){
                if(root1.left!= null){
                    if(!compareTree(root1.left,root2.left)){
                        return false;
                    }
                }else{
                    return false;
                }
            }
            if(root2.right!=null){
                if(root1.right!= null){
                    if(!compareTree(root1.right,root2.right)){
                        return false;
                    }
                }else{
                    return false;
                }
            }
            return true;
        }
        return false;
    }
}
```
