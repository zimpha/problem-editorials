# Petrozavodsk Winter 2020. Day 1. SPb SU Contest

+ [x] [A. Bijection]
+ [x] [B. Rectangle Tree]
+ [x] [C. Integer Cow]
+ [x] [D. Lost in Transfer]
+ [ ] [E. Maze with a Hint]
+ [x] [F. Maharajas are Going Home]
+ [x] [G. Ook]
+ [x] [H. Pi Approximation]
+ [x] [I. Partition of Queries]
+ [ ] [J. Random Chess Game]
+ [x] [K. What? Subtasks? Again?]
+ [ ] [L. The Five Bishops]

## A. Bijection

题意：通信题。给出$n$，要把从$(0,0)$出发只能往上或者往右到达$(n,n)$的路径和长度为$2n$的合法括号序列外加$0$到$n$的整数建立一一映射。

$1 \le n \le 300$

题解：可以考虑按照字典序排序，然后一一对应起来，需要写个高精度。

## B. Rectangle Tree

题意：给出一个$n \times n$的格子，每个格子上有个整数$a_{i,j}$。定义`combinatorial rectangle`是这个格子的一个子矩形$A \times B$，$A, B \subseteq \{0,1,\dots,n-1\}$。定义`rectangle tree`是一个二叉树，每个节点$v$是一个`combinatorial rectangle` $r(v) \subseteq \{0, 1, \dots, n-1\} \times \{0, 1, \dots, n-1\}$。对于每个内部节点$s$，它一定有两个儿子$c_1$和$c_2$，并且$r(s)=r(c_1) \cup r(c_2), r(c_1) \cap r(c_2) = \empty$。

一个对于`rectangle tree`被称为好的，当且仅当$r(root)=\{0,1,\dots,n-1\} \times \{0,1,\dots,n-1\}$并且对于每个叶子节点$l$，每个$r(l)$的格子上的整数都是一样的。

现在给出一个大小为$S$的好`rectangle tree`，构造另一个好的`rectangle tree`，使得深度不超过$3 \log_2 S$，大小不超过$5S$。

$1 \le n \le 1000, 1 \le a_{i,j} \le 10^7, 1 \le S \le 10000, nS \le 10^6$

题解：分治，每次选个点$C$，满足$size(C) \ge N / 3$，$size(left(C)) \le N / 3$并且$size(right(C)) \le N / 3$。这样可以分成三个子树继续做，需要把无用的分支砍掉。

## C. Integer Cow

题意：有一个圆心在$(x_c,y_c)$，半径为$r$的圆。然后给出一个点$(x_0, y_0)$，在圆内找个整点距离它最近。

$-10^9 \le x_0, y_0, x_c, y_c \le 10^9, 1 \le r \le 10^9$

题解：求出线段$(x_0,y_0)$和$(x_c,y_c)$在圆周的交点$M$，然后暴力在附近枚举一下，坐标$\pm 10^5$就够了。

## D. Lost in Transfer

题意：通信题。有$n$个不同的数$a_1,a_2,\dots,a_n$。你要把这$n$个数传输给另一个人，传输过程中最多会有一个数丢失。你要设计一个传输协议，使得另一个人能够恢复出这$n$个数。

$20 \le n \le 100, 1 \le a_i \le 500$

题解：先求出这$n$个数的异或和，那么最大是$511$。我们可以用一个长度为$6$的permutation来加密它。考虑把所有数排序，前$6$个顺序，接下来$6$个逆序，依次类推。然后每$6$个用刚才那个permutation做一次变换。这个序列作为输出的序列。

解密的时候就先特判下没有丢数的情况。之后枚举这个数在哪一个大小为$6$的block丢掉了。然后可以求出剩下没丢数的block对应的排列，看看是否一致即可。一致的话就找到了异或和，自然就能求出丢掉的数。

## E. Maze with a Hint

题意：通信题。有一个$n \times n$的迷宫，入口是左下角，出口是左上角。你可以根据迷宫信息编码一个长度不超过$1000$的`01`串。然后从入口开始进行交互，要到达出口。每次会给出以当前点为中心的$3 \times 3$的迷宫片段，你需要输出下一步往哪里走。或者判定到达了出口，然后退出。要求不能超过$6000$步。

$5 \le n \le 200$

题解：考虑应用左手规则，唯一不能确定的地方是十字路口，加密这些十字路口的信息即可。

## F. Maharajas are Going Home

题意：有一个左下角在$(1,1)$的无限大棋盘。其中$k$个位置$(r,c)$有棋子，每次可以往左，或者往下，或者沿着对角线方向，或者走马的步，不能动的人输。求出先手的策略。

$1 \le k \le 10, 1 \le r, c \le 2000$

题解：预处理sg函数，每次处理$r-c$一样的副对角线，同时用bitset维护行，列，主对角线出现过的sg值。求一个位置的sg值的话，就是这三个bitset搞一下，然后马字特判下。

## G. Ook

题意：有一个包含`o`和`k`的字符串$s$，`o`的价值为$o$，`k`的价值为$k$。还有个包含`o`，`k`和`?`的字符串$p$。对于每个长度为$|p|$的位置，代价为价值和除以$2$的不匹配数次方，取下整。选出$s$若干个不相交的，长度为$|p|$的子串，使得代价和最大。

$1 \le |p|, |s| \le 250000, 1 \le o, k \le 1000$

题解：先用FFT求出每个位置不匹配的数目，然后dp即可。

## H. Pi Approximation

题意：对于一个$n$，令$f(n)$表示边长不超过$n$的`primitive Pythagorean triples`个数。然后用$\frac{f(n)}{n}$来近似$\frac{1}{2 \pi}$。现在给一个$n_{min}$和$n_{max}$，求出$\pi$的最优近似分数。

$5 \le n_{min} \le n_{max} \le 200000000, n_{max} - n_{min} < 100$

题解：所有`primitive Pythagorean triples`满足$a=x^2-y^2, b=2xy, c=x^2+y^2$，其中$x > y > 0$，$\gcd(x,y)=1$并且$x$和$x$奇偶性不同。

一种做法是暴力生成所有的`primitive Pythagorean triples`，然后把所有询问离线。另一种做法是枚举每个$n$和$x$，用容斥计算合法的$y$的个数。

## I. Partition of Queries

题意：有一个队列，可以加入一个数，耗时$0$；可以询问当前队列大小，耗时为当前队列大小。现在给你一个长度为$n$的操作序列，你可以在某些维护插入清空队里的操作，耗时$y$。求出最小总耗时。

$1 \le n \le 10^6, 0 \le y \le 10^6$

题解：裸斜率优化。

## J. Random Chess Game

## K. What? Subtasks? Again?

题意：有一场比赛，有$5$个特性，总共有$n$个参赛选手。然后有$k$个条件，第$i$个条件为，如果特性$f_i$打开了，那么选手$c_i$不会参赛。现在问是否存在一个方法使得参赛人数不超过$m$，在这个基础上求出最多参赛人数。

题解：$2^5$枚举所有可能即可。

## L. The Five Bishops