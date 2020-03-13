# XIX Open Cup. Grand Prix of Daejeon

+ [ ] [A. A Plus Equals B](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/A/)
+ [ ] [B. Bohemian Rhaksody](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/B/)
+ [ ] [C. Cactus Determinant](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/C/)
+ [ ] [D. Dijkstra Is Playing At My House](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/D/)
+ [ ] [E. Eat Economically](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/E/)
+ [ ] [F. Fruit Tree](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/F/)
+ [x] [G. Good Set](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/G/)
+ [ ] [H. Hard To Explain](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/H/)
+ [ ] [I. Increasing Sequence](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/I/)
+ [ ] [J. Jealous Teachers](https://official.contest.yandex.ru/opencupXIX/contest/12741/problems/J/)

## G. Good Set

题意：对于集合$U=\{0, 1, 2, \dots, 2^k - 1\}$，$A \subset U$是好的，当且仅当：

+ 如果$x, y \in A$，那么它们的位运算或$x \text{ | } y \in A$
+ 如果$x, y \in A$，那么它们的位运算与$x \text{ & } y \in A$

现在给出$n$个不同的在$0$到$2^k-1$的数，求出有多少好的集合$A$包含所有这些数。

$1 \le k \le 7, 1 \le n \le 2^k$

题解：考虑把一个数看成$\{0,1,\dots,k-1\}$的一个子集。那么如果一个好的集合包含了$0$和$2^k-1$，那么这个实际上是一个$\{0,1,\dots,k-1\}$的拓扑。

一个$\{0,1,\dots,k-1\}$的拓扑和$k$个节点的[transitive digraph](http://mathworld.wolfram.com/TransitiveDigraph.html)是一一对应的。

+ 对于一个拓扑$T$，定义这样一个图$f(T)$：$u$到$v$有一条有向边当且仅当在$T$里的所有包含$u$的集合都包含了$v$。显然$f(T)$是一个transitive digraph。
+ 对于一个transitive digraph $G$，定义集合$g(G)$为：集合$A$属于$g(G)$当且仅当没有边从$A$连向$U-A$。也容易证明$g(G)$是一个拓扑。

然后可以发现$f(g(G))=G$，$g(f(T))=T$，因此拓扑和$k$个节点的transitive digraph是一一对应的。

那么我们这题可以转成求有多少满足条件的$k$个节点的transitive digraph。一定包含整数$a_i$的话，其实是限制了一些边一定不能存在。

我们按照$(0,1),(1,0),(0,2),(2,0),(1,2),(2,1), \dots, (0,k-1), (k-1,0), (1,k-1), (k-1,1), \dots, (k-2,k-1), (k-1,k-2)$的顺序枚举所有边加还是不加。每加完一条边可以用位运算判定是否符合transitive。

最后我们能够枚举出所有的拓扑。但是我们所求的东西不一定需要包含$0$和$2^k-1$，因此对于每个拓扑我们还需要判定下去掉空集或者去掉全集是否可行。令$A(u)$表示$u$和$u$的所有出边构成的点集，那么$A(0), A(1), \dots, A(k-1)$实际上构成了这个拓扑的一组基。我们只需要判断下$\cup A(u)$和$\cap A(u)$是否为全集或者空集即可。
