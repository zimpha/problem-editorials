# Valentines Day Contest 2020

+ [x] [A. Leakage](https://codeforces.com/gym/102512/problem/A)
+ [ ] [B. Confession](https://codeforces.com/gym/102512/problem/B)
+ [x] [C. Isolation](https://codeforces.com/gym/102512/problem/C)
+ [x] [D. Equality](https://codeforces.com/gym/102512/problem/D)
+ [ ] [E. Valentine](https://codeforces.com/gym/102512/problem/E)
+ [x] [F. Opposition](https://codeforces.com/gym/102512/problem/F)
+ [x] [G. Honeymoon](https://codeforces.com/gym/102512/problem/G)

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

题解：那些和$(X,Y)$距离恰好为$D$的都是不能走的点，搞出这些点集，假设有$m$个。令$dp(a,(x_i,y_i))$表示走了$a$步，第一次到达点$(x_i,y_i)$的方案数。那么$dp(a,(x_i,y_i))=ways((0,0),(x_i,y_i),a)-\sum_{b=1}^{a-1}\sum_{j=1}^{m}dp(b,(x_j,y_j) \cdot ways((x_i,y_i),(x_j,y_j),a-b))$。

其中$ways((x_i,y_i),(x_j,y_j),n)$表示从$(x_i,y_i)$走$n$步到达$(x_j,y_j)$的方案数。这个就是两个组合数相乘。

最后答案就是$4^N-\sum_{i=1}^{N}\sum_{j=1}^{m}dp(i,(x_j,y_j)) \cdot 4^{N-i}$。

## D. Equality

题意：给出$N$，$X$个区间$[a_i,b_i]$和$Y$个区间$[c_i,d_i]$。求出有多少$T$，使得$1 \le T \le N$并且$T,3T,5T,\dots,$都在这$X$区间里，$2T,4T,6T,\dots,$都在这$Y$个区间里。

$1 \le N \le 10^9, 1 \le X, Y \le 300, 1 \le a_i \le b_i \le N, 1 \le c_i \le d_i \le N$

题解：转成考虑哪些$T$不合法，也就是说枚举一个不在$X$里的区间$[l,r]$使得存在一个$k$，$(2k-1)T$在区间里。或者枚举一个不在$Y$里的区间$[l,r]$使得存在一个$k$，$2kT$在区间里。枚举$k$和$T$较小那个就可以统计了。

## E. Valentine

题意：给出$X$，构造一个$N \times M$的矩形，使得恰好存在X$个$K \times 1$或者$1 times K$的子矩形，位置是严格递增的。

$1 \le X \le 7995051, 1 \le N, M \le 200, 1 \le a_{i,j} \le 10^6$

## F. Opposition

题意：有个字符串$s$，由`LOVE?`组成。两个人轮流玩，每次可以把一个`?`替换成其他四个字符。先手目的是最大化`LOVE`子串的个数，后手是最小化。你需要写个程序交互完成这个博弈，作为先手或者后手。

$1 \le |s| \le 200000$

题解：先求出在哪些位置插入一个字符后能够得到`LOVE`。那么先手一开始一定是从这些位置里选，后手也一样。之后先手每放一步，后手就能阻止形成`LOVE`。因此仅需要维护这个集合即可。

## G. Honeymoon

题意：给出$N$对数$(a_1,b_1),(a_2,b_2),\dots,(a_n,b_n)$。然后有$Q$个询问，每次给出一个区间$[l_i,r_i]$，定义$f_{x}=\max(\sum_{y=1}^{x} a_{l_i+y-1}, \sum_{y=1}^{x} b_{l_i+y-1})$，求出$f_(1)+f(2)+\dots+f(r_i-l_i+1)$。

$1 \le N, Q \le 500000, -10^6 \le a_i, b_i \le 10^6, 1 \le l_i \le r_i \le n$

题解：令$sb$表示$b$的前缀和，$sa$表示$a$的前缀和。那么考虑分$sb_i-sb_{l-1} \ge sa_i - sa_{l-1}$和$sb_i-sb_{l-1} < sa_i - sa_{l-1}$把$\max$去掉。等价于$sb_i-sa_i \ge sb_{l-1}-sa_{l-1}$和$sb_i-sa_i < sb_{l-1}-sa_{l-1}$。离线处理即可。
