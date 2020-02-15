# Valentines Day Contest 2020

+ [ ] [A. Leakage](https://codeforces.com/gym/102512/problem/A)
+ [ ] [B. Confession](https://codeforces.com/gym/102512/problem/B)
+ [ ] [C. Isolation](https://codeforces.com/gym/102512/problem/C)
+ [ ] [D. Equality](https://codeforces.com/gym/102512/problem/D)
+ [ ] [E. Valentine](https://codeforces.com/gym/102512/problem/E)
+ [ ] [F. Opposition](https://codeforces.com/gym/102512/problem/F)
+ [ ] [G. Honeymoon](https://codeforces.com/gym/102512/problem/G)

## A. Leakage

题意：给出$N$个点$M$条边的无向图。有$Q$个询问，每次给出两个点$C_i$和$D_i$，求出从$C_i$到$D_i$的必经点个数。

$3 \le N \le 200000, 1 \le M, Q \le 200000, 1 \le C_i, D_i \le N$

题意：求出割点，然后建出树，然后没了。

## B. Confession

题意：给出长度为$n$的排列$p_1,p_2,\dots,p_n$。对于一个随机的排列$a_1,a_2,\dots,a_n$，依次对每个$a_i$做如下操作：

+ 令$X = p_{a_i}$，如果$p_X=a_i$，那么$X$和$a_i$组成一对，并且被标记为不可用
+ 否则，如果$X$被标记了，或者存在一个$j > i$使得$a_j=X$，那么什么都不发生
+ 否则，$X$和$a_i$成为一对，并且被标记为不可用。

求出期望有多少对数，如果答案是$\frac{P}{Q}$，输出$P \cdot Q^{-1} \bmod (10^9+7)$。

$1 \le n \le 100, 1 \le p_i \le N$

## C. Isolation

题意：给出$N$，$X$，$Y$和$D$。求出从$(0,0)$出发，走$N$步，不能走到离$(X,Y)$曼哈顿距离小于等于$D$的位置。求方案数，对$10^9+7$取模。

$|X|, |Y| \le 1500, |X| + |Y| > D, 1 \le N \le 1500, 0 \le D \le 4$

## D. Equality

题意：给出$N$，$X$个区间$[a_i,b_i]$和$Y$个区间$[c_i,d_i]$。求出有多少$T$，使得$1 \le T \le N$并且$T,3T,5T,\dots,$都在这$X$区间里，$2T,4T,6T,\dots,$都在这$Y$个区间里。

$1 \le N \le 10^9, 1 \le X, Y \le 300, 1 \le a_i \le b_i \le N, 1 \le c_i \le d_i \le N$

## E. Valentine

题意：给出$X$，构造一个$N \times M$的矩形，使得恰好存在X$个$K \times 1$或者$1 times K$的子矩形，位置是严格递增的。

$1 \le X \le 7995051, 1 \le N, M \le 200, 1 \le a_{i,j} \le 10^6$

## F. Opposition

题意：有个字符串$s$，由`LOVE?`组成。两个人轮流玩，每次可以把一个`?`替换成其他四个字符。先手目的是最大化`LOVE`子串的个数，后手是最小化。你需要写个程序交互完成这个博弈，作为先手或者后手。

$1 \le |s| \le 200000$

## G. Honeymoon

题意：给出$N$对数$(a_1,b_1),(a_2,b_2),\dots,(a_n,b_n)$。然后有$Q$个询问，每次给出一个区间$[l_i,r_i]$，定义$f_{x}=\max(\sum_{y=1}^{x} a_{l_i+y-1}, \sum_{y=1}^{x} b_{l_i+y-1})$，求出$f_(1)+f(2)+\dots+f(r_i-l_i+1)$。

$1 \le N, Q \le 500000, -10^6 \le a_i, b_i \le 10^6, 1 \le l_i \le r_i \le n$
