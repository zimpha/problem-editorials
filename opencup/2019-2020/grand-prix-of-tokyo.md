# XX Open Cup. Stage 15. Grand Prix of Tokyo

+ [x] [A. Cookies](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/A/)
+ [x] [B. Evacuation](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/B/)
+ [x] [C. Sum Modulo](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/C/)
+ [ ] [D. Xor Sum](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/D/)
+ [x] [E. Count Modulo 2](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/E/)
+ [x] [F. Robots](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/F/)
+ [ ] [G. Matrix Inversion](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/G/)
+ [x] [H. Construct Points](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/H/)
+ [x] [I. Amidakuji](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/I/)
+ [x] [J. Median Replace Hard](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/J/)
+ [ ] [K. Game and Queries](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/K/)
+ [x] [L. Yosupo’s Algorithm](https://official.contest.yandex.ru/opencupXX/contest/18072/problems/L/)

## A. Cookies

题意：有$N$块饼干，第$i$块甜度是$A_i$。有$M$个小孩，第$i$个会带一块甜度为$B_i$的饼干，他还有个偏好度$S_i$。考虑如下过程：

+ 假设一开始有$A_1,A_2,\dots,A_k$这些饼干在桌子上。
+ 这些孩子轮流过来，第$i$个来的时候会把饼干放到桌子上。如果$S_i=S$，他会拿走现在桌上甜度最大的饼干；如果$S_i=B$，他会拿走现在桌子上甜度最小的饼干。
+ 求出最后桌子上饼干的甜度之和。

对于每个$k=1,2,\dots,n$，求出最后剩下来的饼干甜度之和。

$1 \le N, M \le 2 \times 10^5, 0 \le A_i, B_i \le 10^9-1$

题解：原问题其实等价于这个操作：

+ 有$M$个数对$(B_i, S_i)$，每次给出一个数$v=A_j$，对于每个$i$，
  + 如果$S_i=S$，那么如果$v > B_i$，那么交换$v$和$B_i$
  + 如果$S_i=B$，那么如果$v < B_i$，那么交换$v$和$B_i$

可以发现，对于连续的`S`，我们可以构建一个大根堆；对于连续的`B`，我们可以构建一个小根堆。考虑相邻的小根堆$x$和大根堆$y$，如果$\min(x) \ge \max(y)$，显然我们可以交换这两个堆的位置而不改变答案。并且交换之后。这两个可能分别和其他相邻的堆合并了。

可以证明，令$L$是当前大根堆的个数，最多操作$\frac{2M}{L}$步，大根堆的数目会变成$\frac{5L}{6}+C$，其中$C$是一个常数。

于是只需要暴力模拟上述过程即可。

## B. Evacuation

题意：有$N+2$个城镇，依次编号为$0$到$N+1$，第$i$个城镇里的避难所可以容纳$A_i$人。总共有$S$个游客要到某一个城镇游玩。现在给出$Q$个询问，每次$L_i,L_i+1,\dots,R_i$这些城镇收到影响，所有游客必须进入避难所，或者到达这些城镇以外的城镇。一个人往相邻城镇移动的代价是$1$，问最坏情况下的最小移动代价。

$1 \le N,Q \le 2 \times 10^5, 1 \le S \le 10^{12}, 0 \le A_i \le S, \sum A_i \le 10^{12}, 1 \le L_i \le R_i \le N$

题解：对于一个询问$l$和$r$，令$m=\frac{l+r}{2}$。显然当起始位置$x \in [l, m]$的时候，我们并不关心右边界的位置；类似的，当起始位置$x \in [m, r]$的时候，我们并不关心左边界的位置。于是不妨可以左右区间分开做，先考虑$x \in [l, m]$。

令$g(l,x)$表示起点在$x$，左边界在$l$的最小代价。我们可以预处理一点东西，然后可以$O(1)$计算这个函数。可以证明$g(l,x)$满足totally monotone，即$g(l,x)+g(l+1,x+1) \ge g(l,x+1)+g(l+1,x)$。那么接下来就由两种方法可以做这个题了。

做法1：构建一个线段树，然后把区间$[l,m]$分成线段树上$O(\log n)$个小区间。那么可以发现对于线段树上每个节点$u$，它上面有一堆询问。这些询问满足左端点不固定，$x \in [u.l,u.r]$。如果把这些询问的左端点排序，然后只考虑这些左端点和$x \in [u.l,u.r]$这个子矩阵，也是满足totally monotone的，可以用[SMAWK algorithm](https://en.wikipedia.org/wiki/SMAWK_algorithm)或者分治求出答案。

做法2：由于$g(l,x)$满足totally monotone，那么固定$x$后，$g(*,x)$其实是凸的。我们从小到大枚举$x$，然后考虑把$g(*,x)$这个凸壳加进来，显然这么多凸壳里面，对于固定的$l$，我们只关心$g(l,x)$最大的那个$x$。可以证明这个也是一个凸壳，并且肯定是来自于$g(*,x)$的某一段。也就是说其实可以用栈来维护最终的凸壳。每次新加入一个$g(*,x)$的话，可以先把肯定没用的凸壳弹栈，最终考虑栈顶的凸壳和新加入的凸壳的交点即可。多亏$g(l,x)$满足totally monotone，这样做正确性有了保证。

## C. Sum Modulo

题意：有一个随机数生成器，可以生成$1$到$N$内的任意整数。有一个序列$A_1,A_2,\dots,A_N$表示每个数生成的概率：数字$i$生成的概率为$\frac{A_i}{S}$，其中$S = \sum_{i=1}^{N}A_i$。

你有一个整数$X$，一开始为$0$。每次可以生成一个$1$到$N$的整数$v$，然把$X$变成$X+v \bmod M$。求出从$X$变成$K$的期望步数，对$998244353$取模。

$1 \le N \le \min(500, M-1), 2 \le M \le 10^{18}, 1 \le K \le M - 1,1 \le A_i \le 100$

题解：显然直接做需要列出$M$个变量的方程。注意到，$f(x)$一定可以表示成$f(0),f(1),\dots,f(N-1)$的线性组合。于是我们只需要知道$f(M-N),f(M-N+1),\dots,f(M-1)$分别关于$f(0),f(1),\dots,f(N-1)$的表示，就可以列出关于$f(0),f(1),\dots,f(N-1)$的线性方程组。最后可以直接解出$f(0),f(1),\dots,f(N-1)$，然后找出$f(K)$关于$f(0),f(1),\dots,f(N-1)$的线性组合，就可以直接求值了。

传统矩阵乘法需要$O(N^3 \log M)$的复杂度，考虑可以用多项式的思路来加速。

令$f(x)=w_x+\sum_{i=0}^{n-1}c_x(i) f(i)$，那么整体式子平移$y$结果也是不变的，也就是说$f(x+y)=w_x+\sum_{i=0}^{n-1}c_x(i) f(i+y)$，把$f(i+y)$展开可以得到

$$
f(x+y)=w_x+\sum_{i=0}^{n-1}c_x(i) (w_y+\sum_{j=0}^{n-1} c_y(j)f(i+j))
$$

稍微化简一下得到

$$
f(x+y)=w_x+w_y\sum_{i=0}^{n-1}c_x(i)+\sum_{k=0}^{2n-1} f(k)\sum_{i+j=k}c_x(i)c_y(j)
$$

显然右侧是一个卷积形式，暴力$O(n^2)$可以算出来。之后从$2n-1$开始依次消掉每一项即可。

于是可以用上面的做法用$O(N^2 \log M)$的复杂度倍增出$f(M-N)$的表示，然后令$y=1$，做$N$次就可以得到$f(M-N),f(M-N+1),\dots,f(M-1)$的表示。

## E. Count Modulo 2

题意：给出$K$个不同的数$A_1,A_2,\dots,A_K$。求出有多少长度为$N$的序列$a_1,a_2,\dots,a_N$，满足：

+ $a_1+a_2+\dots+a_N=S$
+ 对于每个$i$，都存在一个$j$，使得$a_i=A_j$

答案对$2$取模。

$1 \le N \le 10^{18}, 0 \le S \le 10^{18}, 1 \le K \le 200, 0 \le A_1 < A_2 < \dots < A_K \le 10^5$

题解：考虑$a$固定的情况，令$c(j)$表示$A_j$在$a$里出现次数。根据lucas定理，可以发现一定有$N \text{ and } c(j) = c(j)$并且$c(i) \text{ and } c(j) = 0$。

也就是说，对于$N$二进制表示中的每一个$1$，都需要找一个$A_j$。那么可以变成一个背包问题，假设$N$的第$i$位二进制是$1$，那么有$K$种物品，大小分别为$2^i \cdot A_1, 2^i \cdot A_2, \dots, 2^i \cdot A_K$。

令$dp(i,j)$表示考虑到第$i$位位置，和为$j$的方案数。考虑到$j \equiv S \bmod 2^{i}$，显然合法的$j$只有$O(A_K)$个。加上`std::bitset`优化后可以做到复杂度$O(\frac{K \cdot A_K \log N}{w})$

## F. Robots

题意：有$N$个机器人，第$i$个一开始在$a_i$处。有$N$个终点，第$i$个在$b_i$处。你需要依次激活每个终点，然后每激活一个终点，最近的机器人就会到达终点，然后爆炸。求出一个激活顺序，使得总移动距离最小。

$1 \le N \le 2 \times 10^5, 0 \le a_1 < a_2 < \dots < a_N \le 10^9, 0 \le b_1 < b_2 < \dots < b_N \le 10^9$

题解：显然距离是$\sum_{i=1}^{N} |a_i-b_i|$。激活顺序的话用一个栈就可以维护。

## H. Construct Points

题意：构造$4$个点$a,b,c,d$，使得

+ 坐标都是整数，并且绝对值不超过$10^9$。
+ 直线$ab$和直线$cd$的交点坐标绝对值不小于$10^{27}$。

题解：使得两直线的斜率之差尽可能小即可。比如，$(-10^9,0), (1,10^9), (0, -10^9), (10^9,-1)$。

## I. Amidakuji

题意：给出$N$，构造$K$个排列$p_1,p_2,\dots,p_K$使得：

+ $0 \le K \le \lceil \log_2 N\rceil + 1$
+ 对于所有的$x$和$y$，存在$K$个排列$q_1,q_2,\dots,q_K$使得$(q_K \circ q_{K-1} \circ \cdots \circ q_1)[x]=y$并且$q_i=p_i$或者$q_i=p_i^{-1}$。

$1 \le N \le 1000$

题解：当$N$是奇数的时候，直接令$p_{i,j}=j+2^i \bmod N$即可。

当$N$是偶数的时候，如果$N$是$4$的倍数，直接令$p_0=(2,3,1,0,6,7,5,4,\dots,N-2,N-1,N-3,N-4)$，其他和奇数一样；如果N$不是$4$的倍数，那么令$p_0=(2,3,1,0,6,7,5,4,\dots,N-4,N-3N-5,N-6,N-2,N-1)$，$p_1=(0,1,2,3,\dots,N −6,N −5,N −2,N −1,N −3,N −4)$，其他和奇数一样。

## J. Median Replace Hard

题意：给出一个长度为$8$的`01`串$P$。对于一个长度为$N$的`01`串$X$，考虑如下操作：选择三个连续位置$X_i,X_{i+1},X_{i+2}$，把他们换成$P[X_i+2X_{i+1}+4X_{i+2}]$。

如果能够通过操作$\frac{N-1}{2}$次得到`1`，那么$X$是好的。

现在给出一个串$S$，仅包含`01?`。你可以把`?`替换成`0`或者`1`，求出能够变成好串的替换方案数，对$10^9+7$取模。

$1 \le |S| \le 300000$

题解：可以考虑建出DFA，然后再DFA上dp即可。对于DFA上每个状态$x$，我们都拿能够到达它的最短`01`串$s_x$来表示它。考虑两个状态$x$和$y$，他们是同一个状态当且仅当$|s_x|$和$|s_y|$都是奇数，对于任意`01`串$z$，都有$s_x+z$是好的 $\leftrightarrow$ $s_y+z$是好的。

对于这题，没必要枚举所有$z$，仅需要取$|z| \le 10$即可。

## L. Yosupo’s Algorithm

题意：平面上有$N$个红点和$N$个蓝点，第$i$个红点坐标为($r^x_i , r^y_i$)，权值为$r^w_i$；第$i$个蓝点坐标为($b^x_i , b^y_i$)，权值为$b^w_i$。

有$Q$个询问，每次给出两个整数$L$和$R$，求出满足下面条件的$j$和$k$：

+ $r^y_j < b^y_k$
+ ($r^x_j < L_i$ and $R_i < b^x_k$) or ($L_i < r^x_j$ and $b^x_k < R_i$)
+ $r^w_j+b^w_k$最大

$1 \le N \le 10^5, 1 \le Q \le 500000, −1,000,000,000 \le r^x_i , L_i ≤ −1, 1 \le b^x_i , r^x_i, r^y_i , b^y_i, r^w_i , b^w_i \le 1,000,000,000$

题解：考虑一个分界线$y$满足$r^y_j < y < b^y_k$，显然可以证明要么$r^w_j$最大，要么$b^w_k$最大。

于是可以考虑对$y$分治，对于每个分治中心，都可以找出$O(N)$对可行的解。总共$O(N \log N)$对可行的解。最后直接对询问离线，做扫描线即可。

也可以考虑如下的方法，可以只找出$O(N)$对可行的解：

+ 对于每个红点$j$，找出$b^y_k > r^y_j$的，$b^w_k$最大的$k$
+ 对于每个蓝点$k$，找出$b^y_k > r^y_j$的，$r^w_j$最大的$j$
+ 考虑红点$j$满足$r^w_j$在前缀里最大，令$j^\prime$是最近那个$r^w_{j^\prime} > r^w_j$的位置。找出$b^y_k > r^y_{j^\prime}$的，$b^w_k$最大的$k$。

证明很显然，利用一开始说的性质即可。