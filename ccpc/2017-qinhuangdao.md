# The 2017 China Collegiate Programming Contest, Qinhuangdao Site

+ [ ] [A. Balloon Robot](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370121)
+ [ ] [B. Expected Waiting Time](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370122)
- [ ] [C. Crusaders Quest](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370123)
- [ ] [D. Graph Generator](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370124)
- [ ] [E. String of CCPC](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370125)
- [ ] [F. Getting Lost](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370126)
- [ ] [G. Numbers](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370127)
- [ ] [H. Prime Set](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370128)
- [x] [I. Triangulation](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370129)
- [x] [J. Tree Equation](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370130)
- [ ] [K. Diversity and Variance](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370131)
- [ ] [L. One-Dimensional Maze](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370132)
- [ ] [M. Safest Buildings](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370133)

## I. Triangulation

题意：给出平面上$n$个点$(x_i, y_i)$，保证任意三点不共线。求出权值和最小的三角剖分，并输出方案数。点$i$和点$j$之间有边的话，代价为$w_{i,j}$。

$3 \le n \le 18, 0 \le x_i, y_i \le 10^6, 0 \le w_{i,j} \le 10^6$

题解：首先搞一些坐标偏移，使得任意两个点的$x$坐标都互不相同。接下来考虑一个三角剖分里一条从最左边点$p_1$到最右边点$p_m$路径$C=p_1 \to p_2 \to \dots \to p_m$，使得$p_i$的$x$坐标小于$p_{i+1}$的$x$坐标。假设这条路径不是上凸壳，那么以下情况必然有至少一种出现：

+ 存在一个$i$和这条路径上方的点$o$，使得$p_i.x < o.x < p_{i+1}.x$，且$p_i,p_{i+1},o$这三个点构成的三个点属于这个三角剖分。

+ 存在一个$i$，使得$p_{i-1},p_i,p_{i+1}$这三个点构成的三角形属于这个三角剖分。

证明如下：对于某两个非上凸壳上的相邻点$p_{i}$和$p_{i+1}$，一定存在一个在$C$上方的三角形其中一条边是$p_i \to p_{i+1}$。考虑这个三角形上另外一个点$o$，如果$o$的$x$坐标在$p_i$和$p_{i+1}$之间，那么满足了第一个情况，接下来假设第一种情况不存在，这个时候$o$肯定是某个$p_k$。那么考虑$o$和$p_i$的$x$坐标的大小关系，一开始$o.x > p_i.x$，到最后$o.x < p_i.x$。那么肯定存在一个$i$，使得第二种情况满足。

然后对于一条路径$C$，满足两种情况的三角形可能有多个，我们选取最左边那个。那么从下凸壳开始，每次加入这个最左边的三角形，一定可以不重不漏的遍历每个三角形，最终到达上凸壳。

因此考虑$dp(mask,i)$表示当前路径上点集是$mask$，上一次添加的三角形的对应了第$i$条边的最小权值以及对应的方案数。那么接下来枚举下一个三角形从第$j$ ($j \ge i$)条边加上去。有两种加法，分别对应两种情况，枚举一下即可。

复杂度$O(2^n n^2)$。

## J. Tree Equation

题意：定义了两棵有根树的乘法和加法操作，给出三棵有根树$A$，$B$和$C$。求出两棵有根树$x$和$Y$，使得$A \cdot X+B \cdot Y=C$。

$1 \le |A|, |B|, |C| \le 10^5$

题解：考虑$C$里面最深的叶子是属于$A \cdot X$还是$B \cdot Y$的，不妨考虑是$A \cdot X$的，其他情况类似。

考虑从这个叶子往上走$height(C)-height(A)$步走到一个节点$x$，那么如果有解的话以这个$x$为根的子树一定是$X$，于是我们能够求出$A \cdot X$了。把$A \cdot X$从$C$里删掉，用同样的方法可以求出$Y$。判定下是否合法即可。
