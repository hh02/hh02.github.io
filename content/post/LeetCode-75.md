---
title: "LeetCode 75. Sort Colors"
date: 2021-10-25T17:14:15+08:00
draft: false
---

## 题目

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

Example 1:

```text
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

## 思路

朴素的方法：第一遍遍历把所有0移动到最左端，第二遍遍历把所有1移动到0后面。

改进一（双指针）：可以只遍历一遍，用两个指针p0, p1分别代表0的位置和1的位置，从左往右遍历遇到1将1交换到p1的位置，然后 p1++, 遇到0则将0交换到p0的位置，由于p0的位置上可能是1，如果是1还要再将1移动到p1的位置；然后 p0++, p1++；

改进二（双指针）：遍历一遍，用p0, p2分别代表0和2的位置，从左往右遍历，遇到0则将0交换到p0的位置，然后p0向后移动一位，遇到2则将2交换到p2的位置，然后p2再向前移动一位，但是原来p2的位置可能是2，如果是2还要再将2交换到p2的位置，直到不是2为止。

## 代码

改进一

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int p0 = 0, p1 = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] == 1) {
                swap(nums[i], nums[p1]);
                p1++;
            } else if (nums[i] == 0) {
                swap(nums[i], nums[p0]);
                if (p0 < p1) {
                    swap(nums[i], nums[p1]);
                }
                ++p0;
                ++p1;
            }
        }

    }
};
```

改进二

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int p0 = 0, p2 = n - 1;
        for (int i = 0; i <= p2; i++) {
            while (i <= p2 && nums[i] == 2) {
                swap(nums[i], nums[p2--]);
            }
            if (nums[i] == 0) {
                swap(nums[i], nums[p0++]);
            }
        }

    }
};
```
