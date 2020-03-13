# AtCoder Beginner Contest Selections

## [AtCoder Beginner Contest 155. F. Perils in Parallel](https://atcoder.jp/contests/abc155/tasks/abc155_f)

题意：$n$个位置$a_i$有灯泡，状态是$b_i$。有$m$个操作，每次可以把在$l_i$到$r_i$之间的灯泡取反。求出一个操作序列，使所有灯泡熄灭。

$1 \le n \le 10^5, 1 \le a_i \le 10^9, 0 \le b_i \le 1, 1 \le m \le 2 \times 10^5, 1 \le l_i, r_i \le 10^9$

题解：令$f(i)$表示位置$i$的灯泡状态，`1`表示亮着，`0`表示熄灭。然后令$g(i)=f(i) \oplus f(i+1)$，可以发现$f(i)=g(i) \oplus g(i+1) \oplus \dots \oplus g(10^9)$。

考虑对一个区间$[l, r]$取反，实际上是等价于把$g(l-1)$和$g(r)$取反。那么可以把一个操作看成连接点$l_i-1$和$r_i$的一条边，这样我们有了一个图。也就是说对于$g(\cdot)$里的每个$1$，我们找一对匹配一下，然后沿着一条路径操作下，这对$1$就消失了。