# January Lunchtime 2020

+ [ ] [Construct Array](https://www.codechef.com/LTIME80A/problems/CARR)
+ [ ] [CCDSAP Exam](https://www.codechef.com/LTIME80A/problems/CCDSAP)
+ [ ] [Minimum and Maximum](https://www.codechef.com/LTIME80A/problems/MINMAXIN)
+ [ ] [Folding Paper](https://www.codechef.com/LTIME80A/problems/PAPER)
+ [ ] [Under the Tunnels](https://www.codechef.com/LTIME80A/problems/POPTUNNL)

## Construct Array

题意：给出$N$和$M$，求出有多少长度为$N$的序列，序列元素都在$1$到$M$之间，且不存在三个相邻元素一样，对$10^9+7$取模。

$1 \le N, M \le 10^{18}$

## CCDSAP Exam

题意：有个长度为$N$的`01`串，每次操作可以把一个`1`和相邻的`0`交换位置。求最小操作次数使得没有两个连续的`1`。

$1 \le N \le 2 \times 10^5$

## Minimum and Maximum

题意：交互题。有一个长度为$N$的序列$A_1,A_2,\dots,A_N$，你需要通过以下询问找到序列的最小，次小，最大和次大值：

+ 询问两个整数$i$和$j$，如果$A_i \le A_j$，返回$i$，否则返回$j$。

注意：交互器是自适应的。你最多只能问$\lfloor \frac{3}{2} N \rfloor + 20$。

$4 \le N \le 1000$

## Folding Paper

题意：有一张纸，你操作了$N$次，对应一个由`RLUD`组成的字符串$S$，最后得到了一个$W \times H$的长方形。然后你在上面滴了$M$滴墨水。求出展开后最近点对的距离。

$2 \le M \le 1000, 1 \le N \le 1000, 3 \le W, H \le 10^9$

## Under the Tunnels

题意：有$N$块砖，和一个$N \times N$的`01`矩阵$S$。当你站在第$i$块砖时，如果$S_{i,j}=0$，那么这块砖不能走，否则可以走。你每次可以走到$|i-j| \le K$的砖$j$上。求出最小步数到达$N$。

$1 \le K < N \le 10^3$
