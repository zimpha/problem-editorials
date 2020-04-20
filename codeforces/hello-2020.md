# Hello 2020

+ [x] [A. New Year and Naming](https://codeforces.com/contest/1284/problem/A)
+ [x] [B. New Year and Ascent Sequence](https://codeforces.com/contest/1284/problem/B)
+ [x] [C. New Year and Permutation](https://codeforces.com/contest/1284/problem/C)
+ [x] [D. New Year and Conference](https://codeforces.com/contest/1284/problem/D)
+ [x] [E. New Year and Castle Construction](https://codeforces.com/contest/1284/problem/E)
+ [x] [F. New Year and Social Network](https://codeforces.com/contest/1284/problem/F)
+ [x] [G. Seollal](https://codeforces.com/contest/1284/problem/G)

## A. New Year and Naming

题意：略

题解：略

## B. New Year and Ascent Sequence

题意：一个序列$a_1,a_2,\dots,a_l$存在`ascent`当且仅当存在$(i,j)$使得$1 \le i < j \le l$并且$a_i < a_j$。现在给出$n$个序列$s_1,s_2,\dots,s_n$，求有多少对$(x,y)$使得$s_x+s_y$存在`ascent`。

$1 \le n \le 10^5, 0 \le s_{i,j} \le 10^6, \sum |s_i| \le 10^5$。

题解：如果一个序列$s_x$已经有`ascent`了，那么任何$s_y$都是合法的；$s_y$里有`ascent`也是类似。否则$s_x$和$s_y$都是一个递减的序列，值需要关心$s_y$的开头是否大于$s_x$的结尾。随便统计下即可。

## C. New Year and Permutation

题意：对于一个排列$p_1,p_2,\dots,p_n$，定义价值为满足$\max\{p_l, p_{l+1}, \dots, p_r\} - \min\{p_l, p_{l+1}, \dots, p_r\} = r - l$的$(l,r)$的对数。

现在给出$n$和质数$m$，求出$n!$个排列的价值和，对$m$取模。

$1 \le n \le 25000, 10^8 \le m \le 10^9$

题解：枚举$x=r-l$的大小，贡献为$x! \cdot (n-x)! \cdot (n-x+1)^2$。

## D. New Year and Conference

题意：有$n$个课，在$a$教室里上的话需要在$[sa_i,ea_i]$时间，在$b$教室的话需要在$[sb_i,eb_i]$时间。

求出是否存在一个非空子集$S$，使得这个子集在某个教室区间不相交，在另一个教室区间存在相交。

$1 \le n \le 10^5, 1 \le sa_i, ea_i, sb_i, eb_i \le 10^9, sa_i \le ea_i, sb_i \le eb_i$

题解：现在子集大小为$2$就够了，不妨假设在$a$里相交了。那么不妨枚举$a$里的一个公共点，你可以维护处当前有哪些区间。你的目的是找两个区间在$b$里面不相交，也就是$sb_i$的最大值大于$eb_i$的最小值。扫描线即可。

## E. New Year and Castle Construction

题意：给出平面上$n$个不同的点$(x_1,y_1),(x_2,y_2),\dots,(x_n,y_n)$。没有三点共线。对于每个点$p$，求出$f(p)$表示有多少简单四边形包含$p$。输出$f(p)$的和。

$5 \le n \le 2500, -10^9 \le x_i, y_i \le 10^9$

题解：对于一个$p$，考虑哪些四边形不包含$p$。就是说枚举一个$q$，那么直线$pq$左侧选三个点即可。这个只要枚举$p$后，把所有点极角排序，然后双指针枚举过去就能算出来。

## F. New Year and Social Network

题意：给出两个$n$个点的树$T_1$和$T_2$。考虑这样一个二分图，左边点是$T_1$的所有边$E(T_1)$，右边点是$T_2$的所有边$E(T_2)$。对于$e \in E(T_1), f \in E(T_2)$，他们之间有边当且仅当$T_1-\{e\}+\{f\}$是一棵树。求出这个二分图的一个最大匹配，以及方案。

$2 \le n \le 250000$

题解：可以证明，对于$e \in E(T_1)$，我们可以找到$f \in E(T_2)$使得$T_1-\{e\}+\{f\}$，$T_2-\{f\}+\{e\}$都是树。

那么我们考虑从$T_2$的叶子开始枚举$f$，然后在$T_1$中找到对应的$e$。可以发现，在$T_1-\{e\}+\{f\}$和$T_2-\{f\}+\{e\}$这两棵树中，
+ 对于$T_2-\{f\}+\{e\}$，我们可以直接忽略掉$e$，因为以后再也用不到了。
+ 对于$T_1-\{e\}+\{f\}$，我们可以把$e$对应的两个点合并车一个点。

这个用一个并查集就可以搞定。

## G. Seollal

题意：给出$n \times m$的网格，有些位置是障碍物，用`X`表示；有些位置是空地，用`O`表示。保证$(1,1)$是空地，并且从$(1,1)$出发可以到达其他所有空地。现在给每个空地黑白染色，$(1,1)$是黑色，相邻两个空地颜色不一样。

你需要找出这样一个网格图的一个生成树，使得除$(1,1)$外，其他黑点的度数都恰好是$2$。

题解：把这些有度数要求的点当做特殊点，设为集合$S$。显然，如果我们能够选出一个生成森林，使得每个特殊点度数都是$2$就好了。

考虑把度数都是$2$的限制改成度数不超过$2$，那么生成森林对应了`graphical matroid`，度数不超过$2$对应了`choice matroid`。我们只需要做一个拟阵交即可。假设选出来的边集为$E$，只要$|E| \ge 2|S|$就是有解的，否则无解。之后我们只需要用一些其他边把生成森林变成生成树即可。