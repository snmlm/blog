---
title: 21 弹出序列
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入两个整数序列，第一个序列表示栈的压入顺序，
- 请判断第二个序列是否可能为该栈的弹出顺序。
- 假设压入栈的所有数字均不相等。
- 例如序列1,2,3,4,5是某栈的压入顺序，
- 序列4,5,3,2,1是该压栈序列对应的一个弹出序列，
- 但4,3,5,1,2就不可能是该压栈序列的弹出序列。
- （注意：这两个序列的长度是相等的）
<!-- more -->

### 思路
- 正常处理，按照pushA进行压入，栈顶比对popA的值。
- 相等就弹出栈顶，继续比较popA的下一个值。
- 不相等就继续压入。
- 返回是判断栈是否为空，空了就表示popA是pushA的一个弹出序列，不为空就不是。
- 这里没有给栈的数据结构，给了arrayList的，需要模拟栈的样子。
- 这里我用了add(index,value),直接把list当成栈去处理。
- 也可以想成正常数组，细节地方需要调整，时刻获取数组长度即可。
### Java 1.8

```
public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        for (int i = 0,j=0; i < popA.length;) {
            arrayList.add(0,pushA[i++]);
            while(j < popA.length && arrayList.get(0)==popA[j]){
                arrayList.remove(0);
                j++;
            }
        }
        return arrayList.isEmpty();
    }
}
```