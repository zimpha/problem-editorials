# Grand Prix of Southern Europe

+ [ ] [A. Max or Min](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/A/)
+ [ ] [B. Level Up](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/B/)
+ [ ] [C. Find the Array](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/C/)
+ [ ] [D. Cycle String?](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/D/)
+ [ ] [E. Life Transfer](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/E/)
+ [ ] [F. Game on a Tree](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/F/)
+ [ ] [G. Projection](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/G/)
+ [x] [H. Tree Permutations](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/H/)
+ [ ] [I. Absolute Game](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/I/)
+ [ ] [J. Graph and Cycles](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/J/)
+ [ ] [K. Stranded Robot](https://official.contest.yandex.ru/opencupXX/contest/14765/problems/K/)

## A. Max or Min

题意：给出$n$个数$a_1,a_2,\dots,a_n$，排成一个环。你可以把$a_i$变成$\min(a_{i-1},a_i,a_{i+1})$或者$\max(a_{i-1},a_i,a_{i+1})$。对于每个$1 \le x \le m$，输出把这个数组全部变成$x$的最小操作次数。

$3 \le n \le 200000, 1 \le m \le 200000, 1 \le a_i \le m$

## B. Level Up

题意：你在level $0$要升级到level $2$。从$0$到$1$需要经验值$s_1$，从$1$到$2$需要经验值$s_2$。现在有$n$个任务，第$i$个任务在level $0$做需要花时间$t_i$，得到经验值$x_i$；在在level $1$做需要花时间$r_i$，得到经验值$y_i$。求出升级到level $2$的最小耗时。

$1 \le n, s_1, s_2 \le 500, 1 \le y_i \le x_i \le 500, 1 \le r_i < t_i \le 10^9$

## C. Find the Array

题意：有$n$个互不相同的整数$a_1,a_2,\dots,a_n$，你不知道它们的具体值，需要通过交互找出它们的具体值。你可以询问：1. 某个数的具体值；2. 询问$k$个数两两之间的绝对值，结果会shuffle后返回。不能询问超过$30$次。

$1 \le n \le 250, 1 \le a_i \le 10^9$

## D. Cycle String?

题意：给出长度为$2n$的循环串，你可以shuffle它使得任意长度为$n$的连续子串都是primitive的，即不存在非空字符串$u$和大于$1$的整数$k$，使得这个串是$u^k$。

$2 \le 2n \le 1000000$

## E. Life Transfer

题意：有$n$个人，第$i$个人年龄是$a_i$。现在需要运送这$n$个人。可以租车，包括司机可以载$k$个人，其中司机年龄至少为$l_c$，花费$p_c$。可以租摩托车，只能载$1$个人，年龄至少为$l_m$，花费$p_m$。可以花费$t$的价格施魔法，可以选择两个人$x$和$y$，令$a_x$加$1$，$a_y$减$1$。假设当前年龄为$u$，那么最终年龄$v$必须满足$u-d \le v \le u+d$以及$1 \le v$。

求出最小花费，使得每个人都能乘上某个交通工具。

$1 \le n, k \le 10^5, 1 \le l_m < l_c \le 10^5, 1 \le p_m < p_c \le 10^5, 0 \le t, d \le 10^5, 1 \le a_i \le 10^5$

## F. Game on a Tree

题意：给出一棵$n$个点的有根树，每个点颜色一开始是白色。Alice和Bob玩游戏。Alice先手，选择一个点染黑。之后两个人轮流，每次可以选择当前点的一个白色的祖先或者后代染黑。不能操作的输，求出先手必胜还是必败。

$1 \le n \le 10^5$

## G. Projection

题意：给出一个$n \times m \times h$的方块的两个投影，$n \times m$和$n \times h$的`01`矩阵。求出原图形里最多以及最少有几个方块。

$1 \le n, m, h \le 100$

## H. Tree Permutations

题意：有一颗$n$个点的树，令$p_i < i$是$i$的父亲，$w_i$是$i$和$p_i$这条边的权值。把数组$b=[p_2,w_2,p_3,w_3,\dots,p_n,w_n]$重新排列后得到一个数组$a$。

定义一棵树是`k-long`当且仅当$1$到$n$的路径上存在$k$条边。一棵树是`k-perfect`，当且仅当它是`k-long`，并在在所有是`k-long`的树中，$1$到$n$路径上权值和最大。

现在给出$a$，对于每个$k$，求出所有`k-perfect`的树的$1$到$n$路径上权值和。

$2 \le n \le 10^5, 1 \le a_i \le n-1$

题解：我们先把所有数都排序得到$a_1 \le a_2 \le \dots a_{2n-2}$。

首先如果存在一个数$i$使得$a_i > i$，那么肯定是无解的。由于$1 \le a_i \le n-1$，这样的$i$一定满足$i < n - 1$。然后也就是说最多只有$i-1$个数的不超过$i$，但是$2,3,\dots,i+1$的$p_i \le i$，产生了矛盾。

其次$a_i=i$的那些$i$，一定是$1$到$n$的必经点。如果$a_i=i$，那么显然最多只有$i-1$个数不超过$i-1$。同时可以知道$2,3,\dots,i$的$p_i < i$，也就是说$1$到$i-1$这些数会被用做这些点的$p_i$。于是$i+1,\dots,n$这些点的$p_i$必定大于等于$i$。也就是说从$n$到$1$一定会经过点$i$。

那做法就显然了，考虑把满足$a_i=i$的点全部拿出来，假设有$m$个。然后除去这些点以外的点的集合是$S$，那么只有$m \le k \le m + |S|$的$k$是有解的。每次只需要枚举$k$，然后标记$a_i=i$的不可选，同时$S$里面最小的$k-m$个数也不可选。然后在剩下来的$2n-2-k$个数里选最大的$k$个求和即可。

我们可以用$cnt(x)$表示$x$出现了多少次，然后维护$p$表示$cnt(p..n-1)$是最大的$k$个数。随着$k$的变大，某个$cnt(x)$会减少$1$，$p$永远只会单调减小。复杂度可以做到$O(n)$。

## I. Absolute Game

题意：有两个数组$a_1,a_2,\dots,a_n$和$b_1,b_2,\dots,b_n$。Alice和Bob两个人玩游戏，Alice先手。每次可以从各自个数组里面删掉一个数。当只剩一个数的时候停止游戏。假设$a$里最后剩下$x$，$b$里最后剩下$y$。Alice要是$|x-y|$最大，Bob要使$|x-y|$最小，求出最后结果。

$1 \le n \le 1000, 1 \le a_i, b_i \le 10^9$

## J. Graph and Cycles

题意：给出一个$n$个点完全无向图，每条边有个权值$w$。把它分解成若干个环，使得环的权值和最小。对于一个环$e_1,e_2,\dots,e_k$，权值和定义为$\sum \max(w_{e_i},w_{e_{i \bmod n + 1}})$。

$3 \le n \le 999, n \text{ is odd}, 1 \le w \le 10^9$

## K. Stranded Robot

题意：给出$n \times m \times p$的格子，每个格子可以是

+ `*`：地板
+ `-`：空格子
+ `R`：机器人所在位置，也就是起点
+ `T`：传送们所在位置，也就是终点

有光线沿着重力方向照射，机器人可以按照如下三种方式走，每次行走前可以改变重力的方向，起点和终点必须都能被光照射到，：

1. Moving across the floor：机器人在一个地板上，可以往周围$4$个方向走
2. Jumping off a clif：往前走一步跳下去
3. Dropping down：沿着重力方向滑下去

求出最小步数到达传送门。

$1 \le m, n, p \le 500$
