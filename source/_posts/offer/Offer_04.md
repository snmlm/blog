---
title: 重建二叉树
categories: 剑指offer
tags: 
	- 算法
---
 <meta name="referrer" content="no-referrer" />

### 题目描述

* 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都`不含重复`的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
<!-- more -->

> * 前序遍历：
>   * 访问根节点 
>   * 前序遍历左子树 
>   * 前序遍历右子树
> * 中序遍历：
>   * 中序遍历左子树 
>   * 访问根节点 
>   * 中序遍历右子树
> * 后序遍历：
>   * 后序遍历左子树 
>   * 后序遍历右子树 
>   * 访问根节点

* 思路：
     1
   2   3
  4 5 6 8
 7

### Java 1.8
```
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        TreeNode root = reConstructBinaryTree(pre,0,pre.length-1,in,0,in.length-1);
        return root;
    }
    
    //前序遍历{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}
    public TreeNode reConstructBinaryTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn){
         if(startPre>endPre||startIn>endIn)
            return null;
        TreeNode root=new TreeNode(pre[startPre]);
         
        for(int i=startIn;i<=endIn;i++)
            if(in[i]==pre[startPre]){
                root.left=reConstructBinaryTree(pre,startPre+1,startPre+i-startIn,in,startIn,i-1);
                root.right=reConstructBinaryTree(pre,i-startIn+startPre+1,endPre,in,i+1,endIn);
            }
                 
        return root;
    }
}
```