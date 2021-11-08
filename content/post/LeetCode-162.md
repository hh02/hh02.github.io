---
title: "LeetCode 162. Find Peak Element"
date: 2021-11-06T16:25:03+08:00
draft: false
---

## 题目

A peak element is an element that is strictly greater than its neighbors.

Given an integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞.

You must write an algorithm that runs in O(log n) time.

Example 1:

```text
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

## 思路

我以前一直以为必须单调的数组才能用二分查找，后来遇到 LeetCode 第33题，明白了只要每次能排除掉一半的选项也能用二分查找，再后来就遇到了这题，我才想明白，二分查找是每一确定一半的选项。

l = 0, r = nums.size() - 1, 对于每个 mid，有三种情况：

1. nums[mid-1] < nums[mid] > nums[mid+1]，直接返回答案；
2. nums[mid] < nums[mid+1], 说明mid 到 mid + 1 是递增的，那么mid + 1 ~ r，之间肯定有答案，因为：若mid+1 ~ r 是单增的，则 r 就是峰，若不是单增的，则一定有一个峰；
3. nums[mid-1] > nums[mid], 与2同理。

现在来证明若mid+1 ~ r 单增的，则 r 就是峰。

若 mid+1 ~ r 是单增的, nums[r-1] < nums[r]，我们只要证明 nums[r] > nums[r+1] 就行了。

我们可以证明无论 r 怎么变化，nums[r] 一定大于 nums[r+1]：

- 初始时，r = n-1, nums[r+1] = -∞， 显然 nums[r] > nums[r+1]；
- 在中途迭代中 r = mid' - 1 的条件是 num[mid' - 1] > nums[mid']，所以在迭代后 num[r] > nums[r + 1]。

证毕。

## 代码

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();

        auto get = [&](int i) -> pair<int, int> {
            if (i == -1 || i == n) {
                return {0, 0};
            }
            return {1, nums[i]};
        };

        int left = 0, right = n - 1, ans = -1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (get(mid - 1) < get(mid) && get(mid) > get(mid + 1)) {
                ans = mid;
                break;
            }
            if (get(mid) < get(mid + 1)) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return ans;
    }
};
```
