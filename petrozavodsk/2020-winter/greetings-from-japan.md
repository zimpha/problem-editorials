# Petrozavodsk Winter 2020. Day 2. Greetings from Japan

+ [x] [A. Fast Forwarding](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1400?year=2019)
+ [x] [B. Estimating the Flood Risk](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1401?year=2019)
+ [x] [C. Wall Painting](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1402?year=2019)
+ [x] [D. Twin Trees Bros](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1403?year=2019)
+ [x] [E. Reordering the Documents](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1404?year=2019)
+ [x] [F. Halting Problem](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1405?year=2019)
+ [x] [G. Ambiguous Encoding](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1406?year=2019)
+ [x] [H. Parehtneses Editor](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1407?year=2019)
+ [x] [I. One-Way Conveyors](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1408?year=2019)
+ [x] [J. Fun Region](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1409?year=2019)
+ [x] [K. Draw in Straight Lines](https://onlinejudge.u-aizu.ac.jp/challenges/sources/ICPC/Regional/1410?year=2019)

## A. Fast Forwarding

题意：一开始播放一部电影，按照正常倍速是$1$秒看一单位。有`[3x]`和`[1/3x]`按键，分别会把播放速度乘以$3$或者除以$3$，重复按有叠加效果。给出$t$，求出最少时间到达$t$单位部分，并且到$t$的时候是正常速度。

$0 \le t < 2^{50}$

题解：一开始尽量按下`[3x]`，之后按下`[1/3x]`即可。

## B. Estimating the Flood Risk

题意：一个$w \times d$的格子，其中$n$个格子的高度是知道的。已知相邻两个的高度差最多差$1$，求出高度和的最小可能值。

$1 \le w, d, n \le 50, 1 \le x_i \le w, 1 \le y_i \le d, -100 \le z_i \le 100$

题解：从已经确定的位置出发，可以得到其他位置的高度范围，每个范围的左端点求和即可。

## C. Wall Painting

题意：有$n$个格子，从左往右依次为$1$到$n$，一开始都没有染色。现在有$m$个机器人，第$i$个会把$l_i$到$r_i$的格子都染成$c_i$。你可以选择一些机器人来染色，使得所有格子的总价值最大。一个格子的价值定义为：

+ 如果格子没有被染过色，那么价值为$0$
+ 如果格子仅被染过一种颜色，那么价值为$x$，这一种颜色可以染多次。
+ 如果格子被多种不同的颜色染过，那么价值为$-y$。

$1 \le n \le 10^5, 1 \le m \le 2 \times 10^5, 1 \le x, y \le 10^5, 1 \le l_i \le r_i \le n, c_i \in \{1, 2, 3\}$

题解：考虑最优答案选择的机器人们，如果我们按照区间左端点排序得到$[l_{i_1}, r_{i_1}], \dots, [l_{i_k}, r_{i_k}]$，必然有$l$递增，$r$也递增，且没有一个位置被染超过2次。

考虑把所有区间按照右端点排序，令$dp(i)$表示第$i$个区间必选的最优答案，那么

$$
dp(i)=\max \begin{cases}
dp(j) + (r_i-l_i+1) \cdot x & r_j < l_i \\ 
dp(j) + (r_i-r_j) \cdot x & l_j < l_i < r_j < r_i, c_i=c_j & \\
dp(j) - (r_j-l_i) \cdot y + (r_i - r_j) \cdot x & l_j < l_i < r_j < r_i, c_i \ne c_j)
\end{cases}
$$

## D. Twin Trees Bros

题意：给出两棵三维空间的树，都有$n$个节点。第$i$个节点为$(x_i,y_i,z_i)$，第$j$条边连接节点$u_j$和$v_j$。求出两棵树是否能够通过旋转，平移，缩放操作变成重合。如果可以的话，输出节点重合的方案数。

$3 \le n \le 200, -1000 \le x_i, y_i, z_i \le 1000, 1 \le u_j, v_j \le n$

题解：可以把第一棵树某片叶子平移到原点，然后把这个叶子的父亲旋转到$z$轴正方向上去。之后缩放下，把这条边长度变成$1$。另一棵树的话，枚举一片叶子，做这个变换，看看是否一一匹配即可。

也可以考虑对于每个点，用边长和直线夹角做hash值，这样可以类似树hash的方法来求方案数。

## E. Reordering the Documents

题意：给出一个长度为$n$的排列$s_1,s_2,\dots,s_n$。你需要把他们划分成两个不相交的递增子序列，每个子序列长度不超过$m$。求方案数，对$10^7+7$取模。

$1 \le n \le 5000, n / 2 \le m \le n, 1 \le s_i \le n$

题解：如果$s_i > s_j$并且$i < j$，那么$i$和$j$不能选为同一堆。这样可以建立一个图，如果是二分图的话，有解，否则无解。之后求出每个连通分量黑白节点个数，然后背包下即可。

## F. Halting Problem

题意：有$n$个五元组$(a_i,b_i,c_i,d_i,e_i)$，一开始你的初始值为$x_0$，在$1$号位置。假设你在位置$i$，值为$x$：

+ 如果$x=a_i$，那么$x$会变成$x+b_i$，你会到位置$c_i$。
+ 否则，$x$会变成$x+d_i$，你会到位置$e_i$。

求出能否到达位置$n+1$，以及需要的步数，对$10^9+7$取模。

$1 \le n \le 10^5, -10^{13} \le x_0, a_i, b_i, d_i \le 10^{13}, 1 \le c_i, e_i \le n+1$

题解：只考虑不等于构成的图，显然是一个环套树。我们在执行过程中肯定是走一长段都是不等于，然后再走一条等于的。于是只要能够快速走掉这些不等于的即可。可以分成环和树两部分。

考虑树的，你当前在$v$，值为$x$，你需要找一个最近的祖先$u$，使得$x+s(v)-s(u)=a(u)$，也就是$x+s(v)=a(u)+s(u)$。其中$s(v)$是从根到$v$一路上$d(\cdot)$的和。显然这个用可持久化线段树维护$a(u)+s(u)$的出现位置即可，或者离线处理。

考虑环，你当前在$v$，值为$x$。假设环上$d(\cdot)$的和为$S$，环长为$L$。我们先拉长成两倍，接下来就是找找一个$k$和一个$u$使得，$x+s(u)-s(v)+kS=a(u)$并且$v \le u < v + L$。假设$k$可以是负数的话，也就是要$x-s(v) \equiv a(u)-s(u) \pmod S$。于是我们可以把$a(u)-s(u) \bmod S$相同的一起处理。

+ 如果$S > 0$，就是要找一个$u$使得$a(u)-s(u) \equiv x - s(v) \pmod S, a(u)-s(u) \ge x-s(v)$并且$a(u)-s(u)$最小，有多个的话$u$要最小。
+ 如果$S < 0$，就是要找一个$u$使得$a(u)-s(u) \equiv x - s(v) \pmod S, a(u)-s(u) \le x-s(v)$并且$a(u)-s(u)$最大，有多个的话$u$要最小。

所有树上可行的询问都是$v=c(i),x=a(i)+b(i)$。所有换上可行的询问都是树上询问走到根那种。所以可以离线处理。

## G. Ambiguous Encoding

题意：有$n$个字符，第$i$个字符由一个`01`串$s_i$编码。你需要找出一个最短长度，使得至少存在两个不同的字符串他们的编码一样。

$1 \le n \le 1000, 1 \le |s_i| \le 16$

题解：$dp(i,j)$表示当前较长的串以$s_i$结尾，短串和这个长串长度差$j$时的最短串长。从$dp(i, |s_i|)$出发，跑最短路，最后检查$dp(i,0)$的最小值即可。

## H. Parehtneses Editor

题意：有个空字符串，给出$n$个操作，加一个`(`，或者加一个`)`或者删掉最后一个字符。每次操作后，求出有多少子串是合法括号序列。

$1 \le n \le 200000$

题解：显然我们只要每次维护出新增的合法括号序列数目即可。把`(`看成$1$，`)`看成$-1$，然后维护整个串的和。假设当前和为$d$，令合法后缀的起点为$i$，那么前$i-1$个位置的和也是$d$。由于要求合法，也就是说$d-1$不能出现在$i$到串末尾中。那么只要维护$X(d)$表示和为$d$的前缀的，然后拿$X(d-1)$的最后一个元素在$X(d)$中二分即可。

## I. One-Way Conveyors

题意：给出$n$个点$m$条边的无向图，第$i$条边连接$x_i$和$y_i$。有$k$对点$(a_i,b_i)$，表示$a_i$可以到达$b_i$。现在你要给每条边定向，使得其中$k$对点$(a_i,b_i)$能够满足条件。

$2 \le n \le 10^4, 1 \le m \le 10^5, 1 \le x_i < y_i \le n, 1 \le a_i, b_i \le n, a_i \ne b_i$

题解：考虑求出边双联通分量，然后双联通分量内部的点可以通过给边定向变成强连通（dfs一下，树边和返祖边方向相反即可）。剩下来的就是跨过双联通分量的，记录每个桥边被经过的次数和方向即可。

## J. Fun Region

题意：定义`spiral paths`为不相交的简单polyline并且对于每个节点都顺时针拐了一下。现在给出一个$n$个点的简单多边形，求出多边形内部能够用一条`spiral paths`到达所有的顶点构成的区域面积。

$3 \le n \le 2000, 0 \le x_i, y_i \le 10^4$

题解：考虑$A$，$B$和$C$相邻三个点，如果$ABC$不是凸的，那么$AB$右侧的点肯定都是不合法的。也就是说把所有这样的$AB$拿出来，然后切割多边形即可。

证明如下：

对于每个顶点$v$，令这个顶点通过`ccw spiral paths`能到的区域为$S(v)$，那么显然答案是$\cap_v S(v)$。

考虑相邻两个点$v_i$和$v_{i+1}$，如果$v_{i+1}$是凸的，那么显然有$S(v_{i+1}) \subseteq S(v_i)$。令$C$是所有非凸顶点的集合，那么答案是$\cap_{v \in C} S(v)$。

假设$v_{i+1}$不是凸的，令直线$v_i$$v_{i+1}$遇到的第一个多边形上点是$q$，可以发现$S(v_i)$肯定不包含任意一个$v_{i+1}q$右侧的点。

## K. Draw in Straight Lines

题意：给出一个$n \times m$的黑白染色后的格子。一开始全是白色的，你需要用最小代价把它染成这个样子，有以下操作：

+ 选一条$1 \times k$或者$k \times 1$的格子，染成黑色或者白色。代价为$ak+b$
+ 选一个$1 \times 1$的格子，染成黑色或者白色，代价为$c$。

要求：

+ 已经染成白色的不能被染成黑色
+ 已经染色的格子，最多只能再被染色一次。

$1 \le n,m \le 40, 0 \le a, b, c \le 40, c \le a+b$

题解：由于白色不能盖在黑的上面，那么我们可以考虑先涂黑的，然后涂白的，最后再搞单个的。其次，由于一开始底色是白色的，如果我们横着涂了一条黑色的，肯定不会在上面再横着涂一条白色。因为这样代价肯定不够优，同理竖着涂了一条黑色的也是类似。

对于每个位置$(i, j)$考虑这$4$个变量

+ $bh_{i,j}$表示位置$(i,j)$是否被横着染成了黑色
+ $bv_{i,j}$表示位置$(i,j)$是否没有被竖着染成了黑色
+ $wh_{i,j}$表示位置$(i,j)$是否被横着染成了白色
+ $wv_{i,j}$表示位置$(i,j)$是否没有被竖着染成了白色

仅考虑横着染成黑色的代价，显然是$a \sum_{i,j} bh_{i,j} + b \sum_{i,j} bh_{i,j} \cdot \overline{bh_{i,j+1}}$。类似的竖着染成黑色代价为$a \sum_{i,j} \overline{bv_{i,j}} + b \sum_{i,j} \overline{bv_{i,j}} \cdot bv_{i+1,j}$；横着染成白色的代价为$a \sum_{i,j} \overline{wh_{i,j}} + b \sum_{i,j} \overline{wv_{i,j}} \cdot wh_{i,j+1}$；竖着染成白色的代价为$a \sum_{i,j} wv_{i,j} + b \sum_{i,j} wv_{i,j} \cdot \overline{wv_{i+1,j}}$。

$\sum_{u,v} c_{u,v} x_u \overline{x_v}$的模型我们可以用最小割来考虑。设立源点$S$和汇点$T$：

+ 对于每个$bh_{i,j}$，连一条代价为$a$的边到汇点$T$；连一条代价为$b$的边到$bh_{i,j+1}$。
+ 对于每个$bv_{i,j}$，从源点$S$连一条代价为$a$的边过去；连一条代价为$b$的边到$bv_{i-1,j}$。
+ 对于每个$wh_{i,j}$，从源点$S$连一条代价为$a$的边过去；连一条代价为$b$的边到$wh_{i,j-1}$。
+ 对于每个$wv_{i,j}$，连一条代价为$a$的边到汇点$T$；连一条代价为$b$的边到$wv_{i+1,j}$。

接下来考虑单个个点染色的：
+ 点$(i,j)$如果要染成黑色的话，需要的代价是$c \times bv_{i,j} \overline{bh_{i,j}} + \infty \times (\overline{wh_{i,j}}+wv_{i,j})$。前者表示这个点没有被黑色的染过，后者表示不能在白色上染黑色。因此我们可以连一条从$bv_{i,j}$到$bh_{i,j}$，代价为$c$的边；一条从$S$到$wh_{i,j}$，代价为$\infty$的边；一条从$wv_{i,j}$到$T$，代价为$\infty$的边。
+ 点$(i,j)$如果要染成白色的话，需要的代价是$c \times (bh_{i,j} \overline{wv_{i,j}} + wh_{i,j} \overline{bv_{i,j}}) + \infty \times bh_{i,j} \overline{bv_{i,j}}$。前者表示这个点被黑色的染过但是没被白色染过，后者表示这个位置不能被染黑两次。因此我们可以连一条从$bh_{i,j}$到$bv_{i,j}$，代价为$\infty$的边；一条从$bh_{i,j}$到$wv_{i,j}$，代价为$c$的边；一条从$wh_{i,j}$到$bv_{i,j}$，代价为$c$的边。

显然，这个图从一个从$S$到$T$的最小割就是答案。