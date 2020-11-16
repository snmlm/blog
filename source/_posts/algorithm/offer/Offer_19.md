---
title: 19 顺时针打印矩阵
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，
- 例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 
- 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10。
<!-- more -->

### 思路
- 先确定边界，在哪里开始转弯。
- 可以用循环套循环的方式，直线路程在一个循环内，四个方向，四个循环。
- 也可以用单循环的方式，需要判断在哪个方向上。
### Java 1.8

```
public class Solution {
    public ArrayList<Integer> printMatrix(int [][] matrix) {
        ArrayList<Integer> result = new ArrayList<>();
        int width = matrix.length;
        int Length = matrix[0].length;
        int up = 0;
        int down = width-1;
        int left = 0;
        int right = Length-1;
        int i=0;
        int j=0;
        int count = 1;
        while(true){
            switch (count%4) {
            case 1:
                if(j>right){
                    j--;
                    i++;
                    up++;
                    count++;
                }else{
                    result.add(matrix[i][j++]);
                }
                break;
            case 2:
                if(i>down){
                    right--;
                    count++;
                    i--;
                    j--;
                }else{
                    result.add(matrix[i++][j]);
                }
                break;
            case 3:
                if(j<left){
                    down--;
                    count++;
                    j++;
                    i--;
                }else{
                    result.add(matrix[i][j--]);
                }
                break;
            case 0:
                if(i<up){
                    left++;
                    count++;
                    i++;
                    j++;
                }else{
                    result.add(matrix[i--][j]);
                }
                break;
            }
            
            if(up>down||left>right){
                break;
            }
        }
        return result;
    }
}
```
