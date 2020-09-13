# Petrozavodsk Summer 2020. Day 1. Warsaw U Contest

+ [x] [A. Raid](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/A1/)
+ [x] [B. Broken line](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/B1/)
+ [x] [C. Territories](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/C1/)
+ [x] [D. Tea](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/D1/)
+ [x] [E. Three balls](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/E1/)
+ [x] [F. Family photo](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/F1/)
+ [x] [G. Pop music](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/G1/)
+ [x] [H. Island](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/H1/)
+ [x] [I. Goldfish and pikes](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/I1/)
+ [x] [J. Tokens](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/J1/)
+ [x] [K. Even rain](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/K1/)
+ [x] [L. Floyd-Warshall](https://official.contest.yandex.com/ptz-summer-2020/contest/19423/problems/L1/)

## A. Raid

题意：给出 $n$ 个数 $a_1,a_2,\dots,a_n$，对于每个 $k$ ($1 \le k \le n$)，你要从中选出一个长度为 $k$ 的子序列，使得逆序对最少。输出最小的逆序对个数和方案数。

$1 \le n \le 40, 1 \le a_i \le n, \forall i \ne j, a_i \ne a_j$

题解：考虑 $dp(i, state)$ 表示处理完前 $i$ 个数后当前状态为 $state$ 的时候的逆序对最小值，$ways(i,state)$ 同理，表示最小值条件下的方案数。$state$ 如果直接表示为哪些数选还是没选显然是不太行的。观察到当处理完前 $i$ 个数后，只有 $a_{i+1},\dots,a_n$ 才可能被选上。不妨对这些数排个序，假设为 $b_1 < b_2 < \dots < b_k$，其中 $k=n-i$。

那么，其实我们不关心之前选了哪些数，只关心之前数和 $b_i$ 的大小关系。不妨令 $state$ 记录 $[1,b_1),[b_1,b_2),\dots,[b_{k-1}, b_k),[b_k,n+1)$ 对于这里面每个区间，已经选的数有多少落在了里面。这样我们选或者不选一个 $b_i$，都能快速维护维护 $state$，也能方便进行转移。而且 $state$ 也是可以用一个 $64$ 位整数来存储的，落在区间 $[b_i,b_{i+1})$ 里的个数就是这些对应位里面 `1` 的个数。

然后可以证明这样状态数最多只有 $O(3^{n/3})$，足以过这个题。

## B. Broken line

题意：给出一个字符串 $s$，由前 $16$ 个小写字母组成。你现在可以把每个字母替换成 $\uparrow$ 或者 $\rightarrow$。然后从 $(0,0)$ 出发，遍历字符串 $s$，遇到 $\uparrow$ 向上走一步，遇到 $\rightarrow$ 向右走一步。求出折线下方覆盖面积的最大值。

$1 \le |s| \le 300000$

题解：对于一个由 $\uparrow$ 和 $\rightarrow$ 组成的序列，考虑每个 $\rightarrow$，它对答案的贡献就是左边 $\uparrow$ 的个数。于是我们可以先预处理出 $cnt(x,y)$ 表示字符 $x$ 出现在字符 $y$ 的次数。然后可以 $2^{16}$ 枚举每个字符变成什么东西，根据 $cnt(x,y)$ 就可以统计出答案。复杂度$O(|s|\cdot k + 2^k k^2)$。

## C. Territories

题意：有一个 $X \times Y$ 的网格，给出其中 $n$ 个子矩形左下角是 $(x_i,y_i)$，右上角是 $(x_i^\prime,y_i^\prime)$，要在第 $i$ 个矩形外面放置 $c_i$ 个元素。一个格子如果放了 $p$ 个元素，那么代价是 $\frac{p(p-1)}{2}$。求出一个放置方案使得代价和最大。

$1 \le n \le 10^5, 1 \le X, Y \le 1000, 1 \le x_i \le x_i^\prime, 1 \le y_i \le y_i^\prime, 1 \le c_i \le 1000$

题解：首先可以证明最多只有一个非网格 $4$ 个角的位置会放元素。然后假设你枚举了一个中间位置 $p$ 后，可以发现剩下最多需要两个角，且一定是两个对角，假设为左上角和右下角。你可以把矩形分成一下几类：

+ 仅包含左上角：那么这些可以把元素放到 $p$ 或者右下角；
+ 仅包含 $p$：那么这些可以把元素放到左上角或者右下角；
+ 仅包含右下角：那么这些可以把元素放到左上角或者 $p$；
+ 同时包含左上角和 $p$：这些矩形只能放在右下角
+ 同时包含右下角和 $p$：这些矩形只能放在左上角
+ 这三个点都不包含：可以任意放

$2^3$ 枚举前三种情况怎么放，然后选个最大的放最后一种即可。也可以努力分析一下把 $2^3$ 的枚举去掉。

## D. Tea

题意：有 $n$ 杯水，第 $i$ 杯体积为 $l_i$，初始温度为 $a_i$，目标温度为 $b_i$。现在你可以通过混合的方式得到其它温度的水，或者交换杯水的位置。问最终能否使第 $i$ 杯水体积为 $l_i$，温度为 $b_i$。

$1 \le n \le 10^5, 1 \le l_i, a_i, b_i \le 10^6$

题解：把体积为 $l$，温度为 $a$ 的一杯水看成 $l$ 杯体积为 $1$，温度为 $a$ 的水。你把这些水按照温度从大到小排序，目标状态也是一样。那么肯定每杯体积为 $1$ 的水初始温度和最终温度定了。接下来考虑模拟，一杯水从温度低的到温度高的需要吸收热量，反之需要放出热量。只要从高到低模拟的时候当前不需要额外提供热量(也就是放出的热量有足够的量供别人吸收)，那么肯定是可行的，否则是不行的。最后还需要考虑总热量守恒。

复杂度 $O(n \log n)$。

## E. Three balls

题意：给出 $3$ 个长度为 $n$ 的 `01` 串 $s_1,s_2,s_3$，以及三个整数 $r_1,r_2,r_3$。求出有多少长度为 $n$ 的 `01` 串 $s$，满足：至少存在一个 $i$，使得 $s$ 和 $s_i$ 的 Hamming 距离不超过 $r_i$。对 $10^9+7$ 取模。

$1 \le n \le 10^4, 0 \le r_i \le n$

题解：考虑容斥，令 $S_i$ 表示，满足 $s_i$ 的串的集合，那么答案就是

$$
|S_1|+|S_2|+|S_3|-|S_1 \cap S_2| - |S_1 \cap S_3| - |S_2 \cap S_3| + |S_1 \cap S_2 \cap S_3|
$$

显然，$|S_i|=\sum_{k=0}^{r_i} \binom{r_i}{k}$。

然后考虑 $|S_i \cap S_j|$。

令 $s^\prime=s_i \text{ XOR } s_j$，那么问题可以转换成求有多少串 $s$ 满足：有不超过 $r_i$ 个 `1` 且和 $s^\prime$ 不同位置不超过 $r_j$个。令 $c_0$ 和 $c_1$ 分别表示 $s^\prime$ 中 `0` 的个数和 `1` 的个数。然后我们要把不超过 $r_i$ 个 `1` 分 $x$ 个到 `0` 那，分 $y$ 个到 `1` 那。显然要满足 $a+c_1-b \le r_j$，于是方案数就是

$$
|S_i \cap S_j|=\sum_{x=0}^{r_i}\sum_{y=\max(0,a+c_1-r_j)}^{\min(r_i-x,c_1)}\binom{c_0}{x} \binom{c_1}{b}
$$

接下来考虑 $|S_1 \cap S_2 \cap S_3|$。

和上面一样，我们做同样的转化 $s_2^\prime=s_1 \text{ XOR }s_2,s_3^\prime=s_1 \text{ XOR }s_3$。变成求有多少串 $s$ 满足：有不超过 $r_i$ 个 `1` 且和 $s_i^\prime$ 不同位置不超过 $r_j$ 个。

令 $c_{00},c_{01},c_{10},c_{11}$，分别表示 $s_2^\prime$ 和 $s_3^\prime$ 对应位置分别是 `0` 或者 `1` 的位置个数。同样，需要把然后我们要把不超过 $r_1$ 个 `1` 分 $a$ 个到 `00` 那，$b$ 个到 `01` 那，$c$ 个到 `10` 那，$d$ 个到 `11` 那。然后可以列出以下不等式

$$
\begin{aligned} a \le c_{00}, b \le c_{01}, c \le c_{10}, d \le c_{11} \\ a+b+c+d \le r_1 \\ a+b+c_{10}-c+c_{11}-d \le r_1 \\ a+c_{01}-b+c+c_{11}-d \le r_2 \end{aligned}
$$

稍微化简整理下可以得到

$$
\begin{aligned} a \le c_{00}, b \le c_{01}, c \le c_{10}, d \le c_{11} \\ a+b \le \min(r_1-c_{10}-c_{11}+c+d, r_0-(c+d)) \\ a-b \le r_2-c_{01}-c_{11}+d-c \end{aligned}
$$

变成了一个二维数点问题。由于坐标范围都是 $O(n)$ 的，可以用 $O(n^2)$ 的暴力去做。

## F. Family photo

题意：有一棵 $n$ 个点的有根树，你需要找出一个最长的序列 $a_1,a_2,\dots,a_m$，使得 $a_i$ 是 $a_{i+1}$ 的祖先或者 $a_{i+1}$ 是 $a_i$ 的祖先。

$2 \le n \le 300000$

题解：考虑每个节点 $u$ 维护一个优先队列，队列里前 $k$ 大的数之和其实表示如果再新增 $k$ 个祖先的最优值。那么你在 dfs 过程中，先把儿子的优先队列都合并了。然后取出最大和次大，相加后再加 $1$ 塞回队列里面。这样最后根节点队列里最大值就是答案。

用左偏树维护的话，可以做到 $O(n \log n)$。

## G. Pop music

题意：给出 $n$ 个数 $a_1,a_2,\dots,a_n$。求出一个序列 $b_1,b_2,\dots,b_n$，使得：

+ $0 \le b_1 < b_2 < \dots < b_n \le m$
+ $\sum\limits_{i=1}^{n} a_i \cdot \text{popcount}(b_i)$ 最大

$1 \le n \le 200, n-1 \le m \le 10^{18}, -10^{14} \le a_i \le 10^{14}$

题解：假设我们有一棵包含 $1$ 到 $m$ 的 trie，那么就可以在 trie 上 dp 了。令 $f(x,l,r)$ 表示当前在节点 $x$，还有区间 $b[l..r]$ 还没有被确定。那么我们就可以枚举 $b[l..k]$ 往 $x$ 的左子树走，$b[k+1..r]$ 往 $x$ 的右子树走，进行转移。

可以观察到这颗 trie 其实分成了两部分节点，一部分节点是一棵完全二叉树，一部分节点不是完全二叉树。对于那些是完全二叉树的节点，我们只关心它的树高。对于那些非完全二叉树的节点，总共只有 $O(\log m)$ 个。

于是按照这两类节点，分别做 dp 即可，复杂度 $O(n^3 \log m)$。

## H. Island

题意：有一个小岛，中间有个湖。有 $n$ 个点，其中 $a$ 个沿着湖依次标号为 $1$ 到 $a$；其中 $b$ 个沿着海岸线依次标号为 $a+1$ 到 $a+b$。其中有 $m$ 条边，有些边是有向边，有些边是无向边。保证构成了一个平面图。

现在要选出一个 $\{a+1,a+2,\dots,a+b\}$ 的非空子集，使得 $1$ 到 $a$ 的每个点能够到达子集里至少一个点。求方案数，对 $10^9+7$ 取模。

$2 \le n \le 500000, 1 \le m \le 10^6, a,b \ge 1, a + b \le n$

题解：首先题目的各种限制保证了湖上一个点能够遍历到的海岸线上的点一定是个区间。那么可以先缩点，然后在这个有向无环图上dp出这些区间。

之后变成环上有若干区间，然后选若干点使得每个区间内至少有一个点。这个问题在线段上是可以做到 $O(n)$ 的。

由于给定的是平面图，然后有一个不会证明的猜测：区间个数和区间最小长度的乘积不是很大（可能是 $O(n)$ 或者 $O(n^{1.5})$）。于是就可以找个最小的区间，枚举在哪个位置切开这个区间。之后就是一个线段上的问题了。

## I. Goldfish and pikes

题意：有 $n$ 个物品，第 $i$ 个大小为 $w_i$。给出 $q$ 个操作：

+ $1\ s\ k$：询问初始值为 $s$，每次可以选择一个小于 $s$ 的 $w_i$，删掉并加到 $s$ 上去。求出最小操作次数，使得 $s \ge k$。
+ $2\ w$：加入一个重量为 $w$ 的物品。
+ $3\ w$：删去一个重量为 $w$ 的物品。

$1 \le n \le 300000, 1 \le q \le 10^5, 1 \le s, k \le 10^{18}, 1 \le w, w_i \le 10^{12}$

题解：考虑暴力模拟上述过程，假设下一个大于等于 $s$ 数是 $x$，那么我们肯定是先把 $s$ 变成至少 $x+1$ 是最优的。于是可以选出一些小于 $s$ 的数，使得他们加在 $s$ 上大于等于 $x+1$，并删掉这些数。之后，我们重复这个过程，直到到达 $k$ 为止。

上述暴力的复杂度就是 $O(\log k)$ 的，因为考虑一次模拟中，我们获得了一个比 $s$ 大的数 $x$，那么下一次 $x$ 肯定可以加在 $s$ 上，这样会至少让 $s$ 翻倍。于是最多不会超过 $2 \lfloor \log_2{\frac{k}{s}}+1 \rfloor$ 轮模拟。

用平衡树模拟即可，模拟结束后需要把删掉的数依次加回去。总的复杂度 $O(q \log^2 k)$。

## J. Tokens

题意：给出两个 $A \times B \times C$ 的三维矩阵，每次可以找一个 $a_{i,j,k} \ge 1$ 做如下三种操作：

+ $a_{i,j,k} - 1$ 同时 $a_{i+1,j,k}+1$
+ $a_{i,j,k} - 1$ 同时 $a_{i,j+1,k}+1$
+ $a_{i,j,k} - 1$ 同时 $a_{i,j,k+1}+1$

求出能否从第一个变成第二个。

$1 \le A \le 10000, 1 \le B, C \le 6$

题解：考虑构建一个二分图，左边点是第一个矩阵，右边点是第二个矩阵，然后如果能从一个点到另一个点就连一条边。考虑 Hall 定理，无解等价于存在一个左边点子集，它的和大于相邻的右边点集合。

观察可以发现，我们选取左边点集合的时候，如果 $(i,j,k)$ 选了，那么 $(i^\prime,j^\prime,k^\prime)$ ($i \le i^\prime, j \le j^\prime, k \le k^\prime$) 也会选，因为这样才能最大化左边的和。因此每一层左边点集合肯定是一个阶梯状的东西，这个东西最多有 $\binom{B+C}{C}$ 个。我们可以逐层 dp，只要这一层选取的阶梯轮廓完全在下一层选取轮廓的忧伤那么就是合法的。

如果一开始预处理好所有的轮廓线和合法的转移，那么复杂度是 $O(A \binom{B+C}{C} \min(B, C))$ 的。

## K. Even rain

题意：给出 $n$ 个数 $h_1,h_2,\dots,h_n$，你可以把其中 $m$ 个数变成 $0$。求出能够使得下雨后积水总量是偶数的修改方案数，对 $10^9+7$ 取模。

$1 \le n \le 25000, 0 \le m \le \min(25, n-1)$

题意：令 $prefix_i$ 表示 $h_1,h_2,\dots,h_i$ 的最大值，$suffix_i$ 表示 $h_i,h_{i+1},\dots,h_n$ 的最大值，那么显然积水量为 $\sum_{i=1}^{n} \min(prefix_i, suffix_i) - h_i$。

不妨从另一个角度考虑，我们固定一个 $h_x$ 表示序列里面的最大值，那么上面的式子其实可以改成 $\sum_{i=1}^{x-1} (prefix_i - h_i) + \sum_{i=x+1}^{n} (suffix_i - h_i)$，这样就把答案里面的 $\min$ 给去掉了。

那么左右两侧式子可以分开 dp，不妨先考虑左边。令 $f(i, j, k, e)$ 表示考虑了 $h_1,h_2,\dots,h_i$，当前最大值为 $j$，我们总共删掉了 $k$ 个数，然后当前积水量的奇偶性是 $e$ 的方案数。转移方程就是考虑 $h_{i+1}$ 取还是不取，取了的话还得考虑是否会更新 $j$，比较容易写出来。然后，可以观察到最多只有 $m+1$ 个 $j$ 是有用的，我们先处理出来并离散化。这样就可以做到 $O(nm^2)$ 处理出这个dp数组。

同理，我们可以求出 $g(i,j,k,e)$ 表示考虑了 $h_i,h_{i+1},\dots,h_n$，当前最大值为 $j$，我们总共删掉了 $k$ 个数，然后当前积水量的奇偶性是 $e$ 的方案数。

接下来我们考虑枚举 $h_x$，注意到同一个序列里面可能有多个最大值，我们取 $x$ 最小的那个。那么这个 $h_x$ 对答案的贡献就是

$$
\sum_{k=0}^{m} \sum_{e=0}^{1} \sum_{a=0}^{h_x-1} f(i - 1, a, k, e) \cdot \sum_{b=0}^{h_x} g(i+1,b,m-k,e)
$$

右侧括号里两个式子都可以先预处理出来，也可以做到 $O(nm^2)$ 的复杂度。

## L. Floyd-Warshall

题意：有一个 $n$ 个点 $m$ 条边的带权无向图，考虑如下的 `Floyd-Warshall` 实现

```python
for x in range(1, n + 1):
  for y in range(1, n + 1):
    for z in range(1, n + 1):
      M[y][z] = min(M[y][z], M[y][x] + M[x][z])
```

现在你不小心交换了询问的顺序，变成了下面的实现

```python
for y in range(1, n + 1):
  for z in range(1, n + 1):
    for x in range(1, n + 1):
      M[y][z] = min(M[y][z], M[y][x] + M[x][z])
```

求出有多少位置 $(y,z)$ 算出来还是对的。

$2 \le n \le 2000, 1 \le m \le 3000, 1 \le u_i, v_i \le n, 1 \le w_i \le 100000$

题解：考虑第二个算法什么时候值是对的：

+ 如果 $x$ 到 $y$ 之间有一条 $w$ 的边，并且最短路 $dist(x,y)=w$，显然这时候 $M[x][y]$ 是对的
+ 否则，如果存在一个 $z$，使得 $z$ 在 $x$ 到 $y$ 的最短路上，并且 $M[x][z]$ 和 $M[z][y]$ 都是对的，那么 $M[x][y]$ 是对的。

那么做法就显然了，我们用 `std::bitset` 维护 $f_x(y)$ 表示 $M[x][y]$ 的值是对的，$g_y(x)$ 表示 $M[x][y]$ 的值是对的，$on_{x,y}(z)$ 表示 $z$ 在 $x$ 到 $y$ 的最短路上。

对于 $on_{x,y}(z)$ 可以先求出 $x$ 到其他点的最短路，然后按照最短路从小到大把点排序。接下来依次考虑每个点 $v$ 和 $v$ 的入边们，如果有一条权值为 $w$ 的从边 $u$ 到 $v$ 边，并且 $dist(x,u)+w=dist(v)$，那么 $on_{x,v} = on_{x,v} \text{ | } on_{x,u}$。这样就可以 $O(\frac{n^2m}{w})$ 的复杂度求出所有的 $on_{x,y}$。

之后再枚举 $x$ 和 $y$，判断 $f_x \text{ AND } g_y \text{ AND } on_{x, y}$ 是否为空即可。同时也维护好 $f_x$ 和 $g_y$ 的值，复杂度是 $O(\frac{n^3}{w})$。