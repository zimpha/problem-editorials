# Petrozavodsk Winter 2020. Day 9. Yuhao Du Contest 7

+ [ ] [A. Alternative Accounts](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/A/)
+ [ ] [B. Bitset Master](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/B/)
+ [ ] [C. Cyclic Distance](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/C/)
+ [ ] [D. Data Structure Quiz](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/D/)
+ [ ] [E. Evil Subsequence](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/E/)
+ [x] [F. Fast as Ryser](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/F/)
+ [ ] [G. Geometry PTSD](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/G/)
+ [ ] [H. Heavy Stones](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/H/)
+ [ ] [I. Interesting Game](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/I/)
+ [ ] [J. Junk Problem](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/J/)
+ [ ] [K. Knowledge-Oriented Problem](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/K/)
+ [ ] [L. LCM Sum](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/L/)

## A. Alternative Accounts

题意：有$n$个点的图，给出$k$个集合，表示这集合内部点两两之间有边。求出这个图的最小染色数。

$1 \le n \le 10^5, 1 \le k \le 4$

题解：可以求出所有的极大团，最多$12$个，然后可以搜一搜。

## B. Bitset Master

题意：给出$n$个点的树，$n-1$条边依次为$(u_1,v_1), (u_2,v_2), \dots, (u_{n-1}, v_{n-1})$。节点$u$上有个集合$S_u$，一开始为$\{u\}$。有$m$个操作

+ $1\ u$：询问$S_u$的大小。
+ $2\ p$：把$S_{u_p}$和$S_{v_p}$都改成$S_{u_p} \cup S_{v_p}$。

$2 \le n \le 200000, 1 \le m \le 600000$

## C. Cyclic Distance

题意：给出$n$个点的树，第$i$条边连接$u_i$和$v_i$，边权为$l_i$。给出一个$k$，找出$k$个不同的节点$p_1,p_2,\dots,p_k$，使得$\sum_{i=1}^{k} \text{dis}(p_i,p_{i \bmod k + 1})$最大。

$2 \le n \le 200000, 2 \le k \le n, 1 \le u_i, v_i \le n, 1 \le l_i \le 10^6$

## D. Data Structure Quiz

题意：有个$n \times n$的矩阵，一开始都是$0$。一开始做了$m_1$个操作，每次选一个子矩形，把每个元素都加上$w$。然后有$m_2$个询问，每次查询一个子矩形里面的最大值。

$1 \le n, m_1, m_2 \le 50000, 1 \le w \le 10^9$

## E. Evil Subsequence

题意：对于两个序列$(x_1,x_2,\dots,x_n)$和$(y_1,y_2,\dots,y_n)$，他们匹配当且仅当$x_i = x_j \Leftrightarrow y_i=y_j$。

给出一个长度为$n$个序列$a_1,a_2,\dots,a_n$和长度为$m$的序列$b_1,b_2,\dots,b_m$。求出$a$有多少子序列和$b$匹配，对$10^9+7$取模。

$1 \le n \le 3000, 1 \le m \le \min(5, n), 1 \le a_i \le n, 1 \le b_i \le m$

## F. Fast as Ryser

题意：给出$n$个点$m$条边的无向图和一个整数$c$。对于每个匹配$M$，代价为$c^{|M|}$。求出所有非空匹配的代价和，对$10^9+7$取模。

$1 \le n \le 36, 0 \le m \le \frac{n(n-1)}{2}, 1 \le c \le 10^9 + 6$

题解：假设有了一个匹配$M$，我们在$2i$和$2i-1$之间加一条虚边，那么加上匹配边，我们会得到一些环和一些路径。显然这样的环和路径个数最多只有$\frac{n}{2}$个。

于是我们不妨把$2i$和$2i-1$看成一个连通块，之后$O(2^{n/2}n^2)$算出每个子集构成环或者路径的方案数，假设总共有$l$个节点，那么环的贡献是$c^{l/2}$，路径的贡献是$c^{\lceil \frac{l}{2} \rceil}$或者$c^{\lceil \frac{l}{2} \rceil-1}$。

之后跑个子集卷积把这些连通块合并一下即可。

## G. Geometry PTSD

题意：构造三个三维空间的点$A$，$B$和$C$，使得$\min(|AB|, |AC|, |BC|) \ge 1.7$，并且$(0,0,0)$到平面$ABC$的距离不超过$1.5 \times 10^{-19}$但是大于$0$。

## H. Heavy Stones

题意：有$n$堆石子$a_1,a_2,\dots,a_n$。对于一个固定的$k$，你一开始选中第$k$堆石子，接下来每次可以选择左边一堆或者右边一堆合并成同一堆，代价为两堆大小之和。

对于每个$k=1,2,\dots,n$，求出最终合并成一堆的最小代价。

$1 \le n \le 200000, 1 \le a_i \le 10^6$

## I. Interesting Game

题意：有$n$个非负整数$a_1,a_2,\dots,a_n$，两个参数$A$和$B$。两个人轮流玩游戏。

第一个人每次可以把序列替换成满足下面条件的另一个序列$a_1^\prime,a_2^\prime,\dots,a_n^\prime$：

+ $a_1^\prime \ge a_1, \dots,a_n^\prime \ge a_n$
+ $\sum_{i=1}^{n} a_i^\prime \le \sum_{i=1}^{n} a_i + A$

第二个人每次可以选择$B$个下标$i_1,i_2,\dots,i_B$，然后把$a_{i_1},a_{i_2},\dots,a_{i_B}$都改成$0$。

令$M$是整个过程中$a_1,a_2,\dots,a_n$的最大值，第一个人想要最大化它，第二个人想要最小化它。求出最优情况下$M$的值。

$1 \le B \le n \le 10^5, 0 \le A \le 10^{12}, 0 \le a_i \le 10^{12}$


## J. Junk Problem

题意：给出$n$，构造一个$\{1,2,\dots,n\}$的子集$S$，满足

+ 对于任意$a, b \in S$并且$a < b$，$a$和$b$的异或值应该不同
+ $|S| \ge \lfloor \sqrt{0.5n} \rfloor$

$1 \le n \le 10^7$

## Knowledge-Oriented Problem

题意：给出$n$个点$m$条边的无向图$G$。把$G$复制$k$份得到$G_1,G_2,\dots,G_k$，然后对于每个$u$和$i$，连一条边把$G_i$中的$u$和$G_{i+1}$中的$u$相连。求出这个新图的生成树个数，对$10^9+7$取模。

$1 \le n \le 500, 0 \le m \le \frac{n(n-1)}{2}, 1 \le k \le 10^{18}$

## L. LCM Sum

题意：给出$n$和$k$，求出$\sum_{x=1}^{n} \text{lcm}(x,x+1,\dots,x+k)$，对$10^9+7$取模。

$1 \le n \le 10^{11}, 0 \le k \le 30$