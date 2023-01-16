---
title: leetcode9-回文数
date: 2023/1/16
tags: 
    - leetcode
---

# 题目描述
给你一个整数 `x` ，如果 `x` 是一个回文整数，返回 `true` ；否则，返回 `false` 。

回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

- 例如，`121` 是回文，而 `123` 不是。

**示例 1：**

```
输入：x = 121
输出：true
```

**示例 2：**

```
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3：**

```
输入：x = 10
输出：false
解释：从右向左读, 为 01 。因此它不是一个回文数。
```

**提示：**

- `-231 <= x <= 231 - 1`

​           
# 题目思路



# Java
```java
class Solution {
    public boolean isPalindrome(int x) {
        // 小于0的有负号
        // 0结尾的，要以0开头
        if (x < 0 || (x % 10 == 0 && x != 0)) return false;
        int num = 0;
        // num有可能会比x大10，最后一个0
        while (x > num) {
            num = num * 10 + x % 10;
            x = x / 10;
        }
        return x == num || x == num / 10;
    }
}
```