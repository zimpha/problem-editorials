# Petrozavodsk Winter 2020. Day 3. 300iq Contest 3

+ [x] [A. Airplane Cliques](https://codeforces.com/gym/102538/problem/A)
+ [x] [B. Best Tree](https://codeforces.com/gym/102538/problem/B)
+ [x] [C. Cells Blocking](https://codeforces.com/gym/102538/problem/C)
+ [x] [D. Disjoint LIS](https://codeforces.com/gym/102538/problem/D)
+ [x] [E. Easy Win](https://codeforces.com/gym/102538/problem/E)
+ [x] [F. Farm of Monsters](https://codeforces.com/gym/102538/problem/F)
+ [x] [G. Giant Penguin](https://codeforces.com/gym/102538/problem/G)
+ [x] [H. Horrible Cycles](https://codeforces.com/gym/102538/problem/H)
+ [x] [I. Ignore Submasks](https://codeforces.com/gym/102538/problem/I)
+ [x] [J. Just Counting](https://codeforces.com/gym/102538/problem/J)

## A. Airplane Cliques

题意：给出$n$个点的树，树上两点距离如果不超过$x$，那么连一条边。对于每个$k$，输出有多少大小为$k$的团，对$998244353$取模。

$1 \le n \le 300000, 0 \le x \le n - 1$

题解：随便选个根做一遍DFS，令$depth_v$是点$v$的深度。可以发现对于点$u$，那些满足$depth_v \le depth_u$并且$dist(u,v) \ge x$的点一定构成了一个团。也就是说，对于一个团，我们可以选取$depth$最大的点作为代表，如果有多个，可以选标号最大的。因此我们可以先用树分治求出$a_u$表示有多少点$v$，满足$depth_v < depth_u$或者$depth_v = depth_u \text{ and } v < u$，同时$dist(u,v) \le x$。那么对于一个$k$，答案就是$\sum_u \binom{a_u}{k-1}$。

不妨令$c_x$是$a_u=x$的$u$的个数，那么对于一个$k$答案是$\sum_x c_x \cdot \binom{x}{k-1}=\frac{c_x \cdot x! \cdot \frac{1}{(x - (k - 1))!}}{(k-1)!}$。其实就是$c_x \cdot x!$和$\frac{1}{(n-1-x)!}$的卷积。

## B. Best Tree

题意：给出一棵树的度数序列$d_1,d_2,\dots,d_n$，求出一棵最大匹配最大的树。

$2 \le n \le 200000, 1 \le d_i \le n - 1, \sum d_i = 2(n-1)$

题解：答案是$\min(\lfloor \frac{n}{2} \rfloor, \sum_{i=0}^{n} [d_i > 1])$。

## C. Cells Blocking

题意：给出$n \times m$的格子，有些位置是障碍物。现在你可以放入两个新的障碍物，使得只向右或者向下不能从$(1,1)$走到$(n,m)$，求方案数。

$1 \le n, m \le 3000$

题解：先求出$from_{x,y}$表示$(1,1)$能否到达$(x,y)$以及$to_{x,y}$表示从$(x,y)$能否到达$(n,m)$。然后求出两条从$(1,1)$到$(n,m)$的路径，一条尽量往下走，一条尽量往右走，分别记为$path_{down}$和$path_{right}$。那么两条路径重合部分就是能够只用一个障碍物阻挡的放法。只要选了这些的某个位置，那么剩下一个障碍物可以随便放。

接下来考虑选其他位置，那么这个位置肯定在一条路径上，不妨令它在$path_{down}$上。假设选取位置为$(x,y)$，我们需要找一个最小的$i$使得$(x-i,y+i)$能够到达$(n,m)$且能被$(1,1)$到达。那么从这个$(x-i,y+i)$开始我们就能获得新的$path^\prime_{down}$。同时也可知道和$path_{right}$的重合部分。

## D. Disjoint LIS

题意：给出$n$，求出有多少长度为$n$的排列，满足存在两个不相交的最长上升子序列。

$1 \le n \le 75$

题解：考虑一个排列$(p_1,p_2,\dots,p_n)$插入一个杨表的过程。我们按照$p_i$的值维护一个杨表$P$，可以注意到每次插入都会多出恰好一个格子$s$。那么如果，我们同时也维护另一个杨表$Q$使得$P$和$Q$形状一样，并且把$i$填入到$s$中。那么一个排列就对应了一对杨表$(P,Q)$并且$P$和$Q$形状一样。然后可以证明一对形状一样的杨表$(P,Q)$一定可以还原出一个排列。每次删掉$Q$中最大的数，同时也删掉$P$中对应位置。

于是我们可以枚举所有总大小为$n$，且前两行长度一样的杨表$\lambda$。那么答案就是$\sum_{\lambda} f^2(\lambda)$，其中$f^2(\lambda)$可以用钩子公式计算。

## E. Easy Win

题意：有$n$堆石子$a_1,a_2,\dots,a_n$。两个人玩游戏，每次选一堆取走最多$x$个石子。对于每个$1 \le x \le n$，求出先手必胜还是必败。

$1 \le n \le 500000, 1 \le a_i \le n$

题解：考虑$sg(x, n)$表示大小为$n$的石子，每次最多取$x$的sg函数值，显然$sg(x,n)=n \bmod (x + 1)$。

考虑每个$x$，然后令$y=x+1$，那么对于每个$k$，区间$[ky, ky+y)$里的数可以一起统计。枚举$b$，统计区间$[ky, ky+y)$里有多少数$t$满足$t-ky$二进制表示的第$b$位为$0$。显然这样的$t$，一定在区间$[ky+2^b,ky+2^{b+1}), [ky+2^{b+1}+2^b, ky+2 \cdot 2^{b+1}),\dots,[ky+s \cdot 2^{b+1}+2^b,ky+(s+1) \cdot 2^{b+1})$这些区间里。

预处理数组$cnt_x$表示$a$里大于等于$x$数的个数，然后令$sum_x=sum_{x+2^{b+1}}+cnt_{x+2^b}-cnt_{x+2^{b+1}}$。我们就能求出$a$里面大于等于$x$的且减去$x$后二进制第$b$位是$1$的个数。

对于一个$[ky,ky+y)$区间的询问，完整包含一个$[ky+s \cdot 2^{b+1}+2^b,ky+(s+1) \cdot 2^{b+1})$区间的答案就是$sum_{ky}-sum_{ky+\lfloor \frac{y}{2^{b+1}} \rfloor \cdot 2^{b+1}}$。剩下来还有一些零头需要统计，也就是区间$[ky+\lfloor \frac{y}{2^{b+1}} \rfloor \cdot 2^{b+1}+2^b, ky+y)$，利用$cnt$数组就可以算出来。

## F. Farm of Monsters

题意：有$n$只怪，第$i$只血量为$h_i$。你和你对手轮流打怪，你可以造成$a$点伤害，你的对手可以造成$b$点伤害。你每次可以任意选择一个怪打，你的对手会每次选择还活着的，标号最小的怪打。求出你最多能打死几只怪。

$1 \le n \le 300000, 1 \le a, b \le 10^9, 1 \le h_i \le 10^9$

题解：显然对于第$i$只怪，对手打死它需要$\lfloor \frac{h_i-1}{b} \rlfoor + 1$下，而如果你决定要打死这个怪，你只需要打它$\lfloor \frac{(h_i-1) \bmod b}{a} \rlfoor + 2$下。

于是你可以用个优先队列维护你打死的怪的次数，以及你当前还剩余的次数。如果当前剩余次数够，肯定直接用这些次数打即可。否则你可能会替换出优先队列一只怪，使得剩余次数变得尽可能大。

## G. Giant Penguin

题意：给出$n$个点$m$条边的无向连通图，保证每个点最多属于$k$个简单环。有$q$个操作，要么标记一个点$v$；要么询问距离点$v$最近的被标记的点。

$1 \le n \le 100000, n - 1 \le m \le 200000, 0 \le k \le 10, 1 \le q \le 200000$

题解：考虑随便选一个生成树树分治。由于每个点最多属于$k$个简单环，那么对于一个分治重心，横跨不同子树的边最多只有$k$条。也就是说加上分治重心，最多只有$2k+1$个特殊点。考虑从这些特殊点开始求出到其他点的最短路，然后更新操作就维护距离特殊点最近的被标记的点。查询的话，就枚举每个特殊点作为中间点即可。

## H. Horrible Cycles

题意：有一个二分图，左边和右边各$n$个点。左边第$i$个点会和右边$1,2,\dots,a_i$这些点连边。求出图中简单环个数，对$998244353$取模。

$1 \le n \le 5000, 1 \le a_i \le n$

题解：考虑按照$a_i$从小到大排序。这样每个右边点$i$能够连的边一定包括点$i-1$能够连的边。令$dp(i,j)$表示右边点处理到点$i$，总共构成了$j$条链的方案数，其中要求这些链的起点和终点都是左边的点。那么考虑$i+1$加入后会发生什么

+ 多出了$k=a{i+1}-a_{i}$个左边点，这些点可以选作为孤立点，以后会成为链的一部分。可以用一个$O(k)$的转移搞定。
+ 第$i+1$个点可以连接其中两条链，变成一条链；也可以不做任何操作，丢掉这个点；如果当前只剩一条链，还可以构成一个环。

最后我们会发现除去两个点的二元环，其他环都算了两遍。

## I. Ignore Submasks

题意：给出$n$个数$a_1,a_2,\dots,a_n$。令$f(x)$表示最小的$i$，使得$a_i \text{ AND } x \ne a_i$；没有的话值为$0$。求出$f(1)+f(2)+\dots+f(2^k_1)$，对$998244353$取模。

$1 \le n \le 100, 1 \le k \le 60, 0 \le a_i < 2^k$

题解：枚举$f(x)=i$，那么$x$至少是$a_1 \text{ OR } \dots \text{ OR } a_{i-1}$。然后考虑$a_i$哪一位$1$和$x$不一致，后面的都可以随便填。

## J. Just Counting

题意：给出$n$个点$m$条边的无向图，没有重边和自环。你需要给每条边标上$0$到$4$的一个整数，使得对于每个点，和它相连的边权和是$5$的倍数。求出方案数，对$998244353$取模。

$1 \le n \le 200000, 0 \le m \le 300000$

题解：每个连通分量可以分别考虑。如果连通分量是二分图，那么方案数是$5^{m-n+1}$，否则方案数是$5^{m-n}$。
