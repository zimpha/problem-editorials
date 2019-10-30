# PA 2002 May

+ [x] [Imiona mrówek (Round 0)](https://szkopul.edu.pl/problemset/problem/Dd6sP2-76y6UUIFSjW0F9uwe/site/)
+ [x] [Bałagan i stonki (Round 1)](https://szkopul.edu.pl/problemset/problem/YqMCZQAgBAOuE4IBiz2WYGK-/site/)
+ [x] [LinkNet (Round 1)](https://szkopul.edu.pl/problemset/problem/l3MkEmGhiL-2WyUjSnNnV3Mf/site/)
+ [x] [Wrocławskie ZOO (Round 2)](https://szkopul.edu.pl/problemset/problem/KqUXfSPdeBhPoitr12PKRzOh/site/)
+ [x] [Trikontenerowiec (Round 2)](https://szkopul.edu.pl/problemset/problem/NHHv_Kn4Z98pjKFVpoJ6bOWb/site/) 
+ [ ] [Żuki (Round 3)](https://szkopul.edu.pl/problemset/problem/unrv0WIvym2Ts4nwWZtP2S31/site/)
+ [x] [Superszybkie wyścigi w kółko (Round 3)](https://szkopul.edu.pl/problemset/problem/fWAF3fOirkeghGySJouhq37h/site/) 
+ [ ] [Megawirus (Round 3)](https://main.mimuw.edu.pl/en/user.phtml?op=showtask&task=i&con=PA2002)
+ [x] [Minusy (Round 4)](https://szkopul.edu.pl/problemset/problem/POAyCWzUB990_g4_MA4GF9Jw/site/)
+ [x] [Narciarze (Round 5)](https://szkopul.edu.pl/problemset/problem/cDrSGje2aim78XS24ooejALy/site/)
+ [x] [Waga (Round 5)](https://szkopul.edu.pl/problemset/problem/tq7_CkSHf9RfYWO6BvZzX9rQ/site/)
+ [x] [Liczby B-gładkie (Round 6)](https://szkopul.edu.pl/problemset/problem/VBw12Ev-eDIXnziDWIE9jqVX/site/)
+ [x] [Nawiasy (Round 6)](https://szkopul.edu.pl/problemset/problem/wZnNWkr5fd2DApweCAGbXf0b/site/)
+ [x] [Szyfr (Round 6)](https://szkopul.edu.pl/problemset/problem/w1jMa9aJ6iCV2uqtJBEZorHU/site/)

## Round 0

### Imiona mrówek (imi)

题意：给$n$个单词，求出哪个单词里面本质不同的字母最多。

$1 \le n \le 100$

题解：略

## Round 1

### Bałagan i stonki (a)

题意：给出$n$个单词，问去除`-`以及忽略大小写后有多少个本质不同的单词。

$1 \le n \le 10000$

题解：略

### LinkNet (b)

题意：给出$n$个区间$[a_i,b_i]$，问哪个位置被覆盖次数最多。

$0 \le n \le 10^5, 0 \le a_i < b_i \le 10^9$

题解：略

## Round 2

### Wrocławskie ZOO (c)

题意：动物园里有$a$个入口，$n$个景点，$b$个出口，依次标号为$1,2,\dots,a+n+b$。有$m$条双向路径，给出$k$个依次要访问的景点，要求在访问第$i$个景点的时候不能经过$i$之后那些景点。求从任意出口进入，访问完所有景点，选个出口出去的最短路。

$1 \le a, b \le 25, 1 \le k \le 100, 1 \le n \le 1000, 1 \le m \le 5000$

题解：略

### Trikontenerowiec (e)

题意：有$n$个物品，第$i$个物品价值是$w_i$，高度是$h_i$。有$m$个位置，第$i$位置只能放一个高度不超过$i$的物品。问怎么放使得价值和最大。

$1 \le n \le 10^6, 1 \le m, h_i \le 500000, 1 \le w_i \le 1000$

题解：依次枚举每个位置，从可以放得物品中选取一个价值最大的物品放置。

## Round 3

### Żuki (d)

### Superszybkie wyścigi w kółko (h)

题意：给出一个$n$个点$m$条边的有向图，保证每条边做多两条入边和两条出边。现在要找出$n$条边的子图，使得每个连通分量都是一个简单环。求方案数。

$1 \le n \le 10^4, 1 \le m \le 20000$

题解：每个点拆成入边和出边，然后就可以看做是一个二分图了。求出二分图的一个最大匹配，现在最大匹配就是一组解。然后，对于匹配边$(u,v)$定方向$u \to v$，否则定方向$v \to u$。考虑图中一个增广环，那么肯定可以交错轨取反得到另外一组方案。又由于出边和入边个数的限制，增广环肯定是唯一的，于是求出增广环个数就好了。

### Megawirus (i)

题意：第$k$代的第$i$个数会在第$k+1$代生下$2i$和$2i+1$。现在给出第$k$代的$n$个数，求它们的LCA在哪一代。

$1 \le k \le 512, 1 \le n \le 150$

## Round 4

### Minusy (min)

题意：$n$个元素的表达式$x_1 \pm x_2 \pm \dots \pm x_n$，你要在$x_1 - x_2 - \dots - x_n$里加上括号，使得两个表达式相同。

$2 \le n \le 10^6$

题解：在连续的加号左右加上括号即可。

## Round 5

### Narciarze (nar)

题意：给出一个平面图，图中有$n$个点，$m$条有向边。每个点都有不同的横坐标和纵坐标，有一个最高点$1$和一个最低点$n$。每条有向边连接着两个不同的点，方向是从较高点连到较低点。对于图中任意一点$u$，都至少存在一条$1$到$u$的路径和一条$u$到$n$的路径。图中由每个点发出的边都已经按照结束点的位置从左到右给出。要求你用若干条从$1$到$n$的路径覆盖图中所有的边，并且使路径数最少。所谓覆盖，就是指每条边至少在一条路径中出现。选取的路径之间可以有相同的边。

$1 \le n \le 5000$

题解：首先是一个经典的有源汇有下界最小可行流，但是常数比较大，过不去。考虑构造这样一个新的图，每个节点$i$对应了原图上一条有向边$(u_i,v_i)$。对于新图上两个点$x$和$y$，$x$和$y$之间有边当且仅当$u_x \le u_y$并且$v_x \le v_y$。显然，在原图上的问题等价于在新图上的最小链划分。等价于求反图的最长链。

最暴力的做法可以$O(n^2)$，但是考虑原图是平面图，可以发现将最长反链所对应的边从左到右排列好，相邻的两条边一定是在同一个域中。并且，由于是从高点连向低点，那么这两条边一定属于从域最高点到最低点的两条不同路径上。于是可以考虑找出每个域，然后根据域边的顺序进行dp。

由于边已经按照从左往右的顺序排好，考虑DFS的时候，如果遇到一个访问过的节点，那么这时候一定有两条父边，一条是之前的，一条是当前的。沿着这两条父边往上走，直到碰到交点为止，我们其实就找出了一个域对应的两条路径。其中一条是沿着dfs栈走的，另一条是沿着不在栈中的点走的，交点其实就是两个父节点在DFS树上的LCA。这样复杂度就是$O(n)$的。

### Waga (wag)

题意：给出$n$个物品，第$i$个重量为$w_i$，要求选出两个不相交子集，使得它们和相同。如果有多种方案，选$w_i$最大值最大的方案。

$2 \le n \le 1000, \sum {w_i} \le 50000$

题解：考虑按照$w_i$从小到大的顺序做01背包，令$T_x$表示重量$x$能否达到，如果能够达到，$T_x$记录了最早达到$x$那个子集里面的最大$w$。那么显然，对于一个重量和$x$，我们可以根据$T_x$轻松构造出方案。

题目要求找到两个和一样的子集，那么我们在加入某个$w_i$的时候，如果发现$T_x$之前已经通过之前某个子集构造出来，那么我们其实就已经找到了一个方案。但是这个方案里面可能有重复元素，一个暴力的做法就是直接去掉这些重复元素，因为是两个子集里同时去掉，所以不影响结果。题目要求多种方案的时候，要选择$w_i$最大的，这个只要稍微维护下即可。

注意到这样复杂度是$O(ns)$的，其中$s=\sum w_i$，比较大，过不了。然后根据上面算法，我们每次新加入$w_i$的时候，只关心两种位置$T_x$和$T_{x-w_i}$同时存在，以及$T_x$不存在，$T_{x-w_i}$存在。于是可以用bitset维护$T_x$的存在性，用位运算快速查找上面两种$x$即可。复杂度$O(\frac{ns}{32})$。

another优化：考虑只枚举$w_i$不同的数，令$c_w$表示$w$出现的次数，在$T_x$基础上，我们另外维护一个数组$V_x$表示在这一轮枚举中，$w$被用了几次，显然只要$V_x \le c_w$都是合法的。因此，我们可以把复杂度优化到$O(\min\{n, \sqrt{s}\}s)$。

## Round 6

### Liczby B-gładkie (lic)

题意：给出$n,m,b$，求区间$[n,n+m]$里$b$-smooth数的个数。

$1 \le n \le 2 \times 10^9, 1 \le m \le 10^8, 1 \le b \le 10^6$.

题解：令$f(n,p_{k})$是$1$到$n$中的$p_k$-smooth数个数，显然有这样一个递推式$f(n,p_{k})=f(\lfloor \frac{n}{p_k} \rfloor, p_k)+f(n,p_{k-1})$，对这个式子做记忆化搜索即可。

注意如果$b \ge \sqrt{n}$，那么$f(n,b)=f(n,\sqrt{n})+\sum_{p > \sqrt{n}} \lfloor \frac{n}{p} \rfloor$，可以大大加速计算过程。

### Nawiasy (naw)

题意：给出一个形如$x_1 \pm x_2 \pm \dots \pm x_n$的表达式，你要在$x_1 - x_2 - \dots - x_n$里加上括号，使得两个表达式相同，并且表达式是好的。一个表达式是好的当且仅当：

+ 它是个单变量表达式
+ 如果$w_1$和$w_2$都是好的，那么$(w_1-w_2)$也是好的。

求加括号的方案数，对$10^9$取模。

$2 \le n \le 5000$

题解：显然题目给出了的是一个中缀表达式，假设前$i-1$个符号构成了一个表达式树，对于新来的一个符号$op_i$，你要把它插到树中。考虑从根节点开始一路往右走这条路径$p_1,p_2,\dots,p_k$，显然这条路径的符号要满足从`-`开始，且`-`和`+`交替出现。然后，你要么把$op_i$插到$p_k$后面，要么选择一个$j (1 \le j \le k)$，把原先$p_j$变成$op_i$的左子树，$op_i$变成$p_j$。这样得到的新表达式树满足中序遍历得到$op_1,op_2,\dots,op_i$。

因此考虑$dp_{i,j}$表示前$i$个符号构成的表达式中，从根节点开始一直往右走的路径长度为$j$的方案数。那么显然$dp_{i,j}=dp_{i-1,j-1}+\sum_{k \ge j}dp_{i-1,k}$，前者表示直接append到最右路径下，后者表示替换。用后缀和优化即可得到$O(n^2)$做法。


### Szyfr (szy)

题意：给出$n$个数$a_1,a_2,\dots,a_n$，和一个整数$S$。要求找出一个子集和恰好是$S$。

$1 \le n \le 40, 1 \le a_i \le 2000000000, 0 \le S \le \sum a_i$

题解：meet in the middle
