# Petrozavodsk Winter 2020. Day 5. Jagiellonian U Contest

+ [ ] [A. Bags of Candies](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/A5/)
+ [x] [B. Binomial](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/B5/)
+ [ ] [C. Bookface](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/C5/)
+ [x] [D. Clique](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/D5/)
+ [ ] [E. Contamination](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/E5/)
+ [ ] [F. The Halfwitters](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/F5/)
+ [ ] [G. Invited Speakers](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/G5/)
+ [ ] [H. Lighthouses](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/H5/)
+ [ ] [I. Sum of Palindromes](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/I5/)
+ [ ] [J. Space Gophers](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/J5/)
+ [ ] [K. To argue, or not to argue](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/K5/)
+ [x] [L. Wizards Unite](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/L5/)

## A. Bags of Candies

题解：给出$n$，考虑这样的图：$i$和$j$之间右边当且仅当$\gcd(i,j) > 1$。求出这个图的最大匹配。

$2 \le n \le 10^{11}$

## B. Binomial

题意：给出$n$和树$a_1,a_2,\dots,a_n$。求出有多少对$(i,j)$满足$\binom{a_i}{a_j}$是奇数。

$1 \le n \le 10^6, 1 \le a_i \le 10^6$

题解：$\binom{a_i}{a_j}$是奇数当且仅当他们的二进制表示中$a_i$的每一位都大于等于$a_j$的每一位。这个可以用or卷积求出来。

## C. Bookface

题意：给出$n$个数$c_1,c_2,\dots,c_n$和一个正整数$d$。你每次可以选一个$c_i$，把它加一或者减一，但不能减成负数。求出最小操作次数使得对于所有不同的$i$和$j$都有$|c_i-c_j| \ge d$。

$1 \le n \le 200000, 1 \le d \le 10^6, 0 \le c_i \le 3 \cdot 10^{11}$

题解：先排序成$c_1 \le c_2 \le \dots \le c_n$，显然最终状态他们的相对顺序肯定不变比较好。

## D. Clique

题意：长度为$10^6$的圆周上，有$n$个弧，第$i$条按照顺时针方向从$l_i$到$r_i$。构建这个样一个图：如果弧$i$和弧$j$有交，则他们之间有一条无向边。求出这个图的最大团。

$1 \le n \le 3000$

题解：考虑枚举这个最大团中最短的区间$I$，显然严格在$I$内部我们都不会去选，那些同时包含$I$两个端点的我们一定会选。那么，剩下来的区间要么包含$I$的左端点，要么包含$I$的右端点。假设这两个区间集合分别是$A$和$B$，考虑属于集合$A$的一个区间$a$和属于集合$B$的一个区间$b$。他们俩不能同时选当且仅当以下条件同时成立：

+ $x_a+x_b < |I|$
+ $y_a+y_b < 10^6-|I|$

其中$x_i$表示区间$i$在$I$里的长度，$y_i$表示区间$i$不在$I$里的长度。化简以下就是$x_a < |I| - x_b, y_a < 10^6 - |I| - y_b$。如果把在$A$集合里的区间看成一个二维平面上的黑点$(x_a,y_a)$，把$B$集合里的区间看成一个二维平面上的白点$(|I|-x_b, 10^6-|I|-y_b)$。那么我们就是要选出最多的点，使得不存在一对黑点和白点，黑点坐标严格小于白点坐标。

考虑选出来的白点集合，以及这些白点构成的上边界，这些边界下边一定要是白点，这些边界上面一定要都是黑点，于是我们可以沿着这条上边界dp。考虑按照$x$坐标从大到小处理每个点，令$dp_h$表示这个上边界的$y$坐标不超过$h$的最优值。显然$dp_h$随着h变大也是递增的。

考虑当前如果处理到一个白点$(x,y)$，那么我们可以把满足$y^\prime \ge y$的$dp_{y^\prime}$都加一。如果我们除以到一个黑点$(x,y)$，我们可以把满足$dp_{y^\prime} \le dp_y$的$dp_{y^\prime}$都加一。最后只需要查询$dp_{n-1}$的值即可。显然这些操作可以用线段树维护。

## E. Contamination

题意：给出$n$个圆，圆心在$(x_c,y_c)$，半径为$r$，任意两个无公共点。现在有$q$个询问，每次给出$(p_x,p_y,q_x,q_y,y_{min},y_{max})$，求出能否从$(p_x,p_y)$到达$(q_x,q_y)$，不经过任何一个圆，且行进过程中$y$坐标始终在$[y_{min},y_{max}]$里。

$1 \le n, q \le 10^6, -10^9 \le c_x, c_y \le 10^9, 1 \le r \le 10^9, -10^9 \le p_x,p_y,q_x,q_y,y_{min},y_{max} \le 10^9, y_{min} \le p_y,q_y \le y_{max}$

题解：考虑单组询问，把同时和$y_{min}$和$y_{max}$有交的圆拿出来。由于圆和圆之间没有公共点，那么不能到达的条件就是存在一个圆$(c_x,y_y)$，使得$p_x$和$p_y$在$c_x$的两侧。

那么考虑离线，按照$y$从小到大考虑，维护出当前和$y_{min}$有交的所有圆。用线段树维护$c_x$对应的圆的上边界，如果$[p_x,p_y]$里有上边界大于等于$y_{max}$，那么就是不能走过去。

## F. The Halfwitters

题意：有一个$1$到$n$的排列，你想把它变成$1$到$n$，有以下操作：

+ 交换相邻两个位置，花费$a$分钟
+ 翻转整个序列，花费$b$分钟
+ 搞成一个新的随机排列，花费$c$分钟

求出最优操作下，排好序的期望时间。

$2 \le n \le 16, 1 \le a, b, c \le 1000$

## G. Invited Speakers

题意：给出$n$个黑点和$n$个白点，保证$x$坐标互不相同，$y$坐标互不相同。你需要把他们用$n$条不相交的polyline匹配。构造一组解。

$1 \le n \le 6, -100 \le x_i, y_i \le 100$

题解：一定存在一组解，可以用一条线段连接白点和黑点。

## H. Lighthouses

题解：给出一个$n$个点，他们构成了一个凸包，第$i$个点在$(x_i,y_i)$。有些点之间有边相连。现在以你找出一条最长的简单路径，使得路径不自交。

$3 \le n \le 300, -10^9 \le x_i,y_i \le 10^9$

## I. Sum of Palindromes

题意：给出一个十进制数$n$，把它表示成最多$25$个回文数之和。

$1 \le |n| \le 10^5$

## J. Space Gophers

题意：在一个$10^6 \times 10^6 \times 10^6$的三维立方体里，有$n$条长度为$N$的管道，从一个面打通到对面上。现在有$q$个询问，每次询问能否从只通过管道$(x_1,y_1,z_1)$到达$(x_2,y_2,z_2)$。

$1 \le n \le 300000, 1 \le q \le 500000$

## K. To argue, or not to argue

题意：给出$n \times m$的格子，有些位置被占用了。你需要把$x_1,y_1,x_2,y_2,\dots,x_k,y_k$填入空位置，使得$x_i$和$y_i$不相邻。求方案数，对$10^9+7$取模。

$1 \le nm \le 144, 1 \le k \le \frac{mn}{2}$

题解：考虑容斥，先假设他们没有标号，求出恰好有$j$对相邻的方案数$f(j)$，那么答案就是$2^k \cdot \sum_{j=0}^{k} (-1)^j \cdot \binom{k,j} \cdot f(j) \cdot j! \prod_{r=0}^{k-j-1} \binom{sum-2j-2r}{2}$，其中$sum$表示空位置个数。

然后由于$\min(n,m) \le 12$，$f(j)$可以逐格dp来求出来。

## L. Wizards Unite

题意：有$n$个箱子，第$i$个箱子打开需要时间$t_i$。你有一把金钥匙和$k$把银钥匙，银钥匙用了就没了。金钥匙可以重复利用。不同的钥匙可以同时打开箱子。求出打开所有箱子需要的最小时间。

$0 \le k < n \le 10^5, 0 \le t_i \le 10^9$

题解：显然银钥匙用来打开$t$最大的$k$个。剩下的都用金钥匙打开。