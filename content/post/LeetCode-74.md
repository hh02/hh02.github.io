---
title: "LeetCode 74. Search a 2D Matrix"
date: 2021-10-25T17:00:43+08:00
draft: false
---

## 题目

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.

Example 1:

![20211025170139](https://cdn.jsdelivr.net/gh/hh02/img@main/img/20211025170139.png)

```text
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

## 思路

思路一：先对第一列进行二分查找，再对行进行二分查找；

思路二：将整个矩阵看作一个长为 m * n 的单调上升数组。

## 代码

用的是思路二：

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int low = 0, high = m * n - 1;
        while (low <= high) {
            int mid = (low + high) >> 1;
            int x = matrix[mid / n][mid % n];
            if (x < target) {
                low = mid + 1;
            } else if (x > target) {
                high = mid - 1;
            } else {
                return true;
            }
        }
        return false;
    }
};
```
