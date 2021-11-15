---
title: "LeetCode 15. 3Sum"
date: 2021-11-15T23:56:08+08:00
draft: false
---

## 题目

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

## 思路

与 2sum 类似，先对数组进行排序，枚举前两个数，第三个数是单减的。注意不要枚举重复了。

## 代码

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        for (int i = 0; i < n; i++) {
            if (i > 0 && nums[i] == nums[i-1]) continue;
            int k = n - 1;
            int target = -nums[i];
            for (int j = i + 1; j < n; j++) {
                if (j > i + 1 && nums[j] == nums[j-1]) continue;
                while (j < k && nums[j] + nums[k] > target) k--;
                if (k == j) break;
                if (nums[j] + nums[k] == target) {
                    ans.push_back({nums[i], nums[j], nums[k]});
                }
            }
        }
        return ans;
    }
};
```
