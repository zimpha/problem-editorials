# Petrozavodsk Winter 2020. Day 7. Gennady Korotkevich Contest 5

+ [ ] [A. Avg](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/A/)
+ [ ] [B. Bin](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/B/)
+ [ ] [C. Cat](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/C/)
+ [ ] [D. Div](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/D/)
+ [ ] [E. Exp](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/E/)
+ [ ] [F. Flip](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/F/)
+ [ ] [G. Grp](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/G/)
+ [x] [H. Hit](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/H/)
+ [ ] [I. Ineq](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/I/)
+ [ ] [J. Joy](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/J/)
+ [ ] [K. Kilk](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/K/)

## H. Hit

题意：给出$n$个区间$[l_i,r_i]$，你需要放下$n$个点，使得每个区间里至少包含一个点。并且区间里点个数的最大值要尽可能小。

$1 \le n \le 10^5, 10^9 \le l_i < r_i \le 10^9$

题解：考虑每个区间至少放一个点的贪心做法。维护一个集合表示当前没有放点的区间，每次选出一个右端点最小的区间，在这个右端点放下一个区间。

如果在上述方案下，最大值为$t$，那么可以证明最优值要么是$t$，要么是$t-1$。

考虑上述方案下，包含点数最多的那个区间$[l, r]$。假设这$t$个点从左往右依次为$x_1,x_2,\dots,x_t$。那么在最优方案下，这个区间里的点个数肯定要$\le t$。考虑$l$左边的第一个点为$x^\prime_1$，那么接下来那个点$x^\prime_2$一定要不超过$x_2$。因为我们需要用$x^\prime_2$来覆盖被$x_1$覆盖的区间，如果超过$x_2$，肯定会有区间没有被覆盖。类似的，$x^\prime_3$一定不能超过$x_3$。依次类推，$x^\prime_t$一定不能超过$x_t$。也就是少区间$[l,r]$里至少要有$t-1$个点。

那么接下来只需要判定$t-1$是否可行即可。我们从左往右考虑数轴上每个点$x$，定义$x$是合法的当且仅当如果我们的方案包含了点$x$后，仅考虑加入其它$\ge x$的点，所有右端点$r_i \ge x$的区间里面最多只有$t-1$个点。令$next(x)$是$x$右边最远的合法的点，使得没有区间$[l_i,r_i]$严格在区间$[x,next_x]$里。考虑$y=next^{t-1}(x)$，如果存在一个$[l_i,r_i]$同时包含了端点$x$和$y$，那么$x$显然是不合法的，否则$x$是合法的。

最后如果所有点$\min(l_i)-1$是合法的，那么就存在一个$t-1$的解。

复杂度$O(n \log n)$。