# VK Cup 2015

## VK Cup 2015 - Finals

+ [ ] [A. Matching Names](https://codeforces.com/contest/566/problem/A)
+ [ ] [B. Replicating Processes](https://codeforces.com/contest/566/problem/B)
+ [x] [C. Logistical Questions](https://codeforces.com/contest/566/problem/C)
+ [ ] [D. Restructuring Company](https://codeforces.com/contest/566/problem/D)
+ [ ] [E. Restoring Map](https://codeforces.com/contest/566/problem/E)
+ [ ] [F. Clique in the Divisibility Graph](https://codeforces.com/contest/566/problem/F)
+ [ ] [G. Max and Min](https://codeforces.com/contest/566/problem/G)

## C. Logistical Questions

题意：给出一个$n$个点的树，第$i$个点有个权值$w_i$，第$i$条边连接点$a_i$和$b_i$，边权为$l_i$。你需要找到一个点$x$，使得$f(x)=\sum_{i=1}^{n} w_i \cdot \text{dist}^{1.5}(i,x)$最小。

$1 \le n \le 200000, 0 \le w_i \le 10^8, 1 \le a_i, b_i \le n, a_i \ne b_i, 1 \le l_i \le 1000$

题解：考虑$x$在一条$a$到$b$的路径上，那么可以证明$f(x)$是凸的。因为考虑每个函数$f_i(x)=w_i \cdot \text{dist}^{1.5}(i,x)$，很显然这个是凸的。那么，$n$个凸函数相加最终的函数也是图的。

可以发现，对于任意一条$a$到$b$的路径，$f(x)$的值都是先递减，然后再递增的。那么对于任意一个点$v$，那么最多只存在一个方向，使得$f(x)$减少。因为如果至少有两个的话，那么你考虑这两个点构成的路径，这个函数就不是凸的了，矛盾。

因此如果能够快速找到这个递减的方向，我们就可以用树分治来做了。每次求出重心，然后往递减的那个子树走即可。

假设我们枚举一个点$u$为根，然后以$u$为根构建有根树。考虑固定$u$的一个儿子$v_i$，令$d_i$是仅考虑$y \in \text{Subtree}(v_i)$里的$f_y(x)$的导数之和，即$d_i=\frac{3}{2} \cdot \sum_{y} w_y \cdot \text{dist}(y,u)$。那么你可以发现，如果往$v_i$走，那么整体$f(x)$的导数为$d_i - \sum_{1 \le j \le m, j \ne i} d_j$，其中$m$是$u$的儿子个数。只要往导数小于$0$的方向走即可。