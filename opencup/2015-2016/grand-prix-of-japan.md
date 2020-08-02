# XVI Open Cup. Stage 2. Grand Prix of Japan

+ [ ] [A. Where is the Boundary](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_a)
+ [ ] [B. Vector Field](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_b)
+ [x] [C. Kuru Kuru Sushi](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_c)
+ [ ] [D. Identity Function](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_d)
+ [ ] [E. Enclose Points](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_e)
+ [ ] [F. Marching Course](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_f)
+ [ ] [G. Surface Area of Cubes](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_g)
+ [ ] [H. Laser Cutter](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_h)
+ [ ] [I. Live Programming](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_i)
+ [ ] [J. Black Company](https://atcoder.jp/contests/jag2015summer-day4/tasks/icpc2015summer_day4_j)

## C. Kuru Kuru Sushi

题意：有一个长度为$n$的环，第$i$条边的长度为$w_i$。有$q$个起点$s_j$和终点$t_j$。你要给这$n$条边定向，使得$s_j$能够到$t_j$，并且距离之和最小。

$3 \le n \le 10^5, 1 \le q \le 10^5, 1 \le w_i \le 10^5, 0 \le s_j, t_j \le n - 1$

题解：对于每个点对，我们都有两种走法。不妨假设原始边的方向为逆时针，反向为顺时针。

显然顺时针或者逆时针安排边的方向，一定能够得到一组合法的解，不妨就先求出代价作为初始解。

除了上述两种情况的解以外，我们一定能够找到一个点 $s$ 使得 $s$ 相邻的两条边都往外指，即两条边为 $s \to s \pm 1$。那么找到这样的 $s$ 之后，这个所有边的方向几乎就固定了。

一开始对于所有的点对 $(s_j, t_j)$（假设我们已经转化成了环上对应的下标），如果 $s_j < t_j$，那么不妨令这对点逆时针走，否则沿着顺时针方向走。

接下来沿着逆时针方向枚举环上每个点 $x$，考虑如下步骤

1. 对于所有以 $x$ 为终点的的点对 $(s_j, t_j)$，(即 $x=t_j$)，我们改变这个点对走的方向。如果这个时候的解是合法的，我们就更新下答案。

2. 对于所有以 $x$ 为起点的点对 $(s_j, t_j)$，(即 $x=s_j$)，按照距离 $x$ 逆时针方向最远的点对开始，依次改变这个点对走的方向，同时如果解合法，那么更新答案。

可以发现，上述过程一定能够把所有可能的情况都枚举到。接下来就是如何快速判定解是否合法了。

对于环上每条边 $e$，我们维护 $cw_e$ 和 $ccw_e$ 分别表示顺时针和逆时针被覆盖的次数。如果 $\sum_{e} cw_e \times ccw_e = 0$，那么就是合法的；否则解不合法。

于是仅需要一个支持区间加法，区间求和的线段树或者树状数组就可以判定解是否合法。我们在翻转方向的同时，也能够维护处当前解的代价。

因此总得复杂度是 $O((n + q) \log n)$。