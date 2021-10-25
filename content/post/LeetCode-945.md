---
title: "LeetCode 945. Minimum Increment to Make Array Unique"
date: 2021-10-25T15:13:52+08:00
draft: false
---

## 题目

You are given an integer array nums. In one move, you can pick an index i where 0 <= i < nums.length and increment nums[i] by 1.

Return the minimum number of moves to make every value in nums unique.

Example 1:

```text
Input: nums = [1,2,2]
Output: 1
Explanation: After 1 move, the array could be [1, 2, 3].
```

## 思路

遍历 nums 数组，遇到有重复的数字，加到不重复为止。

这个于哈希有点类似，当遇到重复时候向后寻找空位，但是有可能超时，可以用路径压缩（类似于并查集）进行加速。比官方题解 NlogN 解法要快一点。

## 代码

```cpp
class Solution {
public:
    int find(int x, int* d) {
        if (d[x + d[x]] != 0) {
            d[x] += find(x + d[x], d);
        }
        return d[x];
    }
    int minIncrementForUnique(vector<int>& nums) {
        int n = *max_element(nums.begin(), nums.end());
        int d[n * 2 + 10];
        memset(d, 0, sizeof(d));
        int ans = 0;
        for (const auto& t: nums) {
            int p = find(t, d);
            ans += p;
            d[t + p] = 1;
            
        }
        return ans;


    }
};
```
