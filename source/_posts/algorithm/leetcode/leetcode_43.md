---
title: leetcode43-字符串相乘
date: 2023/5/12
tags: 
    - leetcode
---

# 题目描述

给定两个以字符串形式表示的非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积，它们的乘积也表示为字符串形式。

**注意：**不能使用任何内置的 BigInteger 库或直接将输入转换为整数。



**示例 1:**

```
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```
输入: num1 = "123", num2 = "456"
输出: "56088"
```



**提示：**

- `1 <= num1.length, num2.length <= 200`
- `num1` 和 `num2` 只能由数字组成。
- `num1` 和 `num2` 都不包含任何前导零，除了数字0本身。

# 题目思路

- 回溯

# Java
```java
class Solution {
    public String multiply(String num1, String num2) {
        if("0".equals(num1) || "0".equals(num2)){
            return "0";
        }
        int length = num1.length() + num2.length();
        int[] num = new int[length];
        for (int i = num1.length() - 1; i >= 0; i--) {
            int a = num1.charAt(i) - '0';
            for (int j = num2.length() - 1; j >= 0; j--) {
                int b = num2.charAt(j) - '0';
                int c = a * b;
                // 十位
                int d = c / 10;
                // 个位
                int e = c % 10;
                int f = num[i + j + 1] + e;
                num[i + j + 1] = f % 10;
                num[i + j] = num[i + j] + d + f / 10;
            }
        }
        StringBuilder sb = new StringBuilder();
        boolean flag = false;
        for (int i = 0; i < length; i++) {
            if (flag || num[i] > 0) {
                flag = true;
                sb.append(num[i]);
            }
        }
        return sb.toString().equals("") ? "0" : sb.toString();
    }
}
```

