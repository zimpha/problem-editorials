# Petrozavodsk Summer 2020. Day 2. SPb SU LOUD ENOUGH Contest

+ [ ] [A. Abstract Circular Cover]
+ [ ] [B. Biggest Set Ever]
+ [ ] [C. Convex Sets On Graph]
+ [ ] [D. Delete Two Vertices Again]
+ [ ] [E. Easy One]
+ [ ] [F. Football]
+ [ ] [G. Game On Board]
+ [ ] [H. Hardcore String Counting 2]
+ [ ] [I. Inv]
+ [ ] [J. Justice For Everyone]
+ [ ] [K. Keep It Cool]
+ [ ] [L. Lower Algorithmics]

## A. Abstract Circular Cover

题意：考虑一个长度为 $n$ 的环，令 $c_{i,l}$ 是从 $i$ 开始长度为 $l$ 的圆弧的代价。对于每个 $k=1,2,\dots,n$，求出恰好用 $k$ 个圆弧覆盖整个环的最小代价。

$1 \le n \le 850, 1 \le c_{i,l} \le 10^6$

## B. Biggest Set Ever

题意：给出 $T$，$n$ 和 $rem$，求出有多少非负整数集合满足：1. 和不超过 $T$；2. 和模 $n$ 余 $rem$。对 $998244353$ 取模。

$0 \le rem < n \le 10^4, 1 \le T \le 10^{100000} - 1$

## C. Convex Sets On Graph

题意：给出 $n$ 个点 $m$ 条边的无向连通图，定义一个集合为 `convex` 当且仅当对于任意两个节点，他们之间的任意一条简单路径都在这个集合里。有多少子集是 `convex` 的，对 $998244353$ 取模。

$1 \le n \le 3 \cdot 10^5, n - 1 \le m \le 3 \cdot 10^5$

## D. Delete Two Vertices Again

题意：给出 $n$ 个点 $m$ 条边的无向连通图。对于每条边，求出删掉这条边的两个端点之后，整个图是否连通。

$3 \le n \le 3 \cdot 10^5, n - 1 \le m \le 3 \cdot 10^5$

## E. Easy One

题意：对于一个包含 `1` 和 `2` 的序列，你可以每次做如下操作：

+ 在某个位置插入一个 `1`，使得这个 `1` 在其他 `1` 的右边。如果没有 `1`，可以插入任何地方
+ 如果某个 `2` 的右侧没有 `1`，那么可以把这个 `2` 改成 `1`。
+ 删掉最右边的 `1`，是第一个操作的反操作。
+ 把最右边的 `1` 改成 `2`，是第二个操作的反操作。

给出 $a$，$b$ 和 $t$，求出从 $a$ 个 `1` 的序列，变成 $b$ 个 `2` 的序列，恰好操作 $t$ 次的方案数。对 $998244353$ 取模。

$0 \le a, b, t \le 10^6$

## F. Football

题意：你在 $(0,0)$ 处，要带着一个球到 $(x_t, y_t)$ 处，有个人在 $(x_o, y_o)$ 想要拦截你。人移动速度最大是 $s_p$，球可以以 $s_b$ 匀速飞。

求出你能够把球传给你的队友。

$-75 \le x_t, y_t, x_o, y_o \le 75, 1 \le s_p, s_b \le 75$

## G. Game On Board

题意：给出 $n \times m$ 的黑白染色格子。你按照这个规则染色：如果某个矩形的三个角都是黑色，那么可以把剩下的角也染成黑色。

求出最少一开始需要多少个格子被染色，以及初始局面的方案数。对 $998244353$ 取模。

$1 \le n, m \le 10^9$

## H. Hardcore String Counting 2

题意：给出 $n$，求出有多少 *square-free* 的仅包含 `a`，`b` 和 `c`的长度为 $n$ 的字符串。

$1 \le n \le 120$

## I. Inv

题意：排列 $p$ 是 *involution*，当且仅当对于所有 $i$ 都有 $p(p(i)) = i$。给出 $n$ 和 $k$，求出有多少长度为 $n$ 的 *involution*，恰好有 $k$ 个逆序对。对 $998244353$ 取模。

$1 \le n \le 500, 0 \le k \le \frac{n(n-1)}{2}$

## J. Justice For Everyone

题意：给出 $n$ 个不同的数 $a_1,a_2,\dots,a_n$，每次可以选择两个位置 $i_1 < i_2$，然后同时把 $a_{i_1}$ 和 $a_{i_2}$ 加一。要求任意时刻这 $n$ 个数都互不相同。

求出从 $a_1,a_2,\dots,a_n$ 变成 $b_1,b_2,\dots,b_n$ 的方案数，对 $998244353$ 取模。

$1 \le n \le 30, 1 \le a_i, b_i \le 200$

## K. Keep It Cool

题意：考虑所有满足 $1 \le a < b \le b$ 的数对 $(a,b)$ 和 这些数对构成的排列。一个排列是 *balanced* 当且仅当对于满足 $1 \le a < b < c \le n$ 的 $a$，$b$ 和 $c$ 都有：$(a,c)$ 在 $(a,b)$ 和 $(b,c)$ 中间。

另外给出 $m$ 个条件，要求 $(a_i,b_i)$ 必须在 $(c_i,d_i)$ 前面。求出有多少 *balanced* 排列，对 $998244353$ 取模。

$3 \le n \le 10, 0 \le m \le 10$

## L. Lower Algorithmics

题意：给出大小为 $n$ 的集合 $A$，每个数在 $1$ 到 $1000$ 范围内。求出用 $l$ 到 $r$ 个数，能够表示多少不同的和，对 $998244353$ 取模。同一个数可以被使用多次。

$1 \le n \le 1000, 1 \le l \le r \le 2000$