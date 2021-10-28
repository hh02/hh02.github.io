---
title: "Learn KMP"
date: 2021-10-28T20:10:06+08:00
draft: true
---

判定 A[1~N] 是否是字符串 B[1~M] 的字串，并求出字符串 A 在字符串 B 中各次出现的位置。

1. 对字符串 A 进行自我匹配，求出一个数组 next, 其中 next[i] 表示“A 中以 i 结尾的非前缀字串”与“A的前缀”能够匹配的最长长度。

引理：

设 next[i] 的候选项为满足 A[1~j] = A[i-j+1~i] 的所有 j。

若 $j_0$ 为 next[i] 的候选项，则小于 $j_0$ 的最大的 next[i] 的候选项是 next[$j_0$]。

由此我们可以知道 next[$j_0$] + 1 ~ $j_0$ 之间都不是 next[i] 的候选项。

这样我们就可以快速求出 next[i] 的所有候选项： next[j], next[next[j]], next[next[next[j]]]...
