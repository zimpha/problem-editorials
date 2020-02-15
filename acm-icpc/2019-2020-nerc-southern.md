# 2019-2020 ICPC, NERC, Southern and Volga Russian Regional Contest

+ [x] [A. Berstagram](https://codeforces.com/contest/1250/problem/A)
+ [x] [B. The Feast and the Bus](https://codeforces.com/contest/1250/problem/B)
+ [x] [C. Trip to Saint Petersburg](https://codeforces.com/contest/1250/problem/C)
+ [ ] [D. Conference Problem](https://codeforces.com/contest/1250/problem/D)
+ [x] [E. The Coronation](https://codeforces.com/contest/1250/problem/E)
+ [x] [F. Data Center](https://codeforces.com/contest/1250/problem/F)
+ [ ] [G. Discarding Game](https://codeforces.com/contest/1250/problem/G)
+ [ ] [H. Happy Birthday](https://codeforces.com/contest/1250/problem/H)
+ [ ] [I. Show Must Go On](https://codeforces.com/contest/1250/problem/I)
+ [ ] [J. The Parade](https://codeforces.com/contest/1250/problem/J)
+ [ ] [K. Projectors](https://codeforces.com/contest/1250/problem/K)
+ [ ] [L. Divide The Students](https://codeforces.com/contest/1250/problem/L)
+ [ ] [M. SmartGarden](https://codeforces.com/contest/1250/problem/M)
+ [ ] [N. Wires](https://codeforces.com/contest/1250/problem/N)

## A. Berstagram

题意：一开始有个长度为$n$的数组$[1,2,\dots,n]$。给出$m$个数$a_1,a_2,\dots,a_m$，对于每个$a_i$，把$a_i$在数组中的位置往前移动一个（如果是第一个则不动）。对于每个$1 \le i \le n$，求出它在数组中最小和最大位置。

$1 \le n \le 10^5, 1 \le m \le 4 \times 10^5$

题解：可以拿Treap暴力模拟。

## B. The Feast and the Bus

题意：有$k$个团队，总共$n$个人。第$i$个人属于第$t_i$个团队。现在需要租一个巴士，每次可以带上一个团队或者两个团队的人。假设巴士容量是$s$，需要$r$次才能载完所有人，那么花费为$rs$。求最小花费。

$1 \le n \le 5 \times 10^5, 1 \le k \le 8000$

题解：枚举$s$，然后贪心即可。

## C. Trip to Saint Petersburg

题意：给出$n$个区间，第$i$个区间为$[l_i,r_i]$，代价为$p_i$。给出$k$，你需要选出一个$L$和$R$，满足$L \le R$，且$\sum\limits_{i=1}^{n}[L \le l_i \le r_i \le R]p_i - k(R-L+1)$的值最大。

$1 \le n \le 2 \times 10^5, 1 \le l_i \le r_i \le 2 \times 10^5, 1 \le p_i, k \le 10^{12}$

题解：把区间按照右端点排序，然后用线段树维护左端点为$x$时的值，每次就是对一个前缀加一个数，以及前缀取最值。

## D. Conference Problem

题意：给出$n$个区间，第$i$个区间为$[l_i,r_i]$，有一个标号$c_i$，如果$c_i=0$，那么它的标号未定。现在，你需要给$c_i=0$的那些区间分配标号，使得这样的区间个数最多：和这个区间有交的区间标号都和它一样。

$1 \le n \le 500, 1 \le l_i \le r_i \le 10^6, 0 \le c_i \le 200$

## E. The Coronation

题意：给出$n$个长度为$m$的`01`串。两个`01`串是`similar`当且仅当至少有$k$个位置一样。现在你可以翻转某些串，使得任意两个串都是`similar`。求出最小翻转次数。

题解：对于两个串$p$和$q$，如果$p$和$q$，$p$和$rev(q)$都`similar`那么他们之间连一条白边，如果仅有一对满足，那么连一条黑边。对于一个连通块，只要有一个点状态定了，其他点的状态都定了。之后检查下状态是否合法，以及对于每个连通块挑最少翻转的状态即可。

## F. Data Center

题意：给出面积为$n$的矩形，求最小周长。

$1 \le n \le 200000$

题解：略

## G. Discarding Game

题意：给出$n$对数$(a_i,b_i)$，有A和B两个人一开始都是$0$分。然后，第$i$次两人分数分别加上$a_i$和$b_i$。超过$k$分的人输，每轮结束后，A可以选择重置分数，假设A的分数为$x$，B的分数为$y$，那么A的变为$\max(0,x-y)$，B的变为$\max(0,y-x)$。求出A要获胜最少需要重置几次分数。

$1 \le n \le 200000, 2 \le k \le 10^9, 1 \le a_i, b_i < k$

## H. Happy Birthday

题意：数字$0$到$9$里面，数字$i$有$c_i$个。求出最小的不能被拼成的数。

$0 \le c_i \le 10^5, \sum c_i \le 10^6$

## I. Show Must Go On

题意：给出$n$个数$a_1,a_2,\dots,a_n$。把所有子集按照(子集大小，$a_i$的和)从大到小排序，选出前$m$个$a_i$的和不超过$k$的。并输出最后一个子集里面的元素。

$1 \le n, m \le 10^6, 1 \le k \le 10^{18}, 1 \le a_i \le 10^{12}$

## J. The Parade

题意：有$n$类数，第$i$类有$c_i$个。你需要把这些数排成$k$行，每行长度一样，并且每行里面的数的类别之差不超过$1$。求出最多能选出多少数。

$1 \le n \le 30000, 1 \le k \le 10^{12}, 0 \le c_i \le 10^{12}$

## K. Projectors

题意：有$n$个类型$1$区间$[a_i,b_i)$和$m$个类型$2$区间$[p_j,q_j)$，你需要把这些区间划分成最多$x+y$组，使得每组里面区间互不相交，且包含类型$1$的组数不超过$x$。

$0 \le n, m, x, y \le 300, n + m > 0, x+y > 0, 1 \le a_i < b_i \le 10^6, 1 \le p_j < q_j \le 10^6$

## L. Divide The Students

题意：有$a$和汇编爱好者，$b$个Basic爱好者，$c$个C++爱好者。你需要把这些人分成三组，使得每组里面都不能同时存在汇编和C++爱好者。求出最大组的大小的最小值。

$1 \le a,b,c \le 1000$

## M. SmartGarden

题意：一个$n \times n$的格子，主对角线以及主对角线下方并且和主对角线相邻的格子都是非法的。现在你需要用不超过$50$个子矩形（可以不连续）覆盖所有合法点，要求不能覆盖到非法点。每个子矩形用$r$个行号和$c$个列号描述，这些行列的交点会被覆盖。

$2 \le n \le 5000$

## N. Wires

题意：数轴上有$1$到$10^9$个点，有$n$条线连接其中不同的两个点。你可以改变某条线的某个连接端点，使得所有线都连通。求最小次数。

$1 \le n \le 10^5, 1 \le x_i, y_i \le 10^9$
