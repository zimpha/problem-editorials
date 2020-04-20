# Petrozavodsk Summer 2018. Yuhao Du Contest 5

+ [ ] [A. Automorphism](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/A/)
+ [ ] [B. Border](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/B/)
+ [ ] [C. Convolution](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/C/)
+ [x] [D. Decomposition](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/D/)
+ [x] [E. Edit](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/E/)
+ [x] [F. Flow](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/F/)
+ [ ] [G. Good Game](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/G/)
+ [x] [H. Hamilton Path](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/H/)
+ [ ] [I. IOI Problem Revised](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/I/)
+ [ ] [J. Jump Jump Jump](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/J/)
+ [ ] [K. Knight](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/K/)
+ [x] [L. Link Cut Digraph](https://official.contest.yandex.ru/opencupXIX/contest/8950/problems/L/)

## A. Automorphism

题意：给出一个有根树，一开始只有一个编号为$1$的根节点。有$m$个操作：

+ 加入一个新的节点，编号为当前最大节点加$1$，父亲为$x$。
+ 询问以$x$为根的子树有多少自同构数，对$998244353$取模。

题解：对于一个点$u$，考虑他的儿子们$v_1,v_2,\dots,v_k$。按照是否同构将他们分成等价类$P_1,P_2,\dots,P_m$。定义$f(u)=\prod_{i=1}^{m} |P_i|$。那么显然一个点$x$对应的答案为$\prod_{y \in \text{Subtree(x)}} f(y)$。

我们用`link-cut tree`来维护整棵树的树链剖分(这里定义子树最大的为重边，如果最大和次打相同那么所有边都是轻边)，考虑加入一个新的加点$p$，可以发现$f(\cdot)$只有$O(\log n)$个位置发生了变化，这些位置一定是$p$到$1$路径上的轻边。这是因为对于一个点$u$，重边$v_1$满足$size(v_1) > size(v_i)$，和$v_1$同构的只可能有一个点，对$f(\cdot)$的贡献可以忽略。

于是我们需要用`link-cut tree`维护每个点的树hash值，同时还得在每个节点$u$维护一个平衡树保存儿子的hash值，同时计算$f(u)$的变化。

## B. Border

题意：给出一个随机生成的`01`串$s$。对于一个子串$s[l..r]$，定义
$$
f(l,r)=\max\{k \mid 0 \le k \le j - i, s[i..i+k-1] = s[j-k+1..j]\}
$$

求出$\sum_{i=1}^{n}\sum_{j=i+1}^{n}f(i,j)$。

题解：由于是随机生成的串，因此$f(l,r)$的值不大。枚举$f(l,r)$的值$x$，那么考虑所有长度为$x$的子串，把相同的归为同一类，然后同一类里的计算下即可。

## C. Convolution

题意：给出序列$a_0,a_1,\dots,a_{n}$和$b_0,b_1,\dots,b_n$，求出$c_0,c_1,\dots,c_n$使得
$$
c_k=\left( \sum_{i=0}^{k}\binom{k}{i}a_ib_{k-i}\right) \bmod 2^{32}
$$

题解：令$f_i=\frac{2^ia_i}{i!},g_i=\frac{2^ib_i}{i!},h_i=\frac{2^ic_i}{i!}$，显然$h$是$f$和$g$的卷积。

## D. Decomposition

题意：给出一个字符串$s$，你可以把它划分成若干个非空字符串，总共有$2^{|S|-1}$种划分方法。

对于一个子串$t$，定义它的权重为最短的字符串$x$的长度，使得$t=xx\dots x$。一个划分的权重为所有子串的权重之积。求出所有划分的权重之和，对$10^9+7$取模。

题解：首先可以用后缀数组求出$s$的所有`runs`，那么对于每个$i$，我们就能求出以$i$结尾的，最小周期为$p$的极大串，用$(p,x)$表示。可以证明总的个数是$O(n \log n)$的。

然后就可以直接dp了，令$dp_i$表示划分到$i$为止的权重之和。那么$dp_i=\sum_{j=0}^{i-1} dp_j \cdot (i - j) - \sum_{(p,x)} \sum_{j=2}^{x} dp_{i-jp} (i - (i - jp)) + p \cdot dp_{i-jp}$。

可以发现对于同一个`runs`里面，$i \pmod p$一样的位置可以直接用个前缀和递推上来。

## E. Edit

题意：给出两棵带权的有根树，对于每个节点儿子也是有序的。你有以下$4$中操作：

1. **Growing**: 对于一个点$x$，令它的儿子们为$y_1, y_2, \dots, y_m$。可以加入一个点$z$，加入一条$x$到$z$的边，并把$z$插到第$k$个儿子的位置上去。然后$x$儿子变为$y_1, y_2, \dots , y_{k−1}, z, y_k, y_{k+1}, \dots, y_m$。代价为$c_1$ 乘上$(x, z)$的边权。
2. **Expansion**: 对于一个点$x$，令它的儿子们为$y_1, y_2, \dots, y_m$。你可以选择一个区间$[l, r]$ ($1 \le l \le r \le m$)。然后加入一个新的点$z$作为 $y_l , y_{l+1}, \dots, y_r$的父亲，以及加入一条$x$到$z$的边。然后$x$儿子变为$y_1, y_2, \dots, y_{l−1}, z, y_{r+1}, \dots, y_m$。$z$的儿子变为$y_l , y_{l+1}, \dots, y_r$。对于所有$l \le i \le r$，边$(z, y_i)$的权值和$(x, y_i)$权值一样。代价为$c_1$ 乘上$(x, z)$的边权。
3. **Contraction**: 对于一个点$x$，令它的儿子们为$y_1, y_2, \dots, y_m$。你可以选择其中一个儿子$y_k$，令它的文字为$z_1, z_2, \dots, z_p$。你可以删掉边$(x, y_k)$，节点$y_k$也会变删掉。然后$x$的儿子变成$y_1, y_2, \dots, y_{k−1}, z_1, z_2, \dots, z_p, y_{k+1}, \dots, y_m$。对于所有$1 \le i \le p$，边$(x, z_i)$的权值和$(y_k, z_i)$的权值一样。代价为$c_2$ 乘上$(x, y_k)$的边权。
4. **Relabeling**: 对于一个点$x$和它的一个儿子$y$，它$(x, y)$的边权从$w_1$改成$w_2$。代价为$c_3 \cdot |w_1 − w_2|$。

有一些条件限制：

+ 你不可以**Relabeling**一条从**Growing**或者**Expansion**来的边。
+ 你不可以**Contraction**一条**Relabeling**过的边

求出从第一棵树变成第二棵树的最小代价。

$1 \le c_1, c_2, c_3 \le 10^6, 1 \le n_1 \le 50, 1 \le n_2 \le 2000$

题解：考虑树的括号序列，可以发现**Growing**和**Expansion**其实是同一个操作，都是插入一对匹配括号。**Contraction**则是删掉一对匹配括号。于是我们可以在括号序列上进行dp。

搞出第一棵树的括号序列$s$，令$f(x,l,r)$表示第二棵树中子树$x$和括号序列第$l$到第$r$位置同构的最小代价，令$g(x,l,r)$表示第二棵树中子树$x$和括号序列第$l$到第$r$位置同构，并且$x$的父边做了一次`relabel`的最小代价。转移方程很简单，复杂度$O(nm^3)$。

## F. Flow

题意：给出一个$n$个点$m$条边的二分图$G$，第$i$条边从左边的$u$到右边的$v$，容量为$w$。考虑这样一个图$F_k$：

+ 复制$k$份$G_i$，第$G_i$的右边节点$u$向$G_{i+1}$的左边节点$u$连一条容量为无穷的边。
+ 新建源点$S$和汇点$T$，源点$S$向$G_1$的左侧点连容量为无穷的边，$G_k$的右侧点向汇点$T$连容量为无穷的边。

令$f_k$为图$F_k$的最大流，求出$\lim\limits_{k \to \infty} f_k$。

$1 \le n \le 2000, 1 \le m \le 4000$

题解：可以发现答案等价于求图中的最大循环流，可以转成最小费用最大流。需要用原始对偶的做法来避免TLE。

## G. Good Game

题意：从$(0,0,\dots,0)$出发走到$(a_0,a_1,\dots,a_{n-1})$。每次可以选择一个坐标然后加一。有$m$个障碍物，并且要求路径上每个点$(x_0,x_1,\dots,x_{n-1})$要满足$x_0 \le x_1 \le \dots \le x_{n-1}$。

求出方案数，对$10^9+7$取模。

$1 \le n \le 50, 0 \le m \le 50, 0 \le a_0 \le a_1 \le \dots \le a_{n-1} \le 10^4$

## H. Hamilton Path

题意：给出一个$n$个点$m$条边的有向图。你需要求出所有满足下面条件的排列$p_1,p_2,\dots,p_n$：对于所有$1 \le i < j \le n$，边$(p_i,p_j)$存在当且仅当$j=i+1$。

定义排列$p_1,p_2,\dots,p_n$的权值为
$$
\left( \sum_{i=1}^{n}p_i \cdot 10^{n-i}\right) \bmod (10^9+7)
$$

求出符合条件的排列个数，对$10^9+7$取模。如果不超过$n$个，按照字典序排序后，输出他们的权值。

$1 \le n \le 500000, 1 \le m \le 20^6$

题解：可以发现，对于每个起点$x$，都最多只有一条唯一的路径，并且可以暴力$O(m)$求出这条可能的路径。

考虑维护这样的一些路径，一开始每条路径都是单点。如果存在一条路径$a \to b$和路径$c \to d$，$b$存在一条唯一连向其他路径的边，并且这条边恰好是$(b,c)$。那么可以把这两条路径合并成同一条。不断重复这个过程，直到没有这样的路径对。可以发现，会有以下几种情况

1. 存在恰好一条路径，这样我们找到了一组解，但是还可能有其他解。
2. 存在两条路径，其中一条路径连向了另外一条路径的非起点的某个点，这种情况可能有解
3. 其他情况都是无解的。

先考虑第一种情况，假设终点往起点有一条边相连，那么我们找到了一条哈密尔顿回路。那么这条路上这样的$x$可以作为起点：没有一条从$x$后面点跨越$x$连向$x$前面点的边。我们可以用前缀和来求出这些合法的点。

假设终点没有往起点连边，那么如果存在一个点$x$往起点$s$连了一条边，那么我们可能可以找到一组解。这样的$x$可能存在多个，稍微分析下就可以发现我们仅需要最后面的那个$x$。同时可以发现，最终排列的结尾肯定是$s$到$x$的一个前缀。进一步可以发现，这个排列的终点$t$一定没有边从$x$的后面忘$t$连边。于是可以暴力找出这个终点$t$，然后从终点出发$O(m)$暴力构建出这个排列。

接下来考虑第二种情况，可以发现如果路径$a \to b$连向了路径$c \to d$的某个点$x$ ($x \ne c$)。那么排列的终点要么是$b$，要么是$c \to x$的某个前缀。如果是$b$的话，类似上面的，可以直接暴力求出来。对于后者，我们可以发现，这个终点$t$也一定满足：

+ 没有边从$x$的后面忘$t$连边，没有其他路径往$t$连边
+ $c \to x$中，没有$t$后面的点跨过$t$，往$t$前面连边。

在满足上面条件下，找一个最靠近$x$的$t$，这个一定是最终可能的终点。同样可以暴力判定下。

## I. IOI Problem Revised

题意：在一个长度为$L$的环上有$n$个点$a_1,a_2,\dots,a_n$。你需要选出$k$个特殊点，使得每个点到最近特殊点的距离之和最小。

$1 \le n \le 200000, 1 \le k \le n, 1 \le L \le 10^{12}, 0 \le a_1 \le a_2 \le \dots \le a_n < L$

题解：可以发现，我们仅需要dp出所有边界线即可，特殊点一定放在相邻两个边界线内的中位数上。

先考虑线上的版本，我们可以用`wqs二分`在$O(n \log n \log W)$求出一组解$p_1,p_2,\dots,p_k$。可以发现，对于最优解$q_1,q_2,\dots,q_k$，一定满足$p_i \le q_i \le p_{i+1}$。

也就是说，我们把环划分成了$k$个区间，我们需要在每个区间里面选出恰好一个点来最小化我们的答案。这个是一个经典问题，来自[Petrozavodsk Summer 2010. Kyiv NU Contest. I. Underground](https://codeforces.com/gym/100020/problem/I)。

选一个长度最小的区间，那么这个区间长度必然不超过$\frac{n}{k}$。然后考虑在这个区间上分治。

+ 令$[l, r]$表示当前的分治区间，数组$vl(\cdot)$和$vr(\cdot)$表示每个区间的范围。
+ 我们可以求出起点选为$m=\frac{l+r}{2}$的最优解$pm(1),pm(2),\dots,pm(k)$。可以发现
  + 对于起点$x \in [l,m-1]$求出来的最优解$px(1),px(2),\dots,px(k)$，一定有$vl(i) \le px(i) \le pm(i)$。
  + 对于起点$x \in [m+1,r]$求出来的最优解$px(1),px(2),\dots,px(k)$，一定有$pm(i) \le px(i) \le vr(i)$。
+ 于是，可以递归$[l,m-1]$或者$[m+1,r]$的时候相应得修改左右端点。

固定起点$x$求最优解的话，可以考虑决策单调性。

可以证明整体复杂度是$O(n \log^2 n)$的。

## J. Jump Jump Jump

## K. Knight

## L. Link Cut Digraph

题意：$n$个点个有向图，一开始没有任何边。有$m$次加边操作，每次加完边后求出存在多少对点$(u,v)$使得$u$能够到$v$，$v$也能够到达$u$。

$1 \le \le 10^5, 1 \le m \le 2.5 \times 10^5$

题解：可以发现，我们只需要求出对于每条边$u \to v$，最早什么时候$v$能够到达$u$即可。求出来后，只需要用一个并查集维护连通块即可。

考虑分治，令`solve(l, r, E)`表示考虑当前边集为$E$，这些边最早会在$[l, r]$的某个时间内满足条件。令$m = \frac{l+r}{2}$，我们先对$E$中出现时刻不超过$m$的边求一遍强连通分量，那么就可以知道哪些边会在时刻$m$满足条件。

不妨设可以满足条件的边集为$E_l$，剩下来的边设为$E_r$。可以发现$E_l$里的边最早满足条件的时间肯定要小于等于$m$，$E_r$里的边满足时间肯定大于$m$。$E_r$里那些出现时间大于$m$有些已经满足条件了，这些边其实可以用来缩点。接下来分别调用`solve(l,m,E_l)`和`solve(m+1,r,E_r)`即可。