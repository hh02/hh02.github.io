---
title: "LeetCode 206. Reverse Linked List"
date: 2021-10-23T23:21:59+08:00
draft: true
---

## 题目

Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:

![eg1](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```text
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

## 思路

有迭代和递归两种写法。

## 代码

### 迭代

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (head == nullptr) return nullptr;
        ListNode* p1 = nullptr;
        ListNode* p2 = head;
        ListNode* p3;
        while(p2) {
            p3 = p2->next;
            p2->next = p1;
            p1 = p2;
            p2 = p3;
        }
        return p1;
        

    }
};
```

### 递归

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) {
            return head;
        }
        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newHead;
    }
};
```
