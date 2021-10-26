---
title: "LeetCode 240. Search a 2D Matrix II"
date: 2021-10-26T16:41:50+08:00
draft: false
---

## 题目

Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.

Example 1:

![20211026164226](https://cdn.jsdelivr.net/gh/hh02/img@main/img/20211026164226.png)

```text
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```

## 思路

由题目可知，矩阵的每一行是递增的，每一列是递增的。

从第一行的最后一个元素 matrix[i][j](i=0, j=n-1) 开始：

1. 若 target == matrix[i][j], 则返回 true；
2. 若 target < matrix[i][j]， 则对于当前 j，所有 i' > i的元素 matrix[i'][j] > matrix[i][j], 所以可以排除掉 matrix[i~m-1][j]，matrix[0~i-1][j] 之前已经被排除掉了，所以 j--;
3. 若 target > matrix[i][j], 对于当前 i，所有 j' < j 的元素, matrix[i][j'] < matrix[i][j], 所以可以排除掉第 matrix[i][0~j], matrix[i][j+1~n-1]之前已经被排除掉了，所以 i++;
4. 重复 1 ~ 3  直到 i > m 或者 j < 0。

主要思路就是每次可以排除一行或者一列。

## 代码

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();
        int i = 0, j = n - 1;
        while (i < m && j >= 0) {
            if (target == matrix[i][j]) {
                return true;
            }
            if (target > matrix[i][j]) {
                i++;
            } else {
                j--;
            }
        }
        return false;
    }
};
```
