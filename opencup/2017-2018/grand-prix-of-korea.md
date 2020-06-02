# Grand Prix of Korea

+ [ ] [Donut](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/A/)
+ [ ] [Circular Arrangement](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/B/)
+ [ ] [Earthquake](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/C/)
+ [ ] [Dynamic Input Tool](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/D/)
+ [ ] [Central Lake](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/E/)
+ [ ] [Computing MDSST](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/F/)
+ [x] [MST with Metropolis](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/G/)
+ [ ] [Number of Cycles](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/H/)
+ [x] [Square Sum of the Occurence Counts](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/I/)
+ [ ] [Game of Sorting](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/J/)
+ [ ] [Subsequence Queries](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/K/)
+ [ ] [XOR Transformation](https://official.contest.yandex.com/opencupXVIII/contest/7389/problems/L/)

## G. MST with Metropolis

题意：给出$n$个点$m$条边的无向带权连通图。对于每个点$i$，求出包含与$i$直接相连所有边的最小生成树的权值。

$1 \le n \le 10^5, n - 1 \le m \le 3 \times 10^5$

题解：先求出一个MST，对于每个点$i$，考虑$i$的邻接点集合$V_i$，显然只有$V_i \cup \{i\}$构成的虚树上的边有用。拿出这些边求个MST即可。

## I. Square Sum of the Occurence Counts

题意：有个字符串s$，对于每个前缀x都统计下：\sum_p f(x,p)^2，其中f(x,p)表示$p在$x$出现次数。

$1 \le |s| \le 10^5$

题解：建出SAM，然后每次就是对一条路径整体加上$1$，询问所有点的平方和。考虑树链剖分，然后线段树维护即可。


