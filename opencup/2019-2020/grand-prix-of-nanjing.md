# XX Open Cup. Stage 17. Grand Prix of Nanjing

+ [ ] [A. Everyone Loves Playing Games](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/A/)
+ [ ] [B. Gifted Composer](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/B/)
+ [ ] [C. An Unsure Catch](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/C/)
+ [ ] [D. String Theory](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/D/)
+ [ ] [E. Road Construction](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/E/)
+ [ ] [F. Girlfriend](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/F/)
+ [ ] [G. Blackjack](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/G/)
+ [ ] [H. Yet Another Geometry Problem](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/H/)
+ [ ] [I. A Math Problem](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/I/)
+ [ ] [J. Gaokao](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/J/)
+ [x] [K. Data Structure](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/K/)
+ [ ] [L. Landlord](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/L/)
+ [ ] [M. Travel Dream](https://official.contest.yandex.ru/opencupXX/contest/18242/problems/M/)

## K. Data Structure

题意：给出一棵$n$个点的有根树，每个点一开始权重为$0$。有$m$个操作：

+ 给出$a,x,y,z$，考虑点$a$的所有后代$u$，如果$u$和$a$的距离对$x$取模等于$y$，那么给$u$的权重加上$z$。
+ 给出$a$，求出点$a$的权重。

$1 \le n, m \le 300000, 1 \le a \le n, 1 \le x \le n, 0 \le y < x, 0 \le z \le 500$

题解：令$d(u)$表示点$u$的深度，按照$x$和$\sqrt{n}$的大小分类：

+ $x \ge \sqrt{n}$，那么合法的$d(u)$只有$\sqrt{n}$种，即$d(u)=kx+d(a)+y$。考虑对询问根号分块，每根号次操作把最近的操作$1$一起操作一下，可以简单的用DFS序扫描线做到。对于操作$2$，先查一遍权重，然后枚举最近的操作$1$，把能够应用的改动加上。
+ $x \le \sqrt(n)$，可以考虑枚举$x$，然后把所有节点按照对$x$取模的值进行分类。那么可以发现，对于操作$1$，就是对一个区间做加法，对于操作$2$就是询问单点的值。可以用一个根号分块的结构来维护。