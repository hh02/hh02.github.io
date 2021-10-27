---
title: "LeetCode 32. Longest Valid Parentheses"
date: 2021-10-27T22:57:22+08:00
draft: false
---

## 题目

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example:

```text
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```

## 思路

- 对于遇到的每个 `(` ，我们将它的下标放入栈中
- 对于遇到的每个 `)` ，我们先弹出栈顶元素表示匹配了当前右括号：
  - 如果栈为空，说明当前的右括号为没有被匹配的右括号，我们将其下标放入栈中来更新我们之前提到的「最后一个没有被匹配的右括号的下标」
  - 如果栈不为空，当前右括号的下标减去栈顶元素即为「以该右括号为结尾的最长有效括号的长度」

## 代码

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> stk;
        stk.push(-1);
        int ans = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') {
                stk.push(i);
            } else {
                stk.pop();
                if (stk.empty()) {
                    stk.push(i);
                } else {
                    ans = max(ans, i - stk.top());
                }
            }
        }
        return ans;

    }
};
```
