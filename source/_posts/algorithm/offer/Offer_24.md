---
title: 24 二叉树中和为某一值的路径
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一颗二叉树的根节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。
- 路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。
- (注意: 在返回值的list中，数组长度大的数组靠前)
<!-- more -->

### 思路
- 递归遍历。
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
    private ArrayList<ArrayList<Integer>> listAll = new ArrayList<>();
    private ArrayList<Integer> list = new ArrayList<>();
    public ArrayList<ArrayList<Integer>> FindPath(TreeNode root,int target) {
        if(root == null){
            return listAll;
        }
        list.add(root.val);
        target -= root.val;
        if(target == 0 && root.left == null && root.right == null){
            listAll.add(new ArrayList<Integer>(list));
        }
        FindPath(root.left,target);
        FindPath(root.right,target);
        list.remove(list.size()-1);
        return listAll;
    }
}
```