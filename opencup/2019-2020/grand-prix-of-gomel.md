# XX Open Cup. Stage 11. Grand Prix of Gomel / Petrozavodsk Winter 2020. Gennady Korotkevich Contest 5

+ [ ] [A. Avg](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/A/)
+ [ ] [B. Bin](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/B/)
+ [ ] [C. Cat](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/C/)
+ [ ] [D. Div](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/D/)
+ [ ] [E. Exp](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/E/)
+ [x] [F. Flip](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/F/)
+ [ ] [G. Grp](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/G/)
+ [x] [H. Hit](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/H/)
+ [ ] [I. Ineq](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/I/)
+ [ ] [J. Joy](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/J/)
+ [ ] [K. Kilk](https://official.contest.yandex.ru/opencupXX/contest/17209/problems/K/)

## F. Flip

题意：有$2n$个人，每个人用掷硬币的方式决定分组：从$1$到$2n$依次掷硬币，如果朝上并且第一组人数不超过$n$个，那么去第一组否则去第二组；如果朝下并且第二组人数不超过$n$个，那么去第而组否则去第一组。

现在给出$m$组人，第$i$组为$A_i = \{a^i_1, a^i_2, \dots, a^i_{k_i}\}$，求出这些人分在了同一组的概率，对$998 244 353$取模。

$2 \le n \le 10^5, 1 \le m \le 10^5, 2 \le k_i \le n, \sum k_i \le 2 \cdot 10^5$

题解：考虑长度为$2n$的`01`串，其中有$n$个`0`和$n$个`1`，表示最终分组情况。可以发现这个串出现的概率是$2^{-\min(l_0,l_1)}$，其中$l_0$和$l_1$分别表示最后一个`0`和`1`出现的位置。因为前面$\min(l_0,l_1)$个位置上，出现的概率都是$\frac{1}{2}$。

对于一个集合$A_i$，我们需要求出$s_{a_1}=s_{a_2}=\dots=s_{a_k}=0 \text{ or } 1$的方案数即可。由于对称性，可以仅考虑等于$0$的情况，令$m=\min(l_0,l_1)$。

+ $m=a_k$，那么必有$s_m=0$，显然方案数是$\binom{m-k}{n-k}$。
+ 令$a_0=0,a_{k+1}=2n+1$，考虑$a_i < m < a_{i+1}$ ($0 \le i \le k$)，那么有$s_m=1$，可以发现方案数为$\binom{m-i-1}{n-1}$，表示要从剩下$m-i-1$个位置中选出$n-1$个`1`来。这个对答案的贡献为$\binom{m-i-1}{n-1} \cdot 2^{-m}$，稍微变形得到$\binom{m-i-1}{n-1} \cdot 2^{-(m-i-1)} \cdot 2^{-i-1}$。预处理出$\binom{x}{n-1} \cdot 2^{-x}$的前缀和，就可以$O(1)$查询每个$i$对应的贡献。
+ $m > a_k$并且$s_m=0$，也可以得到方案数为$\binom{m-k-1}{n-k-1}$，贡献为$\binom{m-k-1}{n-k-1} \cdot 2^{-m}$。变形得到$\binom{m-k-1}{n-k-1} \cdot 2^{-(m-k-1)} \cdot 2^{-k-1}$。由于只有$O(\sqrt{n})$种不同的$k$，对于每种$k$，预处理出$\binom{x}{n-k-1} \cdot 2^{-x}$的前缀和即可。

总的复杂度$O(n \sqrt{n})$。

## H. Hit

题意：给出$n$个区间$[l_i,r_i]$，你需要放下$n$个点，使得每个区间里至少包含一个点。并且区间里点个数的最大值要尽可能小。

$1 \le n \le 10^5, 10^9 \le l_i < r_i \le 10^9$

题解：考虑每个区间至少放一个点的贪心做法。维护一个集合表示当前没有放点的区间，每次选出一个右端点最小的区间，在这个右端点放下一个区间。

如果在上述方案下，最大值为$t$，那么可以证明最优值要么是$t$，要么是$t-1$。

考虑上述方案下，包含点数最多的那个区间$[l, r]$。假设这$t$个点从左往右依次为$x_1,x_2,\dots,x_t$。那么在最优方案下，这个区间里的点个数肯定要$\le t$。考虑$l$左边的第一个点为$x^\prime_1$，那么接下来那个点$x^\prime_2$一定要不超过$x_2$。因为我们需要用$x^\prime_2$来覆盖被$x_1$覆盖的区间，如果超过$x_2$，肯定会有区间没有被覆盖。类似的，$x^\prime_3$一定不能超过$x_3$。依次类推，$x^\prime_t$一定不能超过$x_t$。也就是少区间$[l,r]$里至少要有$t-1$个点。

那么接下来只需要判定$t-1$是否可行即可。我们从左往右考虑数轴上每个点$x$，定义$x$是合法的当且仅当如果我们的方案包含了点$x$后，仅考虑加入其它$\ge x$的点，所有右端点$r_i \ge x$的区间里面最多只有$t-1$个点。令$next(x)$是$x$右边最远的合法的点，使得没有区间$[l_i,r_i]$严格在区间$[x,next_x]$里。考虑$y=next^{t-1}(x)$，如果存在一个$[l_i,r_i]$同时包含了端点$x$和$y$，那么$x$显然是不合法的，否则$x$是合法的。

最后如果所有点$\min(l_i)-1$是合法的，那么就存在一个$t-1$的解。

复杂度$O(n \log n)$。