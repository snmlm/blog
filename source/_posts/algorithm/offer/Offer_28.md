---
title: 28 数组中出现次数超过一半的数字
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
- 例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。
- 由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。
<!-- more -->

### 思路
- 最简单就是直接遍历，时间为O(n)
- 其他方式都是基于排序时间，排序有快有慢，往往不稳定。
### Java 1.8

```
public class Solution {
    public int MoreThanHalfNum_Solution(int[] array) {
        if(array.length==0){
            return 0;
        }
        if(array.length==1){
            return array[0];
        }
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        int maxNumber = array[0];
        int maxCount = 1;

        for (int i = 0; i < array.length; i++) {
            if (!map.containsKey(array[i])) {
                map.put(array[i], 1);
            } else {
                int count = map.get(array[i]);
                map.put(array[i], ++count);
                if(count>maxCount){
                    maxNumber = array[i];
                    maxCount = count;
                }
                if(maxCount>array.length/2){
                    return maxNumber;
                }
            }
        }
        return 0;
    }
}
```