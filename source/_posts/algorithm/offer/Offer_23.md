---
title: 23 二叉搜索树的后序遍历序列
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。
- 如果是则输出Yes,否则输出No。
- 假设输入的数组的任意两个数字都互不相同。
<!-- more -->

### 思路
- 满二叉树：从高到低，除了叶结点外，所有结点的左右结点都存在。
- 完全二叉树：比满二叉树少几个叶结点，从左向右放子结点。
- 平衡二叉树：空树或者它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树也都是平衡树。
- 二叉搜索树：空树或者二叉树的所有结点比它的左子结点大，比它的右子结点小。
- 前序：中左右 DLR
- 中序：左中右 LDR
- 后序：右左中 RLD
- 知道几个点之后，就会发现，二叉搜索树的后序遍历，最后一位是根节点。出去最后一位，剩下的节点可以分成两部分。
- 同理，两部分也满足二叉搜树的特征，递归方式，或者循环方式。
### Java 1.8

```
public class Solution {
    public boolean VerifySquenceOfBST(int [] sequence) {
        if(sequence.length==0){
            return false;
        }
        return Recursion(sequence,0,sequence.length-1);
    }
    
    public boolean Recursion(int [] sequence,int start,int root) {
        if(start>=root){
            return true;
        }
        int i = root;
        while(i>start&&sequence[i-1]>sequence[root]){
            i--;
        }
        for (int j = start; j < i-1; j++) {
            if(sequence[j]>sequence[root]){
                return false;
            }
        }
        return Recursion(sequence,start,i-1)&&Recursion(sequence,i,root-1);
    }
}
```