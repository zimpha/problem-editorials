# XIX Open Cup. Grand Prix of Xi'An

+ [x] [B. Mysterious Host](https://official.contest.yandex.ru/opencupXIX/contest/11340/problems/B/)

## B. Mysterious Host

题意：对于一个排列$p_1,p_2,\dots,p_n$和$q_1,q_2,\dots,q_n$，$p$和$q$等价当且仅当对于任意$1 \le i \le j \le n$，$p_{i..j}$和$q_{i..j}$要么同时连续，要么同时不连续。$p_{i..j}$连续等价于$\max(p_{i..j})-\min(p_{i..j})=j-i$。

给出$N$和$P$，对于$n=1,2,\dots,N$，求出长度为$n$的排列里有多少等价类，对$P$取模。

题解：考虑一个排列对应的析合树，可以发现$p$和$q$等价当且仅当$p$和$q$的析合树同构。于是我们只需要数有$n$片叶子的析合树个数即可。

可以发现对于一个和点，它至少有$2$个儿子；对于一个析点，它至少有$4$个儿子。那么，如果令$f(n,k)$表示有$n$片叶子，恰好有$k$棵树的析合树森林的个数，答案就是$\sum_{k=2}^{n}f(n,k)+\sum_{k=4}^{n}f(n,k)$。

稍微化简下得到$f(n,2)+f(n,3)+3\sum_{k=4}^{n}f(n,k)$。令$g(n)=\sum_{k=4}^{n}f(n,k)$，那么我们可以得到如下递推式。

$$
\begin{aligned}
f(n,1) = f(n,2)+f(n,3)+2 \cdot g(n) \\
f(n,2) = \sum_{i=1}^{n-1} f(n-i,1) \cdot f(i,1) \\
f(n,3) = \sum_{i=1}^{n-1} f(n-i,2) \cdot f(i,1) \\
g(n) = \sum_{i=1}^{n-1} (f(n-i,3)+g(n)) \cdot f(i,1)
\end{aligned}
$$

显然可以$O(n^2)$算出答案，也可以用分治FFT轻松得到$O(n \log n)$的做法。