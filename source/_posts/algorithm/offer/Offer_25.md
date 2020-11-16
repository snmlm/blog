---
title: 25 复杂链表的复制
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），
- 返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）
<!-- more -->

### 思路
- 此解需理解成单链表，random指向的是链表中的某个节点。
- 如果想复杂的话，环形链表，图就不好解了，我是没想出来。
- 开始是想麻烦了，单链表就比较简单了，单点在于random的指向问题。
- a节点复制为a1，插入到a之后。
- 再次遍历，random节点，指向random.next。
- 删除原节点。
- 这个是最坑的（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）
### Java 1.8

```
public class Solution {
    public class RandomListNode {
        int label;
        RandomListNode next = null;
        RandomListNode random = null;
        RandomListNode(int label) {
            this.label = label;
        }
    }

    public RandomListNode Clone(RandomListNode pHead){
        if(pHead==null){
            return null;
        }
        RandomListNode newPHead = pHead;
        while(newPHead!=null){
            RandomListNode newNode = new RandomListNode(newPHead.label);
            RandomListNode temp  = newPHead.next;
            newPHead.next = newNode;
            newNode.next = temp;
            newPHead = newNode.next;
        }
        newPHead = pHead;
        while(newPHead!=null){
            newPHead.next.random = newPHead.random==null?null:newPHead.random.next;
            newPHead = newPHead.next.next;
        }
        newPHead = pHead;
        RandomListNode result = pHead.next;
        while(newPHead.next!=null){
            RandomListNode cloneNode = newPHead.next;
            newPHead.next = cloneNode.next;
            newPHead = cloneNode;
        }
        return result;
    }
}
```