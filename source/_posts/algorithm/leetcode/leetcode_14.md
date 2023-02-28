---
title: leetcode14-最长公共前缀
date: 2023/2/27
tags: 
    - leetcode
---

# 题目描述

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。



**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

**提示：**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` 仅由小写英文字母组成



# 题目思路

- 获取第一个字符串，然后遍历之后，不一致就返回



# Java
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";
        if (strs.length == 1) return strs[0];
        String fristStr = strs[0];
        String result = "";
        for (int i = 1; i <= fristStr.length(); i++) {
            result = fristStr.substring(0, i);
            for (int j = 1; j < strs.length; j++) {
                if (!(strs[j].indexOf(result) == 0)){
                    return fristStr.substring(0, i - 1);
                }
            }
        }
        return result;
    }
}
```