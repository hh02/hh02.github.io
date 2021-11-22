---
title: "LeetCode 139. Word Break"
date: 2021-11-22T22:23:26+08:00
draft: false
---

## 题目

Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:

```text
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

## 思路

动态规划，dp[i] = dp[j] && check(j+1, i);

其中 check 用来检查某一个字串是否在dictSet中， dictSet 可以用stl库中的set（或者unordered_set)。

## 代码

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        auto wordDictSet = unordered_set <string> ();
        for (auto word: wordDict) {
            wordDictSet.insert(word);
        }
        bool dp[s.size() + 1];
        memset(dp, 0, sizeof(dp));
        dp[0] = true;
        for (int i = 1; i <= s.size(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDictSet.find(s.substr(j, i-j)) != wordDictSet.end()) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.size()];
    }
};
```
