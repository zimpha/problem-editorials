# Codeforces Round #612

+ [ ] [Garland](https://codeforces.com/contest/1286/problem/A)
- [ ] [Numbers on Tree](https://codeforces.com/contest/1286/problem/B)
- [ ] [Madhouse](https://codeforces.com/contest/1286/problem/C2)
- [ ] [LCC](https://codeforces.com/contest/1286/problem/D)
- [ ] [Fedya the Potter Strikes Back](https://codeforces.com/contest/1286/problem/E)
- [ ] [Harry The Potter](https://codeforces.com/contest/1286/problem/F)

## A. Garland

题意：有一个长度为$n$的排列$p_1,p_2,\dots,p_n$。有些位置未知，你需要把它们填上使得这样的位置$i$最少：$p_i$和$p_{i+1}$的奇偶性不同。

$1 \le n \le 100, 0 \le p_i \le n$

题解：令$dp(i,j,k)$表示前$i$个位置填了$j$个偶数，第$i$个数的奇偶性是$k$的最优值。转移就枚举当前填什么数即可。

## B. Numbers on Tree

题意：有一棵$n$个点的有根树，每个点上有个整数$a_i$。令$c_i$表示子树$i$里满足$a_j < a_i$的$j$的个数。现在给出这棵树和$c$数组，构造一个$a$数组。

$1 \le n \le 2000, 0 \le c_i \le n - 1, 1 \le a_i \le 10^9$

题解：首先考虑$c_i=0$的那些节点，显然这些$a_i$要求是子树里的最小数。

## C. Madhouse

## D. LCC

## E. Fedya the Potter Strikes Back

## F. Harry The Potter
