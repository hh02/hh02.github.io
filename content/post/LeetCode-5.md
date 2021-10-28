---
title: "LeetCode 5. Longest Palindromic Substring"
date: 2021-10-28T19:54:02+08:00
draft: false
---

## 题目

Given a string s, return the longest palindromic substring in s.

Example 1:

```text
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

## 思路

方法一：动态规划

`f[i][j] = true` 表示 i~j 的字串为回文串，否则不是；

转移：`f[i][j] = (s[i] == s[j]) && (f[i+1][j-1])`

方法二：中心扩展法

是枚举所有回文中心并尝试扩展，需要注意的点是回文串的长度有可能是奇数也可能是偶数，回文中心不一样。

方法三：Manacher 算法

待填坑……

## 代码

动态规划实现

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        bool f[n][n];
        memset(f, 0, sizeof(f));
        for (int i = 0; i < n; i++) f[i][i] = true;
        for (int i = 0; i + 1 < n; i++) {
            if (s[i] == s[i+1]) f[i][i+1] = true;
        }
        for (int l = 3; l <= n; l++) {
            for (int i = 0; ; i++) {
                int j = i + l - 1;
                if (j >= n) break;
                f[i][j] = (s[i] == s[j]) && (f[i+1][j-1]);
            }
        }
        for (int l = n; l; l--) {
            for (int i = 0; ; i++) {
                int j = i + l - 1;
                if (j >= n) break;
                if (f[i][j]) return s.substr(i, j-i+1);
            }
        }
        return s.substr(0, 1);
    }
};
```
