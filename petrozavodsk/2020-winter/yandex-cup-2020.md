# Petrozavodsk Winter 2020. Day 4. Yandex Cup 2020

+ [x] [A. Y-Shaped Knife](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/A4/)
+ [x] [B. Bad Doctor](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/B4/)
+ [x] [C. Topological Ordering](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/C4/)
+ [x] [D. Bracket Euler Tour](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/D4/)
+ [x] [E. Tree of Charge](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/E4/)
+ [x] [F. Find a Tree](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/F4/)
+ [x] [G. One Root](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/G4/)
+ [x] [H. Delete the Points](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/H4/)
+ [ ] [I. Hard Times for Your Data](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/I4/)
+ [x] [J. Program](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/J4/)

## A. Y-Shaped Knife

题意：平面上有$n$个点，第$i$个点在$(x_i,y_i)$。你需要把用一个$Y$形的刀把它们分成三个区域，使得每个区域点个数一样。

$1 \le n \le 10^5, -10^6 \le x_i, y_i \le 10^6$

题解：先把所有点按照某个随机角度旋转一下，这样就能保证每个点的$x$坐标互不相同。可以证明，当$n \equiv 0 \bmod 3$的时候一定是有解的。并且一定存在一个$r=0$的解，在旋转后的点上。

考虑枚举竖线$x$，把$x$左边的点按照$-\frac{1}{\sqrt{3}}$的斜率投影到这条直线上，右边的点按照$\frac{1}{\sqrt{3}}$的斜率投影到这条直线上。由于随机，显然每个点的在上面的投影都互不相同。

考虑前$\frac{2n}{3}$个位置，对于一个合法的$x$，其中必有$\frac{n}{3}$来自$x$的左边，$\frac{n}{3}$来自$x$的右边。可以发现，随着$x$从$-\infty$变大到$\infty$，来自$x$左边的点数从$0$逐渐变大到$\frac{2n}{3}$。于是我们可以二分出合法的$x$来。

知道$x$后，直接就可以算出中心点的$y$坐标。之后按照旋转角度转回去即可。

## B. Bad Doctor

题意：有$n$个医生，第$i$个要求你在第$l_i$天到第$r_i$天，每天吃$k_i$种药，$a_1,a_2,\dots,a_{k_i}$。第$j$种药的价格是$c_j$。

对于每个$i$，你需要求出无视第$i$个医生后需要花的钱。同一种药每天只需要吃一片。

$1 \le n, m \le 500000, 1 \le c_j \le 10^6, 1 \le l_i \le r_i \le 10^6, 1 \le k_i \le m, \sum k_i \le 10^6$

题意：每种药可以分开处理，每种药对应了出现的一堆区间，只被覆盖一次的位置删掉后会对答案产生影响。

## C. Topological Ordering

题意：给出$n$个点$m$条边的有向无环图。对于每对$(u,v)$，求出有多少拓扑排序使得$u$在$v$前面。

$1 \le n \le 20, 0 \le m \le \frac{n(n-1)}{2}$

题解：先求出$f(S)$表示这个点集内点构成的拓扑序。然后枚举一个$S$，以及枚举一个$v \not \in S$，和一个$u \in S$，贡献是$f(S) \cdot f(\overline{S} - \{v\})$

## D. Bracket Euler Tour

题意：给出$n$个点$m$条边的无向图，每个点上有个括号。求出一个欧拉回路使得经过的点构成的括号序列合法。有重边，有自环。

$1 \le n, m \le 200000$

题解：先求出一条欧拉回路，如果这条路上括号数目不一致肯定无解，否则一定可以循环移动找到一个合法的起点。

## E. Tree of Charge

题意：给出$n$个点的有根树，$1$是根，每个节点一开始有个值$c_i$。有$q$个操作：

+ Move the charge up：所有节点同时把节点上的值转移给它父亲。也就说如果节点$v$有儿子$u_1,u_2,\dots,u_k$，那么$v$的值会变成$c_{u_1}+c_{u_2}+\dots+c_{u_k}$或者$c_{u_1}+c_{u_2}+\dots+c_{u_k}+c_v$，如果$v$是根的话。
+ Move the charge down：所有节点同时把值转移给它的儿子们。也就说如果节点$v$有儿子$u_1,u_2,\dots,u_k$，那么每个$u_i$的值变成$\frac{c_v}{k}$。
+ Add charge to a vertex：给某个点$v_i$的值加上另一个数$x_i$。

你可以认为每个叶子底下接了无穷长的链。因此down和up执行相同次数的话叶子的值是不变的。

随后输出每个点上的值，对$10^9+7$取模。

$2 \le n \le 500000, 0 \le c_i \le 10^9+6, 1 \le v_i \le n, 0 \le x_i \le 10^9+7$

题解：注意到一个down后面接着一个up的话，其实可以把这两个操作都删掉。也就是说，最终每个节点都是先向上走$c_{up}$次，然后再向下走$c_{down}$次。这个把所有询问倒着做一遍就可以方便求出每个点对应的$c_{up}$和$c_{down}$。

注意到往上走可以直接走，我们不妨直接走到最终节点，接下来需要处理比较麻烦的往下走。假设节点$u$会往下走到一个节点$v$，那么$c_u$对$v$的答案的贡献就是$\frac{c_u}{\prod_{x \in path(u,v)} ChildrenCount(x)}$。

考虑离线DFS整棵树，然后用线段树维护当前栈中节点对深度为$d$的贡献。那么进入这个节点$u$的时候，我们只需要对深度$depth(u)+c_{down}(u)$加上$w(u)$即可。然后询问$depth(u)$在线段树上的值，这个就是当前点$u$的最终答案。

然后进入子树前，把深度在$[depth(u), n]$内的值都乘上$\frac{1}{ChildrenCount(x)}$即可。

离开节点的时候撤销所有操作。


## F. Find a Tree

题意：给出$n$个点$m$条边的无向图，保证图的色数是$k$。然后给出$k$个节点的树，要求找出图中$k$个不同节点$p_1,p_2,\dots,p_k$，使得$u$和$v$是树边的话，$p_u$和$p_v$在图中有边相连。

$1 \le n, k \le 10^6, 0 \le m \le 10^6$

题解：依次考虑$1$到$n$这些点，然后给$i$分配一个最小的未在邻居出现的颜色。那么假设$c(v)=i$的话，那么对于任意$j < i$，都存在一个$u \in N(v)$使得$c(u)=j$。然后给这棵树选一个根，给根标号$k$，其他点用$1$到$k-1$标号，只要父亲标号大于儿子即可。然后在图中选一个$c(u)=k$的点$u$和根对应，然后可以发现根的儿子一定可以和$u$的某个邻居对应，然后依次dfs下去即可。

## G. One Root

题意：给出$n$和$m$，求出有多少$p$和$q$，满足$|p| \le m$，$|q| \le m$并且$x^n+px+q=0$恰好有一个实数根，

$1 \le n, m \le 10^6, n \ge 2$

题解：令$f(x)=x^n+px+q$，考虑$f^\prime(x)=nx^{n-1}+p$，分$n$的奇偶性讨论。

+ $n$是偶数，那么$f^\prime(x)=0$解只有一个$x=(-\frac{p}{n})^{\frac{1}{n-1}}$。根据单调性，只有$f((-\frac{p}{n})^{\frac{1}{n-1}})=0$这种情况。化简后得到$q=-(-\frac{p}{n})^{\frac{1}{n-1}} \cdot (p-\frac{p}{n})$。枚举$p$，然后用`long double`计算出$q$即可。
+ $n$是奇数，那么当$p < 0$的时候$f^\prime(x)=0$有两个解$x=\pm (-\frac{p}{n})^{\frac{1}{n-1}}$，否则有一个解$0$或者无解。可以发现$p \ge 0$的时候，任意$q$都存在一个实根。令$y=-(-\frac{p}{n})^{\frac{1}{n-1}} \cdot (p-\frac{p}{n})$，那么有$|q| \ge y$。用`long double`计算出$y$，然后就可以求出$q$的范围了。

## H. Delete the Points

题意：平面上有$n$个点，$n$是偶数。每次可以选个两个点，然后话一个正方形仅包含这两个点，然后删掉他们。求出能否删掉所有的点。并输出方案。

$1 \le n \le 3000, 0 \le x_i, y_i \le 10^9$

题解：显然每次操作都是可以删掉$2$个点的。从$y$最大的开始，分若干种情况删即可。

## I. Hard Times for Your Data

题意：有$n$个节点，每个节点容量为$f_i$。现在有$m$组文档，表示在$u_i$和$v_i$上各存了$c_i$份文档。现在你需要删掉一些文档，使得每个节点存储的文档数目恰好为$f_i$。

$1 \le n \le 500, 0 \le m \le \frac{n(n-1)}{2}$

题解：据说是这篇论文：[Maximum Skew-Symmetric Flows and Matchings](https://arxiv.org/abs/math/0304290)

## J. Program

题意：有一个变量$X$，一开始为$1$。有$n$个操作

+ 把$X$的值改成$p$
+ 如果$X$的值为$p$，那么把$X$的值改成$q$。

你可以删掉一些操作，对于每个$k=1,2,\dots,n$，求出最少删掉几个操作才能使得$X$最后的值为$k$。

$2 \le n \le 10^6, 1 \le p, q \le n, p \ne q$

题解：令$dp(i)$表示一个操作后$X=i$的最小删除次数，显然

+ 对于第一种操作，$dp(p)=0$，其他的dp值都要加一
+ 对于第二种操作，$dp(q)=\max(dp(q), dp(p))$，$dp(p)$要加一

用树状数组维护一个每个dp值得加标记，用得时候把标记加到dp值上并清空即可。