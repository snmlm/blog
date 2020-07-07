---
title: 二维数组中的查找
categories: 剑指offer
tags: 
	- 算法
---
 <meta name="referrer" content="no-referrer" />

### 题目描述

* 在一个二维数组中`（每个一维数组的长度相同）`，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
<!-- more -->


* 思路：从左下角开始，向右变大（x++），向上变小（y--）
* 1 2 3 4
* 2 3 4 5
* 3 4 5 6
* 4 5 6 7

### C++ 11

```
class Solution {
public:
    bool Find(int target, vector<vector<int> > array)
	{
        //标志是否存在
	    bool isExist = false;
	    //纵向长度
        int lenghtY = array.size();
        for (int i = 0; i < array[0].size();)
        {
            //lenghtY-1 是数组纵向长度坐标，小于0退出
            //array[0].lenght 一维数组的长度，每个一维数组的长度相同，那不相等的呢
            if (lenghtY - 1 < 0 || i > array[0].size())
            {
                return false;
            }
            if (target > array[lenghtY - 1][i])//大于右移
            {
                i++;
            }
            else if (target < array[lenghtY - 1][i])
            {
                lenghtY--;
            }
            else if (target == array[lenghtY - 1][i])
            {
                isExist = true;
                break;
            }
        }
        return isExist;
    }
};
```

### java 1.8

```
public class Solution {
    public boolean Find(int target, int [][] array) {
        //标志是否存在
        boolean isExist = false;
        //纵向长度
        int lenghtY = array.length;
        for (int i = 0;i < array[0].lenght){
            //lenghtY-1 是数组纵向长度坐标，小于0退出
            //array[0].lenght 一维数组的长度，每个一维数组的长度相同，那不相等的呢
            if(lenghtY - 1 < 0 || i > array[0].lenght){
                return false;
            }
            if(target > array[lenghtY - 1][i]){//大于右移
                i++;
            }else if(target < array[lenghtY - 1][i]){
                lenghtY--;
            }else if(target == array[lenghtY - 1][i]){
                isExist = true;
                break;
            }
        }
        return isExist;
    }
}
```

