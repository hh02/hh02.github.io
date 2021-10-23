---
title: "LeetCode 378. Kth Smallest Element in a Sorted Matrix"
date: 2021-10-22T23:03:34+08:00
draft: false
---

## 题目

Given an n x n matrix where each of the rows and columns are sorted in ascending order, return the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

## 思路

二分查找

## 代码

```cpp
class Solution {
public:
    bool check(vector<vector<int>>& matrix, int mid, int k, int n) {
        int i = n - 1;
        int j = 0;
        int num = 0;
        while (i >= 0 && j < n) {
            if (matrix[i][j] <= mid) {
                num += i + 1;
                j++;
            } else {
                i--;
            }
        }
        return num >= k;
    }
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        int l = matrix[0][0];
        int r = matrix[n-1][n-1];
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (check(matrix, mid, k, n)) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }
};
```


