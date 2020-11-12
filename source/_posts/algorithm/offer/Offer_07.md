---
title: 07 斐波那契数列
date: 2020/03/13
tags: 
    - 算法
    - 剑指offer
---

### 题目描述

* 大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
* n<=39
<!-- more -->

### 思路
    纯粹的斐波那契数列，0,1,1,2,3,5,8....
    n=0时，an=-1;
    n=1时，an=a1=0;
    n=2时，an=a2=1;
    n>2时，an=an-2+an-1;

### Java 1.8
```
public class Solution {
    public int Fibonacci(int n) {
        int a = 0;
        int b = 1;
        int c = 0;
        if(n == 0){
            return a;
        }else if(n == 1){
            return b;
        }else if(n > 1){
            for (int i = 2; i <= n; i++) {
                c = a + b;
                a = b;
                b = c;
            }
            return c;
        }else{
            return -1;
        }
    }
}
```