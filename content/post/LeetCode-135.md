---
title: "LeetCode 135. Candy"
date: 2021-11-08T21:37:29+08:00
draft: false
---

## 题目

There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
Return the minimum number of candies you need to have to distribute the candies to the children.

Example 1:

```text
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```

## 思路

一开始的思路是首先最小值的糖果数是 1，因为没有比它更小的了，然后再去确定次小值。这样直接对原数组排序，从小往大去更新。这样做的时间复杂度是 nlogn。

后来看了题解，有更优的做法。设第 i 个人的糖果个数为 cnt[i], 想了半天也没想明白……

## 代码

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        int n = ratings.size();
        int l[n+1], r[n+1];
        for (int i = 0; i < n; i++) {
            l[i] = r[i] = 1;
        }
        for (int i = 1; i < n; i++) {
            if (ratings[i] > ratings[i-1]) {
                l[i] = l[i-1] + 1;
            }
        }
        int ans = l[n-1];
        for (int i = n-2; i >= 0; i--) {
            if (ratings[i] > ratings[i+1]) {
                r[i] = r[i+1] + 1;
            }
            ans += max(l[i], r[i]);
        }
        return ans;

    }
};
```
