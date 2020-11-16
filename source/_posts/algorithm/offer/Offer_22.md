---
title: 22 从上往下打印二叉树
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 从上往下打印出二叉树的每个节点，同层节点从左至右打印。
<!-- more -->

### 思路
- 难点在于“同层节点从左至右打印”。中间的同层怎么合并。
- 想要获取下层集合，那么就要知道上层集合。
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

    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<>();
        if(root==null){
            return list;
        }
        ArrayList<TreeNode> up = new ArrayList<>();
        up.add(root);
        while(!up.isEmpty()){
            TreeNode temp = up.remove(0);
            if(temp.left!=null){
                up.add(temp.left);
            }
            if(temp.right!=null){
                up.add(temp.right);
            }
            list.add(temp.val);
            
        }
        return list;
    }
}
```