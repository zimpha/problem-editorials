# XX Open Cup. Stage 14. Grand Prix of Wroclaw

+ [ ] [A. Boys Don't Cry](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/A/)
+ [ ] [B. The Witcher](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/B/)
+ [ ] [C. What a Sequence!](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/C/)
+ [x] [D. Two Kilers](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/D/)
+ [ ] [E. All in good fun!](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/E/)
+ [ ] [F. Five Nights at Freddy’s](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/F/)
+ [ ] [G. Choreography](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/G/)
+ [ ] [H. Cheat](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/H/)
+ [x] [I. Interest](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/I/)
+ [x] [J. Planet of the singles](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/J/)
+ [ ] [K. Shadow](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/K/)
+ [ ] [L. Boss of all bosses](https://official.contest.yandex.ru/opencupXX/contest/17756/problems/L/)

## D. Two Kilers

题意：给出$n$个数$a_1,a_2,\dots,a_n$。有$q$个操作，每次会把某个位置$a_{p_j}$改成$v_j$。每次操作后，求出$\min(s, k)$，其中$s$是当前`LIS`的长度，$k$是给定的一个数。

$1 \le n, q \le 10^5, 1 \le a_i, v_j \le 10^9, 1 \le p_j \le n, 1 \le k \le 20$

题解：把每个数看上二维平面上一个点$(i,a_i)$。然后维护一个$k$个点集$T_1, T_2, \dots, T_k$。其中点$(i,a_i)$在$T_r$中，当且仅当以$a_i$结尾的LIS长度恰好为$r$。可以发现，如果$s \le k$的话，我们仅需要维护好$T_r$即可，不妨先考虑$s \le k$。一次修改操作可以等价于先从平面中删除一个点，然后再加入一个点。还可以发现，如果把$T_r$里的点按照$x$坐标从小到大排序，那么$y$坐标一定满足$y_1 \ge y_2 \ge \dots \ge y_m$。

先来看看插入操作$(x,y)$，我们可以$r$从$1$枚举到$k$，直到无法在$T_r$中找到一个点$(x^\prime,y^\prime)$使得$x^\prime < x, y^\prime <y$，显然我们需要把$(x,y)$插入到这个$T_r$中。把这个$(x,y)$插入后，你会发现$T_r$会有一些其他点$(x^\prime,y^\prime)$满足$x^\prime > x, y^\prime > y$，我们需要把这些点都插到$T_{r+1}$上去。同样这些点的插入会使得$T_{r+1}$中某些点会插入到$T_{r+2}$中，依次类推直到$T_k$为止。如果我们用`Treap`维护了这个$T_r$，每次其实就是切出`Treap`中一段连续的节点，可以很方便的解决。

然后考虑删除操作，我们可以先找出这个点$(x,y)$属于哪个$T_r$。然后可以发现，删掉$(x,y)$后要从$T_{r+1}$中拿出一段插入到$T_r$中，$T_{r+2}$之后的集合也是类似的。这个显然也可以用`Treap`轻松做到。

接下来考虑$s > k$的情况，我们维护另外一个点集$S$。插入的时候，如果$|T_k| \ne 0$，那么直接把这个点插入到$S$中；否则走上面的插入流程。删除的时候，如果点在$S$里面，直接删除即可；否则先走一遍上面的流程。之后如果$|T_k| = 0$了，我们需要从$S$中拿点出来插入，直到$|T_k| \ne 0$或者$|S| = 0$为止。可以发现这样维护出来的答案肯定也是对的。

## I. Interest

题意：给出$n$个点$m$条边的有向图，保证从$1$可以到其他所有点。对于每个点$i$，求出从$1$出发的两条不相交路径，使得边权和最小。

$1 \le n \le 10^5, 1 \le m \le 10^6$

题解：如果我们只需要求一个点$x$的答案，就是一个跑两次的最小费用最大流，但是直接应用的话会出现负权边。可以考虑用[Suurballe's algorithm](https://en.wikipedia.org/wiki/Suurballe%27s_algorithm)。先用`Dijkstra`求出$1$到所有点的最短路，定义势能$\phi(i)=\text{dist}(1,i)$。然后把每条边的边权$w(u,v)$修改成$w(u,v)+\phi(u)-\phi(v)$。可以发现，这两个图的最短路是等价的，只需要拿新图的最短路加上$\phi(x)$就能得到$1$到$x$最短路。同时还可以发现$1$到$x$最短路上的边的边权都变成了$0$。之后把$1$到$x$最短路上的边取反，然后用`Dijkstra`再跑一边$1$到$x$的最短路即可。

考虑推广这个做法，先求出从$1$出发的最短路树$D$，然后用势能修改边权，可以发现最短路树上的所有边边权都变成了$0$。同样我们从$1$出发开始找最短路，假设当前从堆顶的点是$u$。考虑$u$的所有出边，显然可以分成两类：

+ 不在最短路树$D$上的边$u \to v$：这类边直接用$dist(u)+w(u,v)$来更新$dist(v)$即可。
+ 在最短路树$D$上的边：可以发现从$u$其实可以到达树上任意的节点，并且花费的代价都是$0$，因为树边的边权都是$0$了。考虑把点$u$删掉，那么$u$所在的连通块会分成若干个小连通块。对于横跨不同小连通块之间的边$A \to B$，我们显然是可以用$dist(u) + w(A,B)$来更新$dist(B)$的。所以一个粗暴的做法就是枚举每个新出现的小连通块，以及里面每条横跨边，做一遍更新。但是这样复杂度是$O(n^2)$的。可以发现，如果不遍历最大的连通块，只遍历其他较小的连通块，这样复杂度是有保证的，每条边最多只会被遍历$O(\log n)$次。

如何判定两个连通块的大小呢，可以考虑倍增的方法。倍增枚举较小的连通块的大小为$2^s$，然后两个连通块各自跑$dfs$，要求恰好遍历$2^s$个点。显然，存在一个$s$使得较小的连通块不能遍历$2^s$个点，较大连通块可以遍历$2^s$个点。这个时候我们就区分出大小了。

## J. Planet of the singles

题意：有两个长度为$4n$的`01`串，你可以对第一个串做如下的操作：

1. 把某一个`0`改成`1`，代价是$t_0$
2. 把某一个`1`改成`0`，代价是$t_1$
3. 交换相邻两个位置，代价是$t_s$

求出把第一个串变成第二个串的最小代价。

$1 \le n \le 10^6, 1 \le t_0, t_1, t_s \le 10^{12}$

题解：