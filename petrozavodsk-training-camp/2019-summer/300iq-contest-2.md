# 300iq Contest 2, Grand Prix of Kazan

- [ ] [A. Apollonian Network](https://codeforces.com/gym/102331/problem/A)
- [ ] [B. Bitwise Xor](https://codeforces.com/gym/102331/problem/B)
- [x] [C. Counting Cactus](https://codeforces.com/gym/102331/problem/C)
- [ ] [D. Determinant](https://codeforces.com/gym/102331/problem/D)
- [ ] [E. Easy Win](https://codeforces.com/gym/102331/problem/E)
- [ ] [F. Fast Spanning Tree](https://codeforces.com/gym/102331/problem/F)
- [ ] [G. Grammarly](https://codeforces.com/gym/102331/problem/G)
- [x] [H. Honorable Mention](https://codeforces.com/gym/102331/problem/H)
- [ ] [I. Interactive Vertex](https://codeforces.com/gym/102331/problem/I)
- [x] [J. Jiry Matchings](https://codeforces.com/gym/102331/problem/J)
- [ ] [K. K-pop Strings](https://codeforces.com/gym/102331/problem/K)

## C. Counting Cactus

题意：你有一个$n$个点$m$条边的图，求出有多少边的子集，使得选出来的构成了一个仙人掌，对$998244353$取模。

$1 \le n \le 13, 0 \le m \le \frac{n(n-1)}{2}$

题解：考虑容斥计算生成树的技巧$f(S)=\sum_{T \subseteq S, T \ne \empty}(-1)^{|T|-1}ways(S, T) \cdot f(S - T)$，其中$S$表示当前生成树的点集，$T$是枚举的一部分叶子，$ways(S,T)$表示把$T$接在$S-T$上的方案数。只要能够预处理出$ways(S,T)$，那么就能$O(3^n)$计算出这个东西。

类似的，仙人掌可以看成一堆环构成的树，如果把两个点的边也看上一个环的话。于是我们也可以用上述技巧，枚举叶子对应的那些环构成的点集$T$，然后进行转移。问题是如何快速计算$ways(S, T)$。

令$C(S)$表示点集$S$构成了一个环的方案数，这个可以用$O(2^n n^2)$的dp计算出来。然后令$CS(u,S)$表示从$u$这个节点挂出若干环，这些环构成的点集恰好是$S$的方案数。这个可以用枚举子集的方法在$O(3^n n^2)$的时间处理出来。

令$F(S,T,k)$表示若干个$CS(u_1,S_1),CS(u_2,S_2),\dots,CS(u_k,S_k)$拼起来，其中恰好有$k$个环的方案数，其中$S$是所有的$u_i$，$T=S_1 \cup S_2 \cup \cdots \cup S_k$并且$S_i \cap S_j = \empty$。有好多中能从$S^\prime$加一个$u$得到$S$的方法，不妨取$u$最大的那个$S^\prime$，于是就是把$CS(u,X)$和$F(S^\prime, Y)$做一个子集卷积得到$F(S, T)$。复杂度是$O(3^n n^2)$。

那么上述的容斥可以改成

$$
f(S)=\sum_{k=1}^{|S|}\sum_{H \subseteq S} \sum_{T \subseteq S}(-1)^{k-1}F(H,T,k) \cdot f(S-(T-H))
$$

上述复杂度是$O(4^n)$的，注意到在固定$T$的情况下$H \subseteq S$实际上一个OR卷积。我们也可以用FWT优化下，复杂度变成$O(3^n n^2)$。

别解：我们考虑包含$1$这个环，从$1$开始bfs，按照深度依次遍历所有环。我们按照点下标从小到大依次访问这些环。那么这样就可以唯一确定这个仙人掌。

考虑用dp模拟这个过程，$f(S,T)$表示当前点集是$S$，这次bfs还没处理的点集是$T$。然后我们每次枚举$T$里最小的点$u$，以及枚举一个子集$H$，把$f(S,T) \cdot CS(u,X)$更新到$f(S \cup X, T - \{u\})$上去。

这样就可以$O(4^n)$求出所有方案。比上一个做法简单很多。

## H. Honorable Mention

题意：你有一个长度为$n$的数组$a_1,a_2,\dots,a_n$。然后有$q$个询问，每次给出$l_i$，$r_i$和$k_i$。求出在$a[l_i..r_i]$里选出$k$个和最大的不相交连续子段。

$1 \le n,q \le 35000, -35000 \le a_i \le 35000, 1 \le l_i \le r_i \le n, 1 \le k \le r_i - l_i + 1$

题解：令$s_i=0/1$表示这个数取还是不取，同时令

$$
y_i=\begin{cases}1 & s_i=1, s_{i-1}=0 \\ 0 & s_i=0 \\ 0 \text{ or }1 & \text{otherwise} \end{cases}
$$

令$f(k)$是满足$\sum_{i=1}^{n}y_i=k$的$\sum_{i=1}^{n}s_i a_i$的最大值，那么显然$f(k)$就是原问题的答案。

可以注意到在固定了$s_0$和$s_n$的情况下，$f(k)-f(k-1) \ge f(k+1)-f(k)$。这个问题可以看成费用流问题，每次新增广的时候费用是递减的。于是$(k,f(k))$是凸的。

对整个数组构建线段树，利用上面的性质，我们就可以用$O(n \log n)$预处理出每个线段树节点的$f(\cdot)$数组。每个节点上维护$2 \times 2$个这样的$f(a,b,\cdot)$数组，表示$s_0=a,s_n=b$情况下的解。那么合并两个线段树节点$X$和$Y$的话，等价于枚举$a,b,c$，然后把$Xf(a,b,\cdot)$和$Yf(b,c,\cdot)$做一个`max`卷积。然后因为他们都是凸包，这个`max`卷积可以用`minkowski sum`来代替，复杂度是线性的。然后注意到$b=1$的时候，我们的$\sum_{i=1}^{n}y_i$其实多加了$1$，我们需要把这个得到的数组位移一下才是正确的结果。

有了上面的结构的话，我们可以来处理每个询问了。对于每个询问，由于$f(\cdot)$是凸的，我们可以用wqs二分来做。每次二分一个$x$，找到一个$u$使得$ux+f(u)$最大，同时使得$u$最小。根据$u$和$k$大小关系可以来决定二分的方向。

但是一个询问会被拆成$O(\log n)$个线段树节点，我们会得到$O(\log n)$个$(a,b,ux+f(u),u)$这样的四元组，用上面提到的方法合并即可。

这样整体复杂度是$O(n \log^2 n+q \log^2 n \log A)$。可以离线所有询问，用整体二分把复杂度变成$O(n \log^2 n+q \log n \log A)$。

## J. Jiry Matchings

题意：有一个$n$个点的带权树，第$i$条边连接$u_i$和$v_i$，权值为$w_i$。对于每个$k \le n - 1$，求出权值和最大的大小为$k$的匹配。

$2 \le n \le 200000, 1 \le u_i, v_i \le n, u_i \ne v_i, -10^9 \le w_i \le 10^9$

题解：令$f(k)$是我们想要求的答案，可以发现也有$f(k)-f(k-1) \ge f(k+1) - f(k)$，因此可以利用和H题类似的技巧来做这题。

考虑把整棵树树链剖分，对于每个节点$u$，维护：

+ $L^u_{inc}(k)$表示除去$u$的重儿子，恰好有$k$个匹配且包含节点$u$的最优值。
+ $L^u_{exc}(k)$表示除去$u$的重儿子，恰好有$k$个匹配且不包含节点$u$的最优值。

对于每条重链的起点$u$，我们需要计算：

+ $H^u_{inc}(k)$表示恰好有$k$个匹配且包含节点$u$的最优值。
+ $H^u_{exc}(k)$表示恰好有$k$个匹配且不包含节点$u$的最优值。

可以发现$H^u_{inc}(k)$和$H^u_{exc}(k)$就是把这条重链上的所有节点$v$的$L^v_{inc}(k)$和$L^v_{exc}(k)$全部依次合并起来，这个可以分治来做。下面考虑如何求$L^u_{inc}(k)$和$L^u_{exc}(k)$。

对于一个普通节点$u$，它的每个轻儿子$v$肯定都是一条重链的起点。那么先用上面的方法求出所有的$H^v_{inc}(k)$和$H^v_{exc}(k)$。然后考虑接上点$u$，得到$H^{uv}_{inc}(k)$和$H^{uv}_{exc}(k)$。那么$L^u_{inc}(k)$和$L^u_{exc}(k)$就是把$H^{uv}_{inc}(k)$和$H^{uv}_{exc}(k)$依次合并起来，这个也可以分治做。
