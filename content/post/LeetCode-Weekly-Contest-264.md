---
title: "LeetCode Weekly Contest 264"
date: 2021-10-25T15:22:51+08:00
draft: false
---

## 5907. Next Greater Numerically Balanced Number

### 题目

An integer x is numerically balanced if for every digit d in the number x, there are exactly d occurrences of that digit in x.

Given an integer n, return the smallest numerically balanced number strictly greater than n.

Example 1:

```text
Input: n = 1
Output: 22
Explanation: 
22 is numerically balanced since:
- The digit 2 occurs 2 times. 
It is also the smallest numerically balanced number strictly greater than 1.
```

### 思路

思路一：可以直接从 n 开始暴力枚举判断。

思路二：n 是 6 位数的，所以可以先把 7 位数以内所有的结果构造出来，然后用二分查找，这种解法速度更快。

### 代码

用的是思路二：

```cpp
class Solution {
public:
    void dfs(int i, vector<int>& tmp, vector<vector<int>>& p) {
        if (i > 7) {
            p.push_back(tmp);
            return;
        }
        dfs(i+1, tmp, p);
        tmp.push_back(i);
        dfs(i+1, tmp, p);
        tmp.pop_back();
    }
    void calc(int* c, long long num, vector<long long>& nums) {
        if (!c[1] && !c[2] && !c[3] && !c[4] && !c[5] && !c[6] && !c[7]) {
            nums.push_back(num);
            return;
        }
        for (int i = 1; i <= 7; i++) {
            if (c[i]) {
                c[i]--;
                calc(c, num*10 + i, nums);
                c[i]++;
            }
        }
        
    }
    int nextBeautifulNumber(int n) {
        vector<int> tmp;
        vector<vector<int>> p;
        dfs(1, tmp, p);
        vector<long long> nums;
        for (const auto& t: p) {
            int c[10];
            memset(c, 0, sizeof(c));
            int sum = 0;
            for (const auto j: t) {
                sum += j;
                c[j] = j;
            }
            if (sum <= 8)
            calc(c, 0, nums);
        }
        sort(nums.begin(), nums.end());

        int l = 0, r = nums.size() - 1, ans = 0;
        while (l <= r) {
            int mid = (l+r) / 2;
            if (nums[mid] > n) {
                ans = nums[mid];
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return ans;
        
    }
};
```
