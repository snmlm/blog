---
title: 变态跳台阶
categories: 剑指offer
tags: 
    - 算法
---
 <meta name="referrer" content="no-referrer" />

### 题目描述

* 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。
* 求该青蛙跳上一个n级的台阶总共有多少种跳法。
<!-- more -->

### 思路
    逆推思想，最后一次能跳几级。
    当n=1时，一次能跳1级，最后一次能跳1级，那么f（1）=f（1-1）=1。
    当n=2时，一次能跳1、2级，最后一次能跳1级，那么f（2）=f（2-1）。
                      最有一次能跳2级，那么f（2）=f（2-2）。
                      f（2）=f（2-1）+f（2-2）。
    当n=3时，一次能跳1、2、3级，最后一次能跳1级，那么f（3）=f（3-1）。
                                 最有一次能跳2级，那么f（3）=f（3-2）。
                                 最有一次能跳2级，那么f（3）=f（3-3）。
    当n=n时，一次能跳1、2、3.....n-2、n-1、n,
    那么f（n）=f（n-1）+f（n-2）+f（n-3）.......+f（n-（n-2））+f（n-（n-1））+f（n-n）。
    简化为f（n）=f（0）+f（1）+f（2）+......+f（n-2）+f（n-1）。
    f（n-1）=f（0）+f（1）+f（2）+......+f（n-2）。
    那么f（n）=f（n-1）+f（n-1）=2*f（n-1）。
    
    1,2,4,8,16.....

### Java 1.8

```
public class Solution {
    public int JumpFloorII(int target) {
        int a = 1;
        if(target==0){
            return -1;
        }else if(target==1){
            return 1;
        }else{
            for (int i = 2; i <= target; i++) {
                a = a<<1;
            }
            return a;
        }
    }
}
```