---
title: 跳台阶
categories: 剑指offer
tags: 
	- 算法
---
 <meta name="referrer" content="no-referrer" />

### 题目描述

* 一只青蛙一次可以跳上1级台阶，也可以跳上2级。
* 求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
<!-- more -->

### 思路
    限定了青蛙一次只能有两种跳法，用逆推方式去思考
    如果最后一次跳1级，那么一共有f（n-1）种跳法。
    如果最后一次跳2级，那么一共有f（n-2）种跳法。
    那么，f（n）=f（n-1）+f（n-2）。
    当n=0时，f（0）=0。
    当n=1时，只有一种f（1）=1。
    当n=2时，有两种情况f（2）=2。
    当n=3时，就符合f（n）=f（n-1）+f（n-2）。
    可以想到是斐波那契数列的变形。0,1,2,3,5,8...

### Java 1.8

```
public class Solution {
    public int JumpFloor(int target) {
        int a = 0;
        int b = 1;
        int c = 0;
        if(target<0){
            return -1;
        }else{
            for (int i = 1; i <= target; i++) {
                c = a + b;
                a = b;
                b = c;
            }
            return c;
        }
    }
}
```