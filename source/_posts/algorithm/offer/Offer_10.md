---
title: 10 矩形覆盖
date: 2020/03/13
tags: 
    - 算法
    - 剑指offer
---

### 题目描述

* 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。
* 请问用n个`2*1`的小矩形无重叠地覆盖一个`2*n`的大矩形，总共有多少种方法？
<!-- more -->

### 思路
    target=1,f(1)=1;
    target=2,f(2)=2;
    target=3,f(3)=f(1)+f(2);
    ....
    target=n-1,当剩最后一块：f(n-1)=f(n-2);
                      当剩最后两块：f(n-1)=2f(n-3);
    target=n,当剩最后一块：f(n)=f(n-1)(竖);
             当剩最后两块：f(n)=f(n-2)(横)+f(n-2)(竖);有一种情况包含了f(n-1)(竖),
             那么两个公式可以合并为f(n)=f(n-2)+f(n-1);
### Java 1.8

```
public class Solution {
    public int RectCover(int target) {
        int a = 1;
        int b = 2;
        int c = 0;
        if(target==1){
            return 1;
        }else if(target==2){
            return 2;
        }else {
            for (int i = 3; i <= target; i++) {
                c = a + b;
                a = b;
                b = c;
            }
        }
        return c;
    }
}
```
