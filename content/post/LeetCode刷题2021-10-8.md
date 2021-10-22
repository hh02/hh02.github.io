---
title: "LeetCode刷题2021 10 8"
date: 2021-10-08T23:21:36+08:00
draft: false
---

| 题目                                                                                 | **题目难度** | 提交次数 |
| :------------------------------------------------------------------------------------- | -------------- | ---------- |
| [#14 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)          | **简单**     | 1 次     |
| [#13 罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/)             | **简单**     | 3 次     |
| [#12 整数转罗马数字](https://leetcode-cn.com/problems/integer-to-roman/)             | **中等**     | 2 次     |
| [#11 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)    | **中等**     | 1 次     |
| [#9 回文数](https://leetcode-cn.com/problems/palindrome-number/)                     | **简单**     | 1 次     |
| [#8 字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/) | **中等**     | 7 次     |
| [#7 整数反转](https://leetcode-cn.com/problems/reverse-integer/)                     | **简单**     | 5 次     |
| [#6 Z 字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)                 | **中等**     | 3 次     |

### 6. Z 字形变换

方法一：迭代，将每个字符放到对应行，然后输出。

方法二：找每一行的字符对应的索引

### 7. 整数反转

ret * 10 + digit <= INT_MAX

$$
ret <= \lfloor \frac{intmax-digit}{10} \rfloor

$$

ret * 10 + dight <= INT_MAX / 10 * 10 + INT_MAX % 10

(ret - INT_MAX / 10) * 10 <= 7 - digit

若 ret > INT_MAX / 10, 不等式不成立

若 ret == INT_MAX / 10，在 digit <= 7 时成立，因为 int 首位最大是2, 所以成立

若 ret < INT_MAX / 10,  不等式成立

所以比较 ret 和 INT_MAX / 10 可防止溢出。

### 8. 字符串转换整数 (atoi)

自动机，但我是直接模拟的。

### 9. 回文数

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }

        int revertedNumber = 0;
        while (x > revertedNumber) { // 这一行的判断方法很好！
            revertedNumber = revertedNumber * 10 + x % 10;
            x /= 10;
        }

        return x == revertedNumber || x == revertedNumber / 10;


    }
};
```

### 11. 盛最多水的容器



双指针法，减小了搜索空间。每次排除不可能是最优解的。

https://leetcode-cn.com/problems/container-with-most-water/solution/on-shuang-zhi-zhen-jie-fa-li-jie-zheng-que-xing-tu/

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l = 0, r = height.size() - 1;
        int ans = 0;
        while (l < r) {
            int area = min(height[l], height[r]) * (r - l);
            ans = max(ans, area);
            if (height[l] <= height[r]) l++;
            else r--;
        }
        return ans;

    }
};
```
