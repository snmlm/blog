---
title: 27 字符串的排列
date: 2020/11/16
tags: 
    - 算法
    - 剑指offer
---

### 题目描述
- 输入一个字符串,按字典序打印出该字符串中字符的所有排列。
- 例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。 输入描述:
- 输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。
<!-- more -->

### 思路
- 用同一个数组进行，两两互换，去重。
### Java 1.8

```
public class Solution {
    public ArrayList<String> Permutation(String str) {
        ArrayList<String> list = new ArrayList<String>();
        if (str != null && str.length() > 0) {
            PermutationHelper(str.toCharArray(), 0, list);
            Collections.sort(list);
        }
        return list;
    }

    private void PermutationHelper(char[] chars, int i, ArrayList<String> list) {
        if (i == chars.length - 1) {
            list.add(String.valueOf(chars));
        } else {
            Set<Character> charSet = new HashSet<Character>();
            for (int j = i; j < chars.length; ++j) {
                if (j == i || !charSet.contains(chars[j])) {
                    charSet.add(chars[j]);
                    swap(chars, i, j);
                    PermutationHelper(chars, i + 1, list);
                    swap(chars, j, i);
                }
            }
        }
    }

    private void swap(char[] cs, int i, int j) {
        char temp = cs[i];
        cs[i] = cs[j];
        cs[j] = temp;
    }
}
```