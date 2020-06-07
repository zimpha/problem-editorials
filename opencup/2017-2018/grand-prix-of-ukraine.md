# XVIII Open Cup. Grand Prix of Ukraine

- [x] [A. Accommodation Plan](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/A/)
- [ ] [B. Card Game](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/B/)
- [ ] [C. The Most Expensive Gift](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/C/)
- [ ] [D. Cut the Cake](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/D/)
- [x] [E. Message](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/E/)
- [ ] [F. Bad Word](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/F/)
- [ ] [G. Zenyk, Marichka and Interesting Game](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/G/)
- [ ] [H. Frog Jumping](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/H/)
- [ ] [I. Slot Machine](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/I/)
- [ ] [J. Half is Good](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/J/)
- [x] [K. Dance](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/K/)
- [ ] [L. Impress Her](https://official.contest.yandex.ru/opencupXVIII/contest/5917/problems/L/)

## A. Accommodation Plan

题意：有一棵$N$个点的树，第$i$条边连接$A_i$和$B_i$，权值为$C_i$。现在你要选出$K$个不同的点，使得存在一个点带这$K$的距离都不超过$L$。

$1 \le K \le N \le 10^5, 1 \le L \le 10^9$

题解：对于这$K$个点都能够到达点里，选取深度最小的那个点作为代表点。假设这个代表点为$u$，那么令$A_u=\{v \mid \text{dist}(v,u) \le L\}$，$B_u=\{v \mid \text{dist}(v,u) \le L \text{ and } \text{dist}(parent(u), v) \le L\}$。那么这个点$u$对答案的贡献为$\frac{|A_u|!}{(|A_u|-K)!}-\frac{|B_u|!}{(|B_u|-K)!}$。

$|A_u|$和$|B_u|$都可以方便的用树分治计算出来。

## E. Message

题意：你有两个字符串$s$和$t$，其中$s$的第$i$个字符删除代价为$w_i$。每次你可以选择一个字符$c$，然后考虑$c$在$s$出现的最早位置和最晚位置，选一个删掉。求出$s$变成$t$的最小代价和。

$1 \le |s|, |t| \le 200000, 1 \le w_i \le 10^9$

题解：有一个$O(n^2)$的dp，令$f(i,j)$表示第一个串匹配到$s_i$，第二个串匹配到$t_j$的最优值。考虑什么时候$s_i$可以被跳过。

令$occ(c)$表示字符$c$在$t$中出现位置的集合，那么$s_i$可以跳过当且仅当$j \le \min(occ(s_i))$或者$j \ge \max(occ(s_i))$。并且可以注意到，如果$j$不在$occ(s_i)$的最大值或者最小值上，一定有$t_j \ne s_i$。

于是乎，我们可以把$t$按照每个字符出现的最早位置和最晚位置分成最多$26 \times 4-1$段：$p_1,[p_1+1,p_2-1],p_2,[p_2+1,p_3-1],p_3,\dots,[p_{n-1}+1,p_n-1],p_n$

对于每一段我们都可以知道$s$里哪些位置一定要被删除，哪些位置一定要留下。假设留下来位置对应的串是$s^\prime$。

对于那些$p_k$的位置，我们可以进行普通的dp转移，只有$s_i=t_{p_k}$的位置才是合法的dp状态。

对于那些$[p_k+1,p_{k+1}-1]$段，我们可以一起转移，把这个子串抠出来，只有在$s^\prime$上匹配的位置才是合法的dp状态。

## K. Dance

题意：有$n$个人，第$i$个人位置在$x_i$。你可以把第$i$个人放到$x_i-d$或者$x_i+d$位置处。然后你要把这些人分成若干组，对于每一组，考虑组里位置最大的$r_j$和最小的$l_j$，代价为$a + b \times (r_j - l_j)$。你需要使得代价和最小。

$1 \le n \le 100, 1 \le d \le 50, 1 \le a, b \le 10^6, 1 \le x_i \le 100$

题解：不妨先把所有人都往左移动$d$，那么第$i$个人的位置要么是$x_i$，要么是$x_i+2d$。可以发现：

1. 现在最大的可能坐标是$200$。
2. 对于两个组$[l_i,r_i]$和$[l_j, r_j]$，这两个区间一定没有任何公共点，否则一定有一个更优的分组。

那么令$v_i$表示位置$i$和位置$i+1$是否是属于同一组，是的话是`1`，否则是`0`。对于一个固定的$v$，我们很容易判定是否合法：$v_i$是`0`当且仅当位置$i-2d$上没有人 或者 $v_{i-2d}$是`1`。一个连续的`01`就是一段区间的开始。

考虑按照$d$的大小来dp这个$v$数组：

+ $2d \le 20$，令$dp(i, mask)$表示考虑到前$i$个位置，最后$2d$个位置状态是$mask$的最小代价。转移的时候只需要每个$i+1$位置是`0`还是`1`即可。如果是`1`的话，需要根据位置$i$是`0`还是`1`确定代价$cost_0=a$，$cost_1=\min(a,b)$；如果是`0`的话，需要判定这个`0`是否合法，用上述条件即可。
+ $2d > 20$，可以发现$\frac{200}{2d} < 10$。那么可以考虑这样一个暴力dp，先枚举$0,2d,4d,\dots,$位置的状态，之后考虑$1,2d+1,4d+1,\dots,$的，依次类推，直到$2d-1,4d-1,6d-1,\dots$位置的状态。直接暴力做复杂度是$O(2^{30})$的，因为我们需要枚举第一层的，用作和最后一层合并。只需要把中间层的转移用逐格dp的方式来做，就可以把复杂度变成$O(2^{20})$。填`0`或者`1`的代价处理方式和上面一样。