## Petrozavodsk Summer 2013. Day 2. Moscow SU ST + NNSU Contest

+ [ ] [A. Tree Puzzle](https://www.e-olymp.com/en/problems/6447)
+ [x] [B. Xoring Machine](https://www.e-olymp.com/en/problems/6448)
+ [x] [C. Reduce the Sequence](https://www.e-olymp.com/en/problems/6449)
+ [x] [D. Tree](https://www.e-olymp.com/en/problems/6450)
+ [x] [E. Magic Roads](https://www.e-olymp.com/en/problems/6451)
+ [x] [F. Patterns](https://www.e-olymp.com/en/problems/6452)
+ [x] [G. ABACABA Matching](https://www.e-olymp.com/en/problems/6453)
+ [ ] [H. Intervals](https://www.e-olymp.com/en/problems/6454)
+ [x] [I. Danger](https://www.e-olymp.com/en/problems/6455)
+ [x] [J. Redundent Edges](https://www.e-olymp.com/en/problems/6456)

## A. Tree Puzzle

题意：一棵高度为 $N$ 的满二叉树，根节点标号是 $1$，节点 $x$ 的左儿子是 $2x$，右儿子是 $2x+1$。每个点都有一个状态，用 `0` 和 `1` 表示。有这样一个操作：

+ 一开始选择一个点 $x$，翻转它的状态
+ 如果这个点不是叶子，那么挑一个它的儿子继续操作：如果 $x$ 的初始状态是 `0`，挑左儿子，否则挑右儿子。

给出一个序列：$x_a=1,\quad x_i=(x_{i-1} \cdot b + c) \pmod p$。如果 $x_i \ge T$，那么节点 $i$ 一开始的状态是 `1`，否则是 `0`。

求出把所有节点状态都改成 `0` 的最小操作次数。

$1 \le N \le 60, 0 \le a,c < p, 1 \le b < p, 2 \le p \le 10^6, 0 < T < p$，保证 $p$ 是质数。

## B. Xoring Machine

题意：对于一个长度为 $N$ 的序列 $x_1,x_2,\dots,x_N$，考虑如下两种操作：

+ `L`：考虑 $i=2,3,\dots,N$，$x_i=x_i \text{ xor } x_{i-1}$
+ `R`：考虑 $i=N,N-1,\dots,2$，$x_i=x_i \text{ xor } x_{i-1}$

给出初始序列 $x_1,x_2,\dots,x_N$ 和操作序列，求出最终的序列。

$1 \le N \le 30000, 0 \le x_i \le 10^9$

题解：可以发现这两个操作是互逆的，也就是说一对 `L` 和 `R` 可以互相抵消。因此，我们只需要将那个表达式处理成有多少个 `L` 或者 `R` 即可。

之后就是分 `L` 和 `R` 分别做即可。

## C. Reduce the Sequence

题意：给出一个长度为 $N$ 的序列 $a_1,a_2,\dots,a_N$。每次可以选择两个相邻的正整数，同时减去 $1$。求出最终序列的可能方案数，对 $10^9+7$ 取模。

$1 \le N \le 10^5, 1 \le a_i \le 300$

题解：假设 $b_1,b_2,\dots,b_n$ 是最终的序列，那么肯定要满足 $b_i \cdot b_{i-1} = 0$。令 $f(i, j)$ 表示考虑了前 $i$ 个数，最终 $b_i=j$ 的方案数，$g(i,j)$ 表示考虑了前 $i$ 个数，最终 $b_i=0$，且需要第 $i+1$ 个数消耗 $j$ 的方案数。

我们很容易得到，$f(i,j)=f(i-1,a[i]-j)+g(i-1,a[i]-j)$ 和 $g(i,j)=\sum_{k > a[i] - j} f(i - 1, j)$。

最终答案就是 $g(n,0)+\sum_{j} f(n,j)$。

## D. Tree

题意：给出 $N$ 个点的树，第 $i$ 个点颜色为 $c_i$，总共有 $C$ 种不同颜色。有 $Q$ 个操作：

+ 把节点 $v_i$ 颜色染成 $w_i$
+ 求出距离节点 $v_i$ 不超过 $k_i$ 的点里，本质不同的颜色个数。

$1 \le N \le 50000, 1 \le Q \le 10^5, 0 \le K \le 50, 1 \le C \le 50, 1 \le c_i \le C, 1 \le v_i \le N, 0 \le k_i \le K$

题解：先以 $1$ 为根构建有根树，然后维护 $cnt(u, x, c)$ 表示以 $u$ 为根的子树里，距离 $u$ 恰好 $x$ 的点中，颜色 $c$ 出现的次数；$cs(u,x)$ 表示以 $u$ 为根的子树里，距离 $u$ 恰好 $x$ 的点中所有颜色的集合。

那么对于修改操作，我们可以 $O(K)$ 的维护好两个数组。对于询问操作，可以 $O(K^2)$ 获得答案。

## E. Magic Roads

题意：有个 $N$ 个点 $M$ 条边的无向图，第 $i$ 条边连接 $a_i$ 和 $b_i$，权值为 $c_i$，一开始每条边状态都是 `1`。有 $Q$ 个操作：

+ 给出节点 $v_i$，把和 $v_i$ 相邻的边状态取反
+ 给出整数 $k_i$，求出所有状态为 `1` 的边里面，边权第 $k_i$ 小的边的标号

$2 \le N \le 500, 1 \le M \le \frac{N(N-1)}{2}, 1 \le Q \le 200000, 1 \le a_i, b_i \le N, 1 \le c_i \le 10^9, 1 \le v_i \le N, 1 \le k_i \le M$

题解：考虑用分块维护当前哪些边的状态是 `1`，块大小可以搞成 $N$。这样每次修改操作复杂度是 $O(N)$ 的，询问操作也是 $O(N)$ 的。总的复杂度 $O(QN)$。

## F. Patterns

题意：有 $N^2$ 个立方体，$6$ 个面上都有颜色，总共有 $6$ 种不同的颜色。有 $N \times N$ 的网格，你需要把这些立方体放上去。求出最终网格的颜色有多少可能性，对 $10^9+7$ 取模。

$1 \le N \le 5$

题解：令 $cnt(x)$ 表示某个最终局面中颜色 $x$ 的数目，可以发现 $cnt(\cdot)$ 一样的可以一起计算出答案来。

于是可以爆搜出所有可能的 $cnt(\cdot)$，之后组合数算一下即可。

## G. ABACABA Matching

题意：对于一个 $26$ 个字母的排列 $p_1,p_2,\dots,p_{26}$。定义

$$
\begin{aligned}
S_1 &=&  p_1 \\
S_2  &=&  S_1  +  p_2  +  S_1 \\
S_3  &=&  S_2  +  p_3  +  S_2 \\
&\dots& \\
S_{26}  &=&  S_{25}  +  p_{26}  +  S_{25}
\end{aligned}
$$

给出一个字符串 $T$，找到一个字母排列，使得能够通过修改最少的字符使得 $T$ 是的 $S_{26}$ 的子串。

$1 \le |T| \le 20000$

题解：令 $ctz(x)$ 是 $x$ 二进制表示中末尾 `0` 的个数，那么可以发现 $S_{26}$ 的第 $x$ 字符为 $p_{ctz(x) + 1}$。还可以发现 $S_{26}$ 是个高度回文对称的字符串。

对于 $T$ 在 $S_{26}$ 中出现位置，我们肯定可以找到一个回文中心，并且我们把这个中心放在 $2^{25}$ 处（也是 $p_{26}$ 唯一在的位置）肯定是不影响答案计算的。

我们不妨枚举 $T_o$ 在回文中心，那么可以发现对于位置 $i$，它应该填上的字符是 $p_{ctz(|i-p|) + 1}$，我们可以处理出一个数组 $cnt(x,y)$ 表示应该填 $p_x$ 的位置上现在有多少个 $p_y$。有了这个数组，我们只需要跑一个二分图最小权匹配，就可以知道最终的最优排列。

然后注意到，如果 $|i-p| \equiv 0 \pmod{2^t}$ 并且 $|i-p| \not\equiv 0 \pmod{2^{t+1}}$，那么位置 $i$ 应该填 $p_{t+1}$。

因此，我们对于每个 $t$，都应该处理出一个数组 $sum(t, e,x)$ 表示有多少 $i$ 满足 $i \equiv e \pmod{2^t}$ 并且 $T_e = c$。那么 $cnt(x,y)=sum(x, p \bmod 2^t,c)-sum(x + 1, p \bmod 2^{t+1},c)$。

## H. Intervals

题意：给出 `0` 到 `9` 里面哪些数位是好的，一个好的数仅由好的数位组成。给出 $N$ 个区间 $[l_i, R_i]$，要求从每个区间里选出一个数，然后加起来。求加起来数是好的的方案数，对 $10^9+7$ 取模。

$1 \le N \le 7, 0 \le L_i \le R_i \le 10^{10}$

## I. Danger

题意：给出 $N$ 个点的树，第 $i$ 条边连接 $u_i$ 和 $v_i$，边权为 $w_i$。有 $Q$ 个操作：

+ 给从 $v_i$ 到 $u_i$ 路径上的边边权都加上 $a_i$，最多只有 $500$ 个这样的操作。
+ 求出距离 $v_i$ 不超过 $k_i$ 的所有点构成的子树的边权和。

$1 \le N \le 1000, 0 \le Q \le 500000, 1 \le u_i, v_i, k_i \le N, 1 \le w_i, a_i \le 10^5$

题解：先 $O(n^2)$ 预处理出 $sum(v,k)$ 表示原来图上距离 $v$ 不超过 $k_i$ 的边权和。对于每个询问，仅需要考虑每个修改操作对这次询问的贡献。

也可以大力树分治，复杂度 $O(Q \log^2 n)$。

## J. Redundent Edges

题意：给出 $N$ 个点 $M$ 条边的有向图和一个起点 $R$。令 $C_0$ 是起点 $R$ 能够到达的点集。令 $C(e)$ 是删掉边 $e$ 之后，$R$ 能够到达的点集。一条边 $e$ 是 *redundant* 当且仅当 $C_0=C(e)$。求出所有 *redundant* 的边。

$1 \le N \le 10^5, 1 \le M \le 200000, 1 \le R \le N$

题解：对于每条边 $i$，新建一个点 $i+n$，从 $a_i$ 到 $i+n$ 连边，$i+n$ 到 $b_i$ 连边。对于这样一个新的有向图，我们需要求出以 $R$ 为根的 Dominator Tree。那些无法被 $R$ 遍历到或者作为叶节点的边就是 *redundant* 的边。