# XX Open Cup. Stage 5. Grand Prix of Korea

+ [ ] [A. 6789](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/A/)
+ [ ] [B. Bigger Sokoban](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/B/)
+ [ ] [C. Cleaning](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/C/)
+ [ ] [D. Container](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/D/)
+ [ ] [E. Dead Cacti Society](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/E/)
+ [ ] [F. Hilbert's Hotel](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/F/)
+ [ ] [G. Lexicographically Minimum Path](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/G/)
+ [ ] [H. Maximizer](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/H/)
+ [ ] [I. Minimal Diameter Spanning Tree](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/I/)
+ [ ] [J. Parklife](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/J/)
+ [x] [K. Wind of Change](https://official.contest.yandex.ru/opencupXX/contest/14556/problems/K/)

## A. 6789

题意：给出$n \times m$的矩阵，每个元素都是`6`, `7`, `8`或者`9`，求最少翻转几张牌使得这个矩阵旋转$180^{\circ}$后不变。

$1 \le n, m \le 500$

## B. Bigger Sokoban

题意：构造一个推箱子的$n \times m$的格子，每个箱子大小都是$2 \times 2$，使得至少需要$40000$才能解决。仅包含一个箱子和一个终点。

$1 \le n, m, n + m \le 100$

## C. Cleaning

题意：给出$n \times m$的格子，每个上面写着`L`, `R`, `U`或者`D`，表示上下左右。你在一个格子上的时候，可以自由移动到相邻位置，但是不能沿着格子上标记的方向走。给出$q$个询问，每次给出一个起点和终点，询问可能经过的格子的数目。

$1 \le n, m \le 1000, 1 \le q \le 300000$

## D. Container

题意：有两个长度为$n$个数组$s$和$t$，每个元素要么是`1`，要么是`2`。每次可以选择连续两个或者三个位置翻转下，代价是元素之和加上$c$。求最小代价从$s$变成$t$。

$1 \le n \le 500, 0 \le c \le 1000$

题解：如果我们仅考虑处理`2`的情况，那么当`2`位置都匹配之后，`1`自然也都匹配了。假设`2`在$s$中位置依次是$p_1,p_2,\dots,p_m$，最终被交换到了$q_1,q_2,\dots,q_m$，那么代价其实是可以直接算出来的
$$
\sum_{i=1}^{m} \lfloor \frac{d_i}{2} \rfloor \cdot (c+1+1+2) + (d_i \bmod 2) \cdot (c+1+2) + \sum_{1 \le i < j \le m} [q_i > q_j]
$$

其中$d_i=|p_i-q_i|$。

还可以发现，对于$p_i$奇偶性一样的那些$q_i$，肯定是递增的，因为不递增肯定没有好处。因此，我们可以按顺序dp每个$q_i$分配给奇数$p_i$或者偶数$p_i$。

令$dp(a, b)$表示分配了$a$个$q_i$给奇数的$p_i$，$b$个$q_i$给偶数的$p_i$。转移的话，第一个求和部分很好计算。对于逆序对部分，显然奇偶性一样的事不会产生逆序对的，仅需要考虑奇偶性不同的。可以简单的预处理一个前缀和就算出逆序对的数目。

对于输出方案的话，我们可以先根据dp值还原出$q_1,q_2,\dots,q_m$。接下来可以发现，操作之间有顺序关系。因此可以构建一个有向图，求出拓扑排序后，根据拓扑排序操作即可。

## E. Dead Cacti Society

题意：给出一个$n$个点$m$条边的仙人掌，每个点有个属性$RV_i$，每条边长度为$L_i$，也有个属性$RE_i$。你可以从每个简单环里选一条边从中间砍断，然后对于一条砍断的边$(u,v)$，$u$会连出一条长度为$RV_u+RE_{u,v}$的边，$v$会连出一条长度为$RV_v+RE_{u,v}$的边。最后会得到一棵树。找出一种砍法，最小化树的直径。

$3 \le n \le 10^5, n \le m \le 150000, 0 \le RV_i \le 10^9, 1 \le L_i, RE_i \le 10^9$

题解：考虑二分答案$D$，你需要判定是否存在一组划分使得直径不超过$D$。考虑把仙人掌分解成环+边。

然后从$1$开始进行树DP，维护$d(u)$表示从节点$u$往下最长路的最小值。遍历到边的话按照普通树方法DP即可。遍历到环的话，把环上点先都处理好。然后从环的入点开始在环上往前和往后处理下算出最长距离即可，之后把前后合并下。

## F. Hilbert's Hotel

题意：有一个无穷长的数组$a$，一开始都是$0$，还有个全局变量$g$，一开始是$1$。有$q$个操作，每个都是以下三种：

+ $1\ k$：如果$k \ge 1$，那么对于每个$x$，先令$a_{x+k} \leftarrow a_x$，然后把前$k$个位置填上$g$；如果$k=0$，那么对于每个$x$，先令$a_{2x} \leftarrow a_x$，然后把所有奇数位置填上$g$。最后令$g \leftarrow g+1$。
+ $2\ g\ x$：询问所有$a_i=g$里面，第$x$小的$i$，对$10^9+7$取模
+ $3\ x$：询问$a_x$的值

$1 \le q \le 300000, 0 \le k \le 10^9, 0 \le x \le 10^9$

## G. Lexicographically Minimum Path

题意：给出一个$n$个点$m$条边的有向图，每条边上有个标号$c_i$。对于所有从$s$到$t$长度不超过$10^{100}$的路径，求出字典序最小的那条。

$1 \le n \le 100000, 0 \le m \le 300000, 1 \le s, t \le n, 1 \le c_i \le 10^9$

## H. Maximizer

题意：给出两个长度为$n$的排列$a_1,a_2,\dots,a_n$和$b_1,b_2,\dots,b_n$。你可以交换$a$里面相邻两个元素。求出最小交换次数，使得$\sum_{i=1}^{n}|a_i-b_i|$最大。

$1 \le n \le 250000$

## I. Minimal Diameter Spanning Tree

题意：给出$n$个点$m$条边的带权无向图，求出最小直径生成树。

$2 \le n \le 500, n-1 \le m \le \frac{n(n-1)}{2}$

## J. Parklife

题意：数轴上有$10^6$个整点，给出$n$个区间，第$i$区间是$[s_i,e_i]$，价值为$v_i$。对于每个$k$，选出一些区间，使得每个点最多被覆盖$k$次，且价值和最大。

$1 \le n \le 250000, 1 \le s_i < e_i \le 10^6, 1 \le v_i \le 10^9$

## K. Wind of Change

题意：给出两棵$n$个点的树，对于每个$i$，求出$\min_{j \ne i} dist(T_1,i,j)+dist(T_2,i,j)$。

$2 \le n \le 250000$

题解：考虑分别对两棵树树分治，那么对于一个$i$，它在$T_1$中属于$O(\log n)$个重心，记为$r_1，在T_2$中也属于$O(\log n)$个重心，记为$r_2$。也就是说对于一个$i$只有$O(\log^2 n)$重方案。

对于每个$(i, r_1,r_2)$，如果我们能找到一个$j$，使得$j$在$T_1$中属于重心$r_1$，在$T_2$中属于重心$r_2$，并且$i$和$j$不在同一棵子树内，并且$dist(T_1,i,r_1)+dist(T_2,i,r_2)+dist(T_1,j,r_1)+dist(T_2,j,r_2)$最小，那么我们就解决了这个问题。

但是上面条件过于强，不妨放缩成$i$和$j$可以在同一棵子树里。那么显然求出来的也是我们想要的答案，因为如果$i$和$j$在同一棵子树里，那么一定存在另外一对$(r_1^\prime,r_2^\prime)$，上面的值更小。

接下来只需要对每对$(r_1,r_2)$维护$dist(T_1,i,r_1)+dist(T_2,i,r_2)$的最小值，以及次小值就好了。对于一个$i$，我们枚举$(r_1,r_2)$，然后在最小值和次小值中找不是$i$的那个，相加取最小。

注意下枚举顺序的话，空间复杂度可以做到$O(n \log n)$的，时间复杂度$O(n \log^2 n)$。

还存在$O(n \log n)$的做法，考虑只对$T_1$树分治。对于每个$(i, r_1)$，我们要在$r_1$的子树下找一个和$i$不同的$j$，使得$dist(T_1,i,r_1)+dist(T_1,j,r_1)+dist(T_2,i,j)$最小。

我们把$r_1$子树下的所有节点抠出来对$T_2$建立一棵虚树，那么这个最小值可以dp出来。
