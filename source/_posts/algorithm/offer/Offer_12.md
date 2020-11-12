---
title: 12 数值的整数次方
date: 2020/03/13
tags: 
    - 算法
    - 剑指offer
---

### 题目描述

* 给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。
* 保证base和exponent不同时为0。
<!-- more -->

### 思路
    考虑exponent是正负的情况。
    10^1011=10^1000*10^0010*10^0001;
    指数>>1，底数^2，结果是一样的，exponent&1==1只有位值为1的才计算，底数并翻倍了。
### Java 1.8

```
public class Solution {
    public double Power(double base, int exponent) {
        double result = 1;
        int a = exponent;
        if(base == 0){
            return 0;
        }
        if(exponent == 0){
            return 1;
        }
        if(exponent < 0){
            exponent = -exponent;
        }
        while (exponent!=0) {
            if((exponent&1)==1){
                result*=base;
            }
            base*=base;
            exponent >>= 1;
        }
        return a > 0?result:1/result;
    }
}
```
