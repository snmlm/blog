---
title: leetcode8-字符串转换整数（atoi）
date: 2023/1/13
tags: 
    - leetcode
---

# 题目描述
请你来实现一个 myAtoi(string s) 函数，使其能将字符串转换成一个 32 位有符号整数（类似 C/C++ 中的 atoi 函数）。

函数 myAtoi(string s) 的算法如下：

1. 读入字符串并丢弃无用的前导空格
2. 检查下一个字符（假设还未到字符末尾）为正还是负号，读取该字符（如果有）。 确定最终结果是负数还是正数。 如果两者都不存在，则假定结果为正。
3. 读入下一个字符，直到到达下一个非数字字符或到达输入的结尾。字符串的其余部分将被忽略。
4. 将前面步骤读入的这些数字转换为整数（即，"123" -> 123， "0032" -> 32）。如果没有读入数字，则整数为 0 。必要时更改符号（从步骤 2 开始）。
5. 如果整数数超过 32 位有符号整数范围 [−231,  231 − 1] ，需要截断这个整数，使其保持在这个范围内。具体来说，小于 −231 的整数应该被固定为 −231 ，大于 231 − 1 的整数应该被固定为 231 − 1 。
6. 返回整数作为最终结果。

注意：

本题中的空白字符只包括空格字符 ' ' 。
除前导空格或数字后的其余字符串外，请勿忽略 任何其他字符。
示例 1：

输入：s = "42"
输出：42
解释：加粗的字符串为已经读入的字符，插入符号是当前读取的字符。
第 1 步："42"（当前没有读入字符，因为没有前导空格）
         ^
第 2 步："42"（当前没有读入字符，因为这里不存在 '-' 或者 '+'）
         ^
第 3 步："42"（读入 "42"）
         ^
解析得到整数 42 。
由于 "42" 在范围 [-231, 231 - 1] 内，最终结果为 42 。
示例 2：

输入：s = "   -42"
输出：-42
解释：
第 1 步："   -42"（读入前导空格，但忽视掉）
       ^
第 2 步："   -42"（读入 '-' 字符，所以结果应该是负数）
         ^
第 3 步："   -42"（读入 "42"）
           ^
           
# 题目思路

- 清空前空格
- 判断正负号
- 遍历字符串，截止下一个非数字的字符
- 注意乘10和累加，溢出int范围

# Java
```
class Solution {
    public int myAtoi(String s) {
        if ((s == null) || s.equals("")) return 0;
        // 清空前空格
        s = s.trim();
        // 判断正负号
        boolean flag = false;
        if (s.length() >= 1 && (s.charAt(0) == '-' || s.charAt(0) == '+')) {
            flag = s.charAt(0) == '-';
            s = s.substring(1, s.length());
        }
        if (s.length() < 1 || '0' > s.charAt(0) || s.charAt(0) > '9') return 0;
        int i = 0, ans = 0;
        while (i < s.length() && '0' <= s.charAt(i) && s.charAt(i) <= '9') {
            int temp = s.charAt(i) - '0';
            if (flag) temp *= -1;
            if (ans > Integer.MAX_VALUE / 10 || (ans == Integer.MAX_VALUE / 10 && temp > 7)) {
                return Integer.MAX_VALUE;
            }
            if (ans < Integer.MIN_VALUE / 10 || (ans == Integer.MIN_VALUE / 10 && temp < -8)) {
                return Integer.MIN_VALUE;
            }
            ans = ans * 10 + temp;
            i++;
        }
        return ans;
    }
}
```