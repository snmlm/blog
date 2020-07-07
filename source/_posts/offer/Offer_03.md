---
title: 从尾到头打印链表
categories: 剑指offer
tags: 
	- 算法
---
 <meta name="referrer" content="no-referrer" />

### 题目描述

* 输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。
<!-- more -->
* 思路：
* 正常思路：利用递归，循环到最后，进行插入
* C++ vector的特性，可以插入特定位置
* java arraylist有Collections工具类，可以直接插入，然后反转

### C++ 11

```
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> vr;
        if (head != NULL){
            vr.insert(vr.begin(), head->val);
			while (head->next != NULL){
                head = head->next;
				vr.insert(vr.begin(), head->val);
			}
		}
        return vr;
    }
};
```

### Java 1.8

```
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
public class Solution {
    ArrayList<Integer> list = new ArrayList<>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode != null){
            if(listNode.next!=null){
                list = printListFromTailToHead(listNode.next);
            }
            list.add(listNode.val);
        }
        return list;
    }
}
```