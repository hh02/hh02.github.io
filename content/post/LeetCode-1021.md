---
title: "LeetCode 1021. Remove Outermost Parentheses"
date: 2021-11-04T12:31:52+08:00
draft: false
---

## 题目

A valid parentheses string is either empty "", "(" + A + ")", or A + B, where A and B are valid parentheses strings, and + represents string concatenation.

For example, "", "()", "(())()", and "(()(()))" are all valid parentheses strings.
A valid parentheses string s is primitive if it is nonempty, and there does not exist a way to split it into s = A + B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string s, consider its primitive decomposition: s = P1 + P2 + ... + Pk, where Pi are primitive valid parentheses strings.

Return s after removing the outermost parentheses of every primitive string in the primitive decomposition of s.

Example 1:

```text
Input: s = "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

## 思路

可以发现最外层的括号在退栈后栈会空，所以记录空栈时括号对的 index，然后删除就可以了。

## 代码

```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        int n = s.size();
        int t1 = -1, t2 = -1;
        stack<int> stk;
        bool d[n + 1];
        memset(d, 0, sizeof(d));
        for (int i = 0; i < n; i++) {
            if (s[i] == '(') {
                stk.push(i);
            } else {
                int t = stk.top();
                stk.pop();
                if (stk.empty()) {
                    d[i] = d[t] = true;
                }
            }
        }
        string ans;
        for (int i = 0; i < n; i++) {
            if (!d[i]) {
                ans.push_back(s[i]);
            }
        }
        return ans;
    }
};
```
