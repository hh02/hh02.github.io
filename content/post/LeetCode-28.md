---
title: "LeetCode 28. Implement strStr()"
date: 2021-10-26T17:05:34+08:00
draft: false
---

## 题目

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

Example 1:

```text
Input: haystack = "hello", needle = "ll"
Output: 2
```

## 思路

KMP算法的模板题，终于会写 KMP啦！！！

## 代码

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int m = haystack.size(), n = needle.size();
        if (!n) return 0;
        int nxt[n+10];
        nxt[0] = -1;
        for (int i = 1, j = -1; i < n; i++) {
            while (j > -1 && needle[i] != needle[j+1]) j = nxt[j];
            if (needle[i] == needle[j+1]) j++;
            nxt[i] = j;
        }
        for (int i = 0, j = -1; i < m; i++) {
            while (j > -1 && (j == n-1 || haystack[i] != needle[j+1])) j = nxt[j];
            if (haystack[i] == needle[j+1]) j++;
            if (j == n - 1) {
                return i - n + 1;
            }
        }
        return -1;
    }
};
```
