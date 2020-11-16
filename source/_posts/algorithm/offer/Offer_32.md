---
title: 32 把数据组排成最小的数
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。
- 例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。
<!-- more -->

### 思路
- 排序，比较规则
-          1.两个数变成同位数，进行比较
-          2.如果相等，则长数去掉最高位，继续比较，最终比较出大小。
- 例如3323和33
-      长数变为，33，32，23依次与33比较，
-      1.33和33比较，相同，继续比较
-      2.32和33比较，32小于33，那么23就不需要和33比较了，直接3323排在33之前，否则反之。
### Java 1.8

```
public class Solution {
    public String PrintMinNumber(int [] numbers) {
        if(numbers.length==0){
            return "";
        }
        String str = "";
        for (int i = 0;i< numbers.length-1;i++){
            for (int j = 0;j< numbers.length-1-i;j++){
                int numberA = numbers[j];
                int numberB = numbers[j+1];
                String numberAStr = numberA+"";
                String numberBStr = numberB+"";
                //置换，长数为numberAStr，短数为numberBStr
                if(numberAStr.length()<numberBStr.length()){
                    numberAStr = numberB+"";
                    numberBStr = numberA+"";
                }
                int b = new Integer(numberBStr).intValue();
                //比较
                for(int k = 0;k <= numberAStr.length()-numberBStr.length();k++){
                    int a = new Integer(numberAStr.substring(k,k+numberBStr.length())).intValue();
                    if(a>b){
                        numbers[j] = b;
                        numbers[j+1] = new Integer(numberAStr).intValue();
                        break;
                    }else if(a<b){
                        numbers[j] = new Integer(numberAStr).intValue();
                        numbers[j+1] = b;
                        break;
                    }
                }
                if(j == numbers.length-2-i ){
                    str = numbers[j+1] + str;
                }
            }
        }
        str = numbers[0]+str;
        return str;
    }
}
```