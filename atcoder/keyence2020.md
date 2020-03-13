# Keyence Programming Contest 2020

+ [ ] [A. Painting](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_a)
+ [ ] [B. Robot Arms](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_b)
+ [ ] [C. Subarray Sum](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_c)
+ [ ] [D. Swap and Flip](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_d)
+ [ ] [E. Bichromization](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_e)
+ [ ] [F. Monochromization](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_f)

## A. Painting

题意：有一个$H \times W$的格子，一开始都是白色的。你每次可以选择一列或者一行全部染黑，求出最少操作几次才能使至少有$N$个黑格子。

$1 \le H, W \le 100, 0 \le N \le H \times W$

题解：令$H \le W$，答案是$\lceil \frac{N}{W} \rceil$。

## B. Robot Arms

题意：给出$N$个区间$[X_i - L_i, X_i + L_i]$。你要删掉最少的区间使得剩下的区间不相交。

$1 \le N \le 10^5, 0 \le X_i \le 10^9, 1 \le X_i \le 10^9$

题解：按照左端点排序，然后贪心即可。

## C. Subarray Sum

题意：给出$N$，$K$和$S$。构造一个长度为$N$的序列$A_1,A_2,\dots,A_N$，使得恰好有$K$对$(l,r)$满足$A_{l}+A_{l+1}+\dots+A_r=S$。

$1 \le N \le 10^5, 0 \le K \le N, 1 \le S \le 10^9, 1 \le A_i \le 10^9$

题解：令前$K$个数是$S$，后$N-K$个数是$S+1$。如果$S=10^9$，则后$N-K$个数为$S-1$。

## D. Swap and Flip

题意：有$N$张牌，一开始都是正面朝上。从左往右第$i$张正面写着$A_i$，反面写着$B_i$。每次你可以选择相邻两张牌交换位置，然后翻转这两张牌。求出最少操作多少次才能使得存在所有牌从左往右非递增。

$1 \le N \le 18, 1 \le A_i, B_i \le 50$

## E. Bichromization

题意：给出一个$N$个点$M$条边的无向图，你需要给每个点黑白染色，以及给每条边一个$1$到$10^9$的边权，使得：

+ 至少有一个点染成了白色，至少有一个点染成了黑色
+ 对于每个点$v$，从$v$到某个异色点的最短路恰好是$D_v$。

$2 \le N \le 10^5, 1 \le M \le 200000, 1 \le D_v \le 10^9$

## F. Monochromization

题意：有一个$H \times W$的格子，每个位置一开始被染成了白色或者黑色。每次你可以选一行或者一列，全部染成白色或者黑色。求出能够到达多少种不同的局面，对$998244353$取模。

$1 \le H, W \le 10$