# Petrozavodsk Summer 2015. Day 4. Moscow IPT Contest

+ [x] [A. Rectangle Query]
+ [x] [B. Game With A Fairy]
+ [x] [C. Portkeys]
+ [x] [D. Maximal Common Subpair]
+ [x] [E. k-transpositions]
+ [x] [F. PQ tree]
+ [x] [G. Random Walking]
+ [x] [H. Sasha And Swag Strings]
+ [x] [I. Tree Confrontation]
+ [x] [J. Two Airlines]

## A. Rectangle Query

题意：强制在线。有$n$个点$(x_i, y_i)$。给出$q$个询问，每次求出$x_1 \le x_i \le x_2, y_1 \le y_i \le y_2$的所有点中本质不同的$x$坐标和$y$坐标个数。

$1 \le n,q \le 50000, 0 \le x_i, y_i \le 500000, 0 \le x_1 < x_2 \le 500000, 0 \le y_1 < y_2 \le 500000$

题解：两种询问是对称的，不妨考虑求本质不同的$y$个数。把所有点按照$(x,y)$排序，考虑每个$(x_i,y_i)$预处理出$y_i$上次出现的$x$坐标。

也就是说对于每个$x$，我们有个`std::vector`来表示某个点$(x,y)$的$y$坐标最近一次出现的$x$坐标$last$，然后对这个建立线段树。线段树每个节点，按照$last$排序，然后对$y$建立可持久化线段树。

那么对于询问的话，就是在每个对应的线段树节点上询问$last < x_1$情况下有多少$y$满足$y_1 \le y \le y_2$。二分出对应的位置，然后直接在可持久化线段树询问即可。

## B. Game With A Fairy

题意：有一个长度为$n$的`01`串，保证至少有一个`1`。你可以每次给出一个长度为$n$的`01`串，如果他们做位运算与操作后恰好有一个`1`，那么返回`+`，否则返回`-`。你需要询问最多$200$次使得返回值为`+`。

$n = 10^4$

题解：考虑每次随机$1,2,\dots,2^p$个`1`，可以证明期望$20$次就能询问出`+`。

## C. Portkeys

题意：有$n$个钥匙，你在点$x_i$个时候可以使用这个钥匙，走到任意满足$l_i \le |x_i-y| \le r_i$的$y$处。现在给出$m$个位置$y_i$，求出从$x_1$走到$y_i$最少需要使用的钥匙个数。

$1 \le n, m \le 2 \cdot 10^5, -10^9 \le x_i, y_i \le 10^9, 0 \le l_i \le r_i \le 10^9$

题解：从$x_1$开始BFS，用`std::set`维护哪些点没有被访问过，每次就是取出`std::set`里一个区间里的数。

## D. Maximal Common Subpair

题意：字符串对$(x,y)$是一个串$s$的子串，当且仅当存在字符串$u$和$v$和$w$使得$s=uxvyw$。给出两个字符串$s_1$和$s_2$，你需要找到一对字符串$(x,y)$使得$|x|+|y|$最长，$(x,y)$分别是$s_1$和$s_2$的子串。

$1 \le |s_1|, |s_2| \le 2 \cdot 10^5$

题解：令$s_1=u_1xv_1yw_1$，$s_2=u_2xv_2yw_2$，那么当$v_1$和$v_2$都是空的时候，显然我们仅需要找出$s_1$和$s_2$的最长公共子串即可。接下来假设$v_1$和$v_2$至少有一个非空，不妨令$v_1$非空。

如果我们枚举了$s_1$里某个$y$，可以发现$y$一定是极大的，并且所有极大的出现位置中，我们只关心出现位置最晚的。类似的$x$也是极大的，所有出现位置中，我们只关心出现位置最早的。这个在$s_2$其实也是成立的。

于是，我们可以用SAM预处理出所有可行的$y$以及它在$s_1$和$s_2$中出现的最晚位置，分别记为$(l_y, y_1,y_2)$；对于$x$也可以预处理一下，分别记为$(l_x,x_1,x_2)$。接下来，考虑枚举一个$(l_y, y_1,y_2)$，求出最长的$x$。可以分成两种情况：

+ $x$和$y$在$s_2$中没有交集，那么显然就是要求$x_1+l_x-1 < y_1$和$x_2+l_x-1 < y_2$情况下，$l_x$的最大值。
+ $x$和$y$在$s_2$中有交集，那么显然就是要求$x_1+l_x-1 < y_1$和$x_2 \le y_2 \le x_2+l_x-1$情况下，$y_2-x_2+1$的最大值。

这两种情况都可以对$y_1$和$x_1$做扫描线，然后树状数组维护$x_2+l_x$对应的最值来解决。

## E. $k$-transpositions

题意：给出排列$1,2,\dots,n$，每次可以选择两个数交换位置。求出最多操作$k$次，能够得到多少本质不同的排列。

$1 \le n \le 10^9, 0 \le k \le 3000$

题解：对于一个排列，考虑将其环分解，那么$n$减去环个数就是最少需要的操作次数。因此本题就是求$n$减去环个数不超过$k$的排列个数。

令$dp(i,j)$表示长度为$i$的排列，环分解后恰好有$j$个环并且每个环长度至少是$2$的方案数，那么答案就是$\sum_{i,j} \binom{n}{i} \cdot dp(i,j)$。易得$dp(i,j)=(i-1)(dp(i-1,j)+dp(i-2.j-1))$。

## F. PQ tree

题意：给出$m$个长度为$n$的排列。数有多少本质不同的`PQ tree`可以表示它们。

$1 \le n, m \le 500$

题解：把所有排列重新标号使得第一个排列恰好是$\{1,2,\dots,n\}$。那么可以发现，对于树上任意节点，这个节点对应的子树构成的数在所有$m$个排列里一定是连续的。于是可以先预处理出区间$[i, j]$是否在所有排列里都是连续的。

令$dp(i,j)$表示区间$[i,j]$对应的`PQ tree`的方案数；$P(i,j)$表示区间$[i,j]$构成了一个$P$节点的方案数；$Q_0(i,j)$表示区间$[i,j]$构成了一个$Q$节点，并且这个点恰好有两个子树的方案数；$Q_1(i,j)$表示区间$[i,j]$构成了一个$Q$节点，并且这个点至少有三个子树的方案数。

显然，可以得到如下的转移方程：

$$
dp(i,j)=P(i,j)+Q_1(i,j) \\
Q_0(i, j) = \sum_{k=i}^{j-1} dp(i, k) \cdot dp(k + 1, j) \\
Q_1(i, j) = \sum_{k=i}^{j-1} (Q_0(i,k)+Q_1(i,k)) \cdot dp(k + 1, j) \\
P(i,j)=Q_0(i,j)+\sum_{k=i}^{j-1} P(i,k) \cdot dp(k + 1, j)
$$

当时对于$Q_1(i,j)$转移有一点限制，并不是所有的$k$都是满足条件的。因为$Q$节点要么是顺序要么是逆序，那么对于一个连续区间$[i,k]$，扩展的时候一定也是要么顺序，要么逆序的。

我们需要预处理出$ext(i,k)$表示区间$[i,k]$在每个排列中只能超一个方向扩展的最长距离$j$。只有$j \le ext(i,k)$的$k$才是能够转移的。

具体怎么处理呢，考虑枚举$(i, k)$，然后对于第$x$个排列，如果有$rank(i) < rank(k)$，那么不能扩展到$[i,k]$的左边去，也就是$ext(i,k) \overset{\min}{\leftarrow} \text{perm}(x, \min_{i \le j \le k} \text{rank}(j) - 1) - 1$。否则不能扩展到$[i,k]$的右边边去，也就是$ext(i,k) \overset{\min}{\leftarrow} \text{perm}(x, \max_{i \le j \le k} \text{rank}(j) + 1) - 1$。

## G. Random Walking

题意：给出一棵$n$个点的树，每条边边权是$1$。有$q$个询问，每次询问从$u$到$v$的期望时间：每次会随机选一条边往外走。

$1 \le n \le 10^5, 1 \le q \le 2 \times 10^5$

题解：令$f(v)$表示从$v$走到它父亲$u$的期望时间，那么显然有$f(v)=\frac{1+\sum_{x \in \text{Son}(v)} (1 + f(x)+f(v))}{\text{deg}(v)}$，化简得到$f(v)=\text{deg}(v)+\sum_{x \in \text{Son}(v)} f(x)$.

令$g(v)$表示从$v$的父亲$u$走到$v$的期望时间，同样可以得到$g(v)=\frac{1+(1+g(u)+g(v))+\sum_{x \in \text{Son}(u) \setminus \{v\}}(1+f(x)+g(v))}{\text{deg}(v)}$，化简得到$g(v)=\text{deg}(u)+\sum_{x \in \text{Son}(u) \setminus \{v\}}f(x)$。

对于每个询问，就是先从$u$走到$\text{lca}(u,v)$，然后走到$v$即可。需要处理$f(\cdot)$和$g(\cdot)$的前缀和。

## H. Sasha And Swag Strings

题意：给出$n$个字符串$s_1,s_2,\dots,s_n$。对于每个字符串$s_i$，构建出后缀树，对于后缀树上每条边对应的子串，求出本质不同的子串个数，然后求和。

$1 \le n \le 10^5, \sum |s_i| \le 5 \cdot 10^5$

题解：先建出后缀树，然后扣出每条边对应的区间。最后套用[How Many Substrings?](https://raw.githubusercontent.com/zimpha/problem-editorials/master/miscellaneous/stringology.md)的做法，复杂度$O(n \log^2 n)$。

别解：考虑建立出SAM，然后把除了根节点以外的出度为$1$的点都缩掉，这样得到的叫做CSAM。然后这个东西满足以下性质：

+ trie $\overset{compactation}{\longrightarrow}$ suffix
tree $\overset{minimization}{\longrightarrow}$ CSAM
+ trie $\overset{minimization}{\longrightarrow}$ SAM $\overset{compactation}{\longrightarrow}$ CSAM

然后可以发现CSAM那些compactation后的边集和Suffix Tree的边集是一样的，CSAM边集长度之和是$O(n)$的。

那么只需要枚举每条边，然后用SAM计算出这条边上本质不同子串个数，之后乘上在Suffix Tree中出现次数即可。

枚举CSAM上的节点$v$，它在Suffix Tree上出现次数就是这个节点对应的区间长度。

## I. Tree Confrontation

题意：有一棵$n$个点的树，其中$a$个点被`A`占领了，$b$个点被`B`占领了，保证这$a$个点是连通的，这$b$个点是连通的。对于`A`或者`B`，它可以选择一个自己占领的城市$v$，以及一条路径$P_1,P_2,\dots,P_k$，其中$P_1=v$，$P_2,P_3,\dots,P_{k-1}$都被自己占领，$P_k$没有被任何人占领。然后交换$P_1$和$P_k$状态，即$P_k$被占领，$P_1$不被任何人占领。

对于两个局面如果能够通过上述操作得到，那么则定义为同一个局面。求出有多少本质不同的局面。

$1 \le n \le 200000, 1 \le a, b \le n$

题解：首先可以发现对于任何局面，我们都可以把它们移动成：存在一条边$(u, v)$，$u$所在连通块属于`A`，$v$所在连通块属于`B`。于是我们仅需要判断$(u,v)$的等价类即可。

对于一条边$(u, v)$，它能够到达$(v, x)$当且仅当$x$那一侧的大小至少是$a$。于是可以枚举$v$，然后根据上述条件用并查集维护等价类即可。

别解：不妨假设$a \ge b$，考虑一定会被$a$霸占的节点。如果存在，那么考虑剩余的森林，答案为其中$SIZE \ge b$的连通块个数；否则，答案要么是$1$，要么是$2$，答案为$1$当且仅当存在一个节点，使得中有两颗子树的$SIZE \ge a$，并存在另一棵子树的$SIZE \ge b$。

## J. Two Airlines

题意：交互题。有一个$n$个点的无向完全图，每条边标着`A`或者`W`。你每次可以询问一条边上标记的字符。用不超过$2n$次，找到一条哈密尔顿回路，使得`A`和`W`只切换过一次。

$3 \le n \le 777$

题解：依次加入每个$i$，然后维护`A`和`W`构成的序列。考虑当前分界点是$x$，那么根据边$(x,i+1)$上的字符决定是往$x$左边插入还是右边插入。