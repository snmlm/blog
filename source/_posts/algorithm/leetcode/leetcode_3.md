---
title: leetcode3-无重复字符串的最长子串
date: 2023/1/16
tags: 
    - leetcode
---

# 题目描述
给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```



**提示：**

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成

​        

# 题目思路

- 清空前空格
- 判断正负号
- 遍历字符串，截止下一个非数字的字符
- 注意乘10和累加，溢出int范围

# Java
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int ans = 0;
        Map<Character,Integer> map = new HashMap<>();
        for (int end = 0,start = 0 ; end < s.length();end++){
            Character character = s.charAt(end);
            if(map.containsKey(character)){
                start = Math.max(map.get(character),start);
            }
            ans = Math.max(ans,end - start + 1);
            map.put(character,end + 1);
        }
        return ans;
    }
}
```