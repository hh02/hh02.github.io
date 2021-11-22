---
title: "LeetCode 430. Flatten a Multilevel Doubly Linked List"
date: 2021-11-22T22:50:39+08:00
draft: false
---

## 题目

You are given a doubly linked list, which contains nodes that have a next pointer, a previous pointer, and an additional child pointer. This child pointer may or may not point to a separate doubly linked list, also containing these special nodes. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure as shown in the example below.

Given the head of the first level of the list, flatten the list so that all the nodes appear in a single-level, doubly linked list. Let curr be a node with a child list. The nodes in the child list should appear after curr and before curr.next in the flattened list.

Return the head of the flattened list. The nodes in the list must have all of their child pointers set to null.

Example 1:

![20211122225308](https://cdn.jsdelivr.net/gh/hh02/img@main/img/20211122225308.png)

```text
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output: [1,2,3,7,8,11,12,9,10,4,5,6]
Explanation: The multilevel linked list in the input is shown.
After flattening the multilevel linked list it becomes:
```

![20211122225339](https://cdn.jsdelivr.net/gh/hh02/img@main/img/20211122225339.png)

## 思路

这题没想出来，看了题解的代码也看了好久才看懂，不过看到评论里有说：前序遍历+重新串联，简单粗暴，不过用时有点长，其实这个可以看成二叉树。

当我们遍历到某个节点 node 时，如果它的child成员不为空，那么我们需要将child只想的链表结构进行扁平化，并且插入node与node的下一个节点之间。

因此，我们在遇到child成员不为空的节点时，就要先去处理child指向的链表结构，这就是一个**深度优先搜索**的过程。当我们完成了对child指向的链表结构的扁平化之后，就可以**回溯**到node节点。

为了能够将扁平化的链表插入node与node的下一个节点之间，我们需要知道扁平化的链表的最后一个节点last，随后进行如下的散步操作：

- 将node与node的下一个节点next断开；
- 将node与child相连；
- 将last与next相连。

这样一来，我们就可以将扁平化的链表成功地插入。

## 代码

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* prev;
    Node* next;
    Node* child;
};
*/

class Solution {
public:
    Node* dfs(Node* node) {
        Node* cur = node;
        Node* last = nullptr;
        while (cur) {
            Node* next = cur->next;
            if (cur->child) {
                Node* child_last = dfs(cur->child);
                next = cur->next;
                cur->next = cur->child;
                cur->child->prev = cur;
                if (next) {
                    child_last->next = next;
                    next->prev = child_last;
                }
                cur->child = nullptr;
                last = child_last;
            } else {
                last = cur;
            }
            cur = next;
        }
        return last;
    }
    Node* flatten(Node* head) {
        dfs(head);
        return head;
    }
};
```

令附先序遍历+重新串联：

```cpp
class Solution {
    vector<Node*> v;
public:
    void dfs(Node* head){
        if(head==NULL) return;
        v.push_back(head);
        dfs(head->child);
        dfs(head->next);
    }
    
    Node* flatten(Node* head) {
        dfs(head);
        int n = v.size();
        for(int i = 0;i<n;i++){
            if(i+1<n) v[i]->next = v[i+1];
            if(i>0) v[i]->prev = v[i-1];
            v[i]->child = NULL;
        }
        return head;
    }
};
```
