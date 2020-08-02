# XVI Open Cup. Stage 15. Grand Prix of Moscow

+ [ ] [A. Guess A Number](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/A)
- [ ] [B. Path Choosing](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/B)
- [ ] [C. Distanced Strings](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/C)
- [ ] [D. Subcubes](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/D)
- [ ] [E. Super Backpack](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/E)
- [ ] [F. Rain](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/F)
- [ ] [G. Points And Circles](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/G)
- [ ] [H. Vectors](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/H)
- [ ] [I. Cartesian Tree](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/I)
- [ ] [J. Maximal Angle](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/J)
- [x] [K. Bipartite Graph](https://official.contest.yandex.ru/opencupXVI/contest/2366/problems/K)

## K. Bipartite Graph

题意：有一个二分图，左边$n$个点，右边$m$个点，标号分别为$0$到$n-1$和$0$到$m-1$。一开始给出了$k$条边$a_i$和$b_i$。然后第$i$步(从$0$开始)会连接$i \bmod n$和$i \bmod m$这两个点。求出到哪一步为止，这个图连通了。

$1 \le n, m \le 10^9, 0 \le k \le 2 \times 10^5, 0 \le a_i < n, 0 \le b_i < m$

题解：考虑这样一个图：$n+m$个点，依次编号为$0$到$n+m-1$，不一定是二分图。第$i$次会连接$i \bmod (n + m)$和$(i+n) \bmod (n+m)$，求什么时候连通。

可以发现，对于上面问题，最多不超过$n+m$步。如果每一步，原问题和这个问题连接的连通分量是同一个，那么这两个问题就是等价的。

考虑第$i$步之前，一定有$i$和$i \bmod n$是连通的。因为$i$和$i-n$连通，$i-n$和$i-2n$连通，依次类推，可以得到$i$和$i \bmod n$连通。

同样也有$(i + n) \bmod (n+m)$和$(i \bmod m) + n$是连通的，证明如下：

+ 当$i < m$的时候，左边和右边都是$i+n$，显然成立。

+ 当$i \ge m$的时候
  
  + 如果$m \ge n$，必然有$i=m+r$，那么左边是$r$，右边是$r+n$和$r$连通。
  
  + 如果$m < n$，那么对于$0 \le r < m$，一定有$r$和$r+n$连通。然后下一步，$m$实际上和$0$连通了，也就是说依次类推，接下来$km+r$会和$r$连通。如果$i=km+r$，那么左边是$(k-1)m+r$，右边是$n+r$都和$r$连通。

因此，第$i$步，你使得$i$和$(i+n) \bmod (n+m)$连通的话，$i \bmod n$和$i \bmod m$就连通了。所以这两个问题是等价的。

然后，考虑前$m$步，我们会把$i$和$i+n$连起来。也就是说，如果$u \bmod n=v \bmod n$，那么$u$和$v$是连通的。

于是你可以先检查这$m$步，加上一开始给的$k$条边后是不是连通的(把端点都对$n$取模后判断)。如果不连通，我们把问题从$(n,m)$规约到了$(m \bmod n, n - m \bmod n)$的问题。如果连通了，那么可以考虑二分$t \in [0, m]$，看看加入这$t$条边后是否连通。

+ 加入$t$条边后，只剩下了$n+m-t$个点是不连通的，标号从$t$到$n+m-1$。然后用并查集判断下即可。

最后，如果到$(0, 1)$这个状态，那么图也是可以连通的，否则永远也不会连通。
