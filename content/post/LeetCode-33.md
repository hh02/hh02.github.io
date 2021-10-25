---
title: "LeetCode 33. Search in Rotated Sorted Array"
date: 2021-10-25T16:47:56+08:00
draft: false
---

## 题目

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

```text
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

## 思路

虽然不是完全单调，但是还是可以用二分。

设在[l, r] 区间上搜索, mid = (l + r) / 2, 由于整个数组上只有一个跳跃点，且跳跃点右侧的值都是小于跳跃点左侧的值。在这个跳跃点左侧的区间，右侧的区间都是单调的，mid 要么在跳跃点的左侧要么在跳跃点的右侧。

1. 若 nums[mid] == target，则 mid 就是答案。
2. 若 nums[mid] > nums[0], 那么 mid 必然在左单调区间，因为右单调区间的值都是小于左单调区间的值的。1. 如果 nums[0] <= target <= nums[mid] 说明 target 不在 [mid + 1, r] 上， 排除一半的搜索范围；2. 否则，target 不在 [l, mid] 上同样排除一半的搜索空间。
3. 若 nums[mid] < nums[0], 与2同理。

## 代码

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = nums.size();
        int l = 0, r = n-1, mid;
        while (l <= r) {
            mid = (l + r) >> 1;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[0] <= nums[mid]) {
                if (nums[0] <= target && target <= nums[mid]) {
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            } else {
                if (nums[mid] <= target && target <= nums[n-1]) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        return -1;


    }
};
```
