# XX Open Cup. Stage 12. Grand Prix of Zhejiang / Petrozavodsk Winter 2020. Yuhao Du Contest 7

+ [ ] [A. Alternative Accounts](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/A/)
+ [x] [B. Bitset Master](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/B/)
+ [ ] [C. Cyclic Distance](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/C/)
+ [x] [D. Data Structure Quiz](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/D/)
+ [ ] [E. Evil Subsequence](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/E/)
+ [x] [F. Fast as Ryser](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/F/)
+ [ ] [G. Geometry PTSD](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/G/)
+ [x] [H. Heavy Stones](https://official.contest.yandex.ru/opencupXX/contest/17333/problems/H/)
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

+ $1\ u$：询问有多少$S_v$包含$u$。
+ $2\ p$：把$S_{u_p}$和$S_{v_p}$都改成$S_{u_p} \cup S_{v_p}$。

$2 \le n \le 200000, 1 \le m \le 600000$

题解：考虑如何暴力处理一个询问。我们从$u$开始DFS，同时维护一个变量$x$，一开始为$0$。那么一条边能走当且仅当这条边上存在一个操作$2$的下标大于$x$，同时我们把$x$更新为这条边上的最小操作下标。那么能够访问到得点的个数就是答案。那么可以用树分治优化这个过程。

考虑进行树分治，对于每个分治重心$g$，我们求出$u$到达$g$的时候的$x$的值，记为$f_u$。同时，对于每个点$v$，考虑一个下标为$e$的操作$2$，这个操作恰好是$g$到$v$的路径上的最后一条边，我们求出这条路径第一条边的最大操作下标，记为$g(v,e)$。显然这两个值都可以通过一遍从$g$开始的DFS求出来。

接下来考虑询问操作，假设从$u$出发，下标为$t$，那么显然得有$f(u) \le t$。然后我们需要求出在这个分治重心$g$下，有多少点$v$，满足$v$和$u$在不同子树中，并且存在一个$e$，使得$g(v,e) \ge f(u), e \le t$。这个可以离线一遍处理出来。

## C. Cyclic Distance

题意：给出$n$个点的树，第$i$条边连接$u_i$和$v_i$，边权为$l_i$。给出一个$k$，找出$k$个不同的节点$p_1,p_2,\dots,p_k$，使得$\sum_{i=1}^{k} \text{dis}(p_i,p_{i \bmod k + 1})$最大。

$2 \le n \le 200000, 2 \le k \le n, 1 \le u_i, v_i \le n, 1 \le l_i \le 10^6$

## D. Data Structure Quiz

题意：有个$n \times n$的矩阵，一开始都是$0$。一开始做了$m_1$个操作，每次选一个子矩形，把每个元素都加上$w$。然后有$m_2$个询问，每次查询一个子矩形里面的最大值。

$1 \le n, m_1 \le 50000, 1 \le m_2 \le 500000, 1 \le w \le 10^9$

题解：不妨假设$n=2^m$，按照$X$轴进行分治，我们可以得到一个$m$层的分治结构，第$k$层有$2^k$个区间，第$i$个区间是$[i \cdot \frac{n}{2^k}, (i+1) \cdot \frac{n}{2^k})$。

那么显然对于每个询问我们可以把它分成在某些层中的$O(\log n)$个区间，我们只需要把这些区间的答案取个$\max$就是最终的答案。我们把$m_1$个操作$(x_1,y_1,x_2,y_2,w)$拆成对$x_1 \ge x, y_1 \le y \le y_2$都加上$w$，对$x_2 > x, y_1 \le y \le y_2$都减去$w$两种操作。

考虑第$k$层，依次枚举每个区间，同时用线段树维护$y$坐标上的最大值。把$x$端点在这个区间里的操作都加上去，这个区间里的操作处理完后。我们来考虑完全包含这个区间的询问，显然就是在线段树上查询一个区间历史最大值。但是注意到，我们处理到下一个区间的时候，这个历史最大值不能继承过来。因此还需要支持下清空历史最大值操作。这个可以通过对区间整体加一个无穷大的值$M$来实现，加完之后当前的最大值和历史最大值都会变成$M+m_y$，其中$m_y$是$y$坐标上加之前的最大值。

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

题解：可以发现按照操作顺序倒着依次从$1$到$n-1$编号的话，代价为$\sum_{i=1}^{n-1} (a_{p_i} \cdot i + a_k)$。

考虑一个经典问题：给出一棵有根树，每次可以选出一个祖先都被选过的点。第$i$次的代价为$i \cdot w_{p_i}$，求出最小代价。

显然这个题就是经典问题的两条链版本。做法是把每条链分成若干块，使得块内所有权重的平均数递减。那么按照平均数归并这两个块后，这个序列就是最终的答案序列。

回到原问题的话，可以发现每次$k$变化后，块的变化数目均摊是$O(1)$的。于是可以用线段树或者Treap维护合并后的序列。

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

题解：令$L=\text{lcm}(1,2,\dots,k)$，可以发现当$x \equiv r \pmod L$时，$\frac{x(x+1)\cdots (x+k)}{\text{lcm}(x,x+1,\dots,x+k)}$是一个固定的整数$c_r$。因此$\text{lcm}(x,x+1,\dots,x+k)$可以写成$\frac{1}{c_r} \sum_{i=1}^{k+1}a_i \cdot (Lt+r)^i$的形式。如果$L$比较小，我们可以$O(Lk)$求出答案。

通过本地一些实验还可以发现，令$L=p_1^{e_1}p_2^{e_2} \cdots p_m^{e_m}$，那么每个质数$p_i^{e_i}$对这个$c_r$的贡献值独立的。具体的说，令$f_i(r)$表示$x \equiv r \pmod{p_i^{e_i}}$时$p_i^{e_i}$的贡献，那么，当$r=\sum_{i=1}^{m} r_i \cdot M_i \bmod L$的时候，$c_r = \prod_{i=1}^{m} f_i(r_i)$。

于是我们可以把$L$拆成$L=L_1 \cdot L_2$，然后用中国剩余定理来合并。令$r \equiv r_1 M_1 + r_2 M_2 \bmod L$，显然$r_1 M_1 + r_2 M_2 < 2L$，不妨假设$r_1M_1 + r_2M_2 < L$。

按照$r_1M_1$和$r_2M_2$分别排序，然后枚举$r_1M_1$，自然也可以求出$r_2 M_2$的范围，肯定是一个前缀。然后把$r=r_1M_1 + r_2M_2$带入一开始求出来的式子，化简下即可求出答案。