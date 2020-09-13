# Petrozavodsk Winter 2015. Day 9. Michael Tikhomirov Contest 1

+ [x] [A. Aarelia Mountains](https://www.acmicpc.net/problem/19208)
+ [x] [B. Bar "Duck"](https://www.acmicpc.net/problem/19209)
+ [x] [C. Collections In Containers](https://www.acmicpc.net/problem/19210)
+ [x] [D. 1D Spreadsheet](https://www.acmicpc.net/problem/19211)
+ [x] [E. Even Separation](https://www.acmicpc.net/problem/19212)
+ [x] [F. Fibonacci's Nightmare](https://www.acmicpc.net/problem/19213)
+ [x] [G. Guess The String](https://www.acmicpc.net/problem/19214)
+ [x] [H. Hilbert's Maze](https://www.acmicpc.net/problem/19215)
+ [x] [I. Infinite Binary Embedding](https://www.acmicpc.net/problem/19216)
+ [x] [J. Jitterbug](https://www.acmicpc.net/problem/19217)

## A. Aarelia Mountains

题意：有 $n$ 个数 $h_1,h_2,\dots,h_n$。你想让这些数非递减，也就是对于任意 $i$，都有 $h_i \le h_{i+1}$。有 $m$ 个操作，第 $i$ 个操作可以选择一个长度为 $l_i$ 的区间，都加上 $t_i$，代价为 $c_i$。最后每个数可以是负数，求出最小代价。

$1 \le n, m \le 200, 0 \le h_i \le 10^6, 1 \le c_i \le 10^6, 1 \le l_i \le n, t_i \in \{-1, 1\}$

题解：令 $a_i=h_i-h_{i-1}$，显然一个长度为 $l$ 的操作，就是把某个 $a_i$ 减去 $t$，$a_{i+l}$ 加上 $t$。显然，是从正的 $a_i$ 到某个负的 $a_j$ 比较优。

于是可以建立费用流模型，源点到所有正的 $a_i$ 连边，所有负的 $a_j$ 到汇点连边。如果负的 $a_j$ 满流的话就是有解，否则无解。 

## B. Bar "Duck"

题意：长度为 $L$ 的线段，上面有 $n$ 个障碍物，第 $i$ 个在 $x_i$，质量为 $m_i$。你可以给第 $i$ 个障碍物一个初始速度 $v_i$，然后选择匀速往左或者往右，消耗能量为 $\frac{m_iv_i^2}{2}$。

问在 $T$ 时间内，总能量不超过 $E$ 的情况下，最长的无障碍物子段的长度。

$1 \le n \le 10^5, 1 \le L, T, E \le 10^6, 0 < x_i < L, 1 \le m_i \le 10^3$

题解：二分答案 $d$，考虑如何判定。假设这个没有障碍物的区间左端点是 $z$，那么在区间 $[z, z+\frac{d}{2}]$ 里的障碍物显然都要往左走，在区间 $[z+\frac{d}{2}, z+d]$ 里的障碍物都要往右走。

可以发现 $z$ 的关键点有 $x_i$，$x_i-\frac{d}{2}$ 和 $x_i-d$。把关键点拿出来排序，那么如果 $z$ 在相邻两个关键点对应的区间里，$[z, z+\frac{d}{2}]$ 和 $[z+\frac{d}{2}, z+d]$ 里的障碍物集合是一样的。

于是对于每个这样的区间，都可以列出一个一元二次方程，求一下最值即可。

关键点可以通过归并的方式合并，这样就可以做到线性判定。

## C. Collections In Containers

题意：给你一个 $n$ 个 $d$ 维的向量集合，满足，如果存在向量 $a_1, a_2, ..., a_d$，那么对于任意 $b$，满足 $0 \leq b_i \leq a_i$ 都存在。

给出一个长度为 $n$ 的数组 $c_1,c_2,\dots,c_n$。你需要找到一个长度为 $n$ 的排列 $p$ 和 $q$，使得 $a_{p_i,j} + a_{q_i,j} \le c_j$。

$1 \le nd \le 10^5, 0 \le c_i \le 10^9, 0 \le v_{i,j} \le c_j$

题解：题目给定的 $c$ 其实没有多大用处，因为我们总是可以构造出一个 $c_j = \max_i(a_{i,j})$ 时候的解。

可以发现，题目给出的限制很强，我们任意去掉一维后这个性质还是满足的。其实题目给出的限制就是说集合是一个凸集。

考虑按照维数递归构造答案，假设我们需要构造满足前 $k$ 维的答案。把所有向量按照第 $k$ 维归类，值一样的归为同一类。那么对于同一类，我们可以递归搞出一个符合前 $k-1$ 维的解。接下来考虑如果使得第 $k$ 维也满足条件。

假设第 $k$ 维的最大值为 $m_k$，那么对于 $2 a_{i,k} \le m_k$ 的，肯定是满足条件的，因此我们需要调整 $2 a_{i,k} > m_k$ 的。对于这种 $a_{i,k}$，肯定存在另一个 $a_{j,k}=m_k-a_{i,k}$，使得 $a_{i,1..k-1} = a_{j,1..k-1}$。只需要交换它俩的匹配就可以使 $a_{i,k}$ 满足条件。

对于一个 $i$ 求出对应的 $j$ 的话，可以使用字符串 hash 来加速判定。

## D. 1D Spreadsheet

题意：有 $n$ 个格子，一开始第 $i$ 个格子包含一个数 $a_i$。有 $q$ 个操作，

+ 令格子 $i$ 包含数 $x$
+ 令格子 $i$ 指向格子 $j$
+ 求出格子 $l$ 到格子 $r$ 的权值和

如果一个格子包含一个数，那么这个格子的权值为这个数；否则这个格子的权值为它指向的格子的权值。保证不会出现循环指向。

$1 \le n, q \le 2 \times 10^5, -10^4 \le a_i, x \le 10^4, 1 \le i, j \le n, 1 \le l \le r \le n$

题解：考虑把操作分块，每 $L$ 次操作重建格子的指向关系和权值。对于一个询问操作，我们只需要关心最近的 $O(L)$ 个修改操作。

把这些操作涉及到的格子拿出来，记为关键点。那么我们可以先基于未修改的权值，求出一个答案来。由于这些关键点都被修改过了，那么需要减去这些关键点对答案的贡献，就是对应子树里面有多少节点在区间 $[l, r]$ 里。同时我们也可以在 $O(L)$ 时间处理出，这 $O(L)$ 个关键点现在的权值是多少。把新的权值乘上子树里面合法节点个数加回贡献即可。

令 $L = \sqrt{n \log n}$ 的话，复杂度是 $O(n \sqrt{n \log n})$。

## E. Even Separation

题意：给出 $n$ 个点 $m$ 条边的无向图。你需要把点分成两组，使得删掉连接不同组的边之后，每个点的度数都是偶数。

$1 \le n \le 500, 0 \le m \le \frac{n(n-1)}{2}$

题解：考虑用 $x_i=0/1$ 表示每个点属于哪个组，$deg_i$ 表示第 $i$ 个点当前的度数。可以发现，

+ 如果 $deg_i$ 是偶数，那么 $\sum_{j \in N(i)} x_j \equiv 0 \pmod 2$
+ 如果 $deg_i$ 是奇数，那么有 $\sum_{j \in N(i)} x_j \equiv \overline{x_i} \pmod 2$，即 $x_i + \sum_{j \in N(i)} x_j \equiv 1 \pmod 2$

于是，我们得到了一个异或方程组，高斯消元解一下就好了。

## F. Fibonacci's Nightmare

题意：考虑这样一个随机序列：$a_0 = 1$，$a_n$ 是随机选出来的 $a_i$ 和 $a_j$ ($0 \le i, j \le n - 1$)的和。

你需要求出 $a_n$ 的方差。

$0 \le n \le 10^6$

题解：考虑方差的公式 $Var(X)=E(X^2) - E^2(X)$，我们仅需要求出 $a^2_n$ 和 $a_n$ 的期望值。

先考虑 $a_n$ 的期望值，根据期望的线性性，显然有 

$$
E(a_n) = \frac{\sum\limits_{i=0}^{n-1}\sum\limits_{j=0}^{n-1} E(a_i)+E(a_j)}{n^2}=\frac{2\sum\limits_{i=0}^{n-1}E(a_i)}{n}
$$

最终其实可以发现，$E(a_n)=n+1$。

接下来考虑 $E(a^2_n)$，显然有

$$
\begin{aligned}
E(a^2_n) &=& \frac{\sum\limits_{i=0}^{n-1}\sum\limits_{j=0}^{n-1} E((a_i+a_j)^2)}{n^2} \\
&=& \frac{\sum\limits_{i=0}^{n-1}\sum\limits_{j=0}^{n-1} E(a_i^2+a_j^2+2a_ia_j)}{n^2} \\
&=& \frac{2 \sum\limits_{i=0}^{n-1}E(a_i^2)}{n}+\frac{2E((\sum\limits_{i=0}^{n-1}a_i))^2}{n^2}
\end{aligned}
$$

我们需要求出 $E((\sum\limits_{i=0}^{n}a_i)^2)$，可以拆成 $(a_n+\sum\limits_{i=0}^{n-1}a_i)^2$，化简下得到

$$
E((\sum\limits_{i=0}^{n}a_i)^2)=E(a_n^2)+E((\sum\limits_{i=0}^{n-1}a_i)^2)+E(a_n(\sum_{i=0}^{n-1}a_i))
$$

继续把 $a_n$ 拆掉的话，最终可以得到

$$
E((\sum\limits_{i=0}^{n}a_i)^2)=E(a_n^2)+\frac{(4+n)\cdot E((\sum_{i=0}^{n-1}a_i)^2)}{n}
$$

递推就可以算出答案了。

## G. Guess The String

题意：交互题。有一个长度不超过 $500$ 的字符串 $s$，仅有小写字母组成。每次你可以询问一个串 $t$ 是不是 $s$ 的子序列。所有询问中 $t$ 的总长不能超过 $6 \cdot 10^5$。

题解：先问出每个字符出现的次数，然后每次拿出两个最短的字符串合并。假设当前是 $z$，还剩 $x$ 和 $y$ 没有合并，就查一查 $z+x[0]+y$ 或者 $z+y[0]+x$ 是不是子序列就可以确定下一个字符是 $x[0]$ 还是 $y[0]$。

## H. Hilbert's Maze

题意：给出一个 $k$ 阶的 Hilbert's Maze，一个起点 $(x_s,y_s)$ 和终点 $(x_t, y_t)$。求出起点到终点的最短路。

$0 \le k \le 30, 1 \le x_s, y_s, x_t, y_t \le 2^{k+1}-1$

题解：对于每个点，我们先构造出一条从 $T_0$ 怎么演变到 $T_k$ 的路径。这条路径只需要记录：当前从这四条边的哪个位置出来以及到这个位置经过了多少距离。

对于两条这样的路径，我们可以找到他们的公共前缀，从这个位置开始，距离就可以独立计算了。因此，我们仅需要计算在这个公共前缀处，我们从一个点到另一个点的距离。

这个基本上可以分成三部分：外面正方形的轮廓线；上面的 $1 \times 2^k$ 的小区域；下面的 $T$ 型区域。对于后两者，我们最终都是要走到外轮廓的，除非两个点属于同一个区域。

## I. Infinite Binary Embedding

题意：给定一棵 $n$ 个节点的满二叉树 $T$ 和一棵无穷满二叉树 $I$。问有多少个从 $T$ 的结点到 $I$ 的结点的单射 $f$, 使得

+ 若 $v$ 是 $T$ 中的叶子，则 $f(v)$ 在 $I$ 中的深度为 $h_v$
+ 若 $v$ 是 $T$ 中 $u$ 的左孩子，则 $f(v)$ 在 $I$ 中是以 $f(u)$ 的左孩子为根的子树中的一个结点
+ 若 $v$ 是 $T$ 中 $u$ 的右孩子，则 $f(v)$ 在 $I$ 中是以 $f(u)$ 的右孩子为根的子树中的一个结点

$1 \le n \le 2000, 0 \le h_v \le 10^9$

题解：令 $dp(v, x)$ 表示 $T$ 中以 $v$ 为根的子树，$f(v)$ 在 $I$ 中深度至少为 $x$ 的方案数。显然，我们就是要求出 $dp(1, 0)$。

可以发现，$f(v)$ 在 $I$ 的哪个深度为 $h_v$ 的位置上并不重要，因为所有子树都是对称的。考虑如下的递推式

$$
dp(v, x) = 
\begin{cases}
2^{h_v} & v \text{ is leaf }, x \le h_v \\ 
\sum_{x \le y \le h_v}\frac{dp(lson(v), y+1)}{2^{y+1}} \cdot \frac{dp(rson(v), y+1)}{2^{y+1}} \cdot 2^y & \text{otherwise}
\end{cases}
$$

可以发现，如果我们令 $dp(v, x) = \sum_{i} a_i \cdot 2^{ix}$，那么我们就可以很方便的维护上面的转移式子。

对于一个 $v$，最大的 $i$，使得 $a_i$ 非零，只和 $v$ 的子树大小有关。因此可以在 $O(n^2)$ 做好转移。

## J. Jitterbug

题意：给出 $n$ 和 $b$，构造一个 $n$ 个点的图，使得从 $1$ 到 $n$ 的期望步数是 $b$。

$n = 200, b = 10^6$

题解：先构造 $100$ 个点的团，然后构造 $100$ 个点的链，接上即可。