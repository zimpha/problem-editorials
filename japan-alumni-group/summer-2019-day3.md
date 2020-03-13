# Japan Alumni Group Summer Camp 2019. Day3

+ [ ] [A. Union Ball](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2988?year=2019)
+ [ ] [B. AddMulSubDiv](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2989?year=2019)
+ [ ] [C. Shuttle Run](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2990?year=2019)
+ [ ] [D. XORANDORBAN](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2991?year=2019)
+ [ ] [E. Red Black Balloons](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2992?year=2019)
+ [x] [F. Invariant Tree](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2993?year=2019)
+ [ ] [G. Toss Cut Tree](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2994?year=2019)
+ [ ] [H. Colorful Tree](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2995?year=2019)
+ [ ] [I. Add](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2996?year=2019)
+ [ ] [J. Horizontal-Vertical Permutation](https://onlinejudge.u-aizu.ac.jp/challenges/sources/JAG/Summer/2997?year=2019)

## F. Invariant Tree

题意：给出一个长度为$n$的排列$p_1,p_2,\dots,p_n$，求出有多少$n$个点的树满足：如果$i$和$j$之间有边，那么$p_i$和$p_j$之间有边。

$1 \le n \le 300000$

题解：考虑把这个排列环分解，令大小为$x$环的个数是$c_x$。然后经过一下尝试和观察可以发现

+ 如果$i$和$j$同属于一个环，那么$i$和$j$不能有边
+ 如果$i$属于环$A$，$j$属于环$B$，那么仅当$|A| \mid |B|$或者$|B| \mid |A|$的时候，$i$和$j$才可能有边。
+ 如果$i$和$j$属于不同的环，那么$i$和$j$有边的话，环上其他点怎么连边也固定了
+ 所有环的最小长度要么是$1$，要么是$2$。

基于上述观察，我们可以按照环的长度依次加入每条边。首先考虑第一层，如果环的最小长度是$1$，那么第一层的方案数是$c_1^{c_1-2}$或者$1$，如果$c_1=1$的话。若干环的最小长度是$2$，那么第一层的方案数是$2^{c_2-1} \cdot c_2^{c_2-1}$，这是因为不同环之间只要有一条边确定了，另外一条边是也确定了。于是，可以从这$c_2$个环里各选一个点连成树，剩下的点也自动构成了一棵树，然后就再选一条边把这两棵树连起来即可。

加下来考虑非第一层的环$c_i$，可以发现这些环可以和之前环长是它约数的环连边，也就是说方案数为$w=\sum_{j | i, j < i} j \cdot c_j$。然后这些环也可以和其他长度为$i$的环连边，方案数为$i$。我们不妨枚举有$d$个环和之前的环连边了，那么这些环需要自己连成$d$个树。类比雪莱公式，我们可以得到如下的式子
$$
\sum_{d=1}^{n} \binom{c_i}{d} \cdot w^{d} \cdot (i \cdot c_i)^{c_i-d-1} \cdot id=w\cdot(w+i\cdot c_i)^{c_i-1}
$$

总体上，可以$O(n)$求出答案。