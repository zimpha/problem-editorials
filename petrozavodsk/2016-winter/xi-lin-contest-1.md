# Petrozavodsk Winter 2016. Day 5. Xi Lin Contest 1

+ [ ] [A. Alice’s Sequence]
+ [ ] [B. Bomb]
+ [ ] [C. Clique]
+ [ ] [D. Deque and Balls]
+ [ ] [E. Easy When You Know How]
+ [ ] [F. Four]
+ [ ] [G. GCD is a Joke]
+ [ ] [H. Prefix Suffix]
+ [x] [I. Triple]
+ [ ] [J. XOR Tree]

## I. Triple

题意：有一个 $n$ 个点树，每条边的长度是 $1$。求出满足条件的三元组 $(A, B, C)$ 的个数：$\text{dist}(A,B) \le \max\{\text{dist}(A,C), \text{dist}(B,C)\}$。

$3 \le n \le 10^5$

题解：不妨改成求满足 $\text{dist}(A,B) > \max\{\text{dist}(A,C), \text{dist}(B,C)\}$ 的三元组的数目，最终用 $n(n - 1)(n - 2)$减掉即可。

考虑树分治，对于每个分治中心$r$，我们统计满足：1. $r$ 在 $A$，$B$ 和 $C$ 三个点构成的虚树中；2. $\text{dist}(A,B) > \max\{\text{dist}(A,C), \text{dist}(B,C)\}$ 的三元组数目。

令 $r$ 的子树分别为 $u_1, u_2, \dots, u_k$，那么可以分成如下三种情况：

### 1. $A$，$B$ 和 $C$ 分别在 $r$ 的三个不同子树下

对于每个子树 $u_i$，我们能够处理出 $ht_i$ 表示高度和 $cnt_i(d)$ 表示距离 $r$ 距离为 $d$ 的点的个数。

假设 $A$，$B$ 和 $C$ 分别在的子树为 $u_i$，$u_j$ 和 $u_k$，不妨令 $i > \max(j, k)$，那么我们只需要顺序枚举 $i$ 和 $d$，维护

+ $add(x)$ 表示 $j < i$ 并且 $y > x$ 的 $cnt_j(y)$ 的和
+ $sub(x)$ 表示 $j < i$ 情况下 $(\sum_{y > x} cnt_j(y)) \cdot (\sum_{y > x} cnt_j(y) - 1)$ 的和

那么对答案的贡献就是

$$
cnt_i(d) \cdot (add(d+1) \cdot (add(d+1)-1) - sub(d+1))
$$

令 $d$ 从 $ht_i$ 开始 从大到小枚举就可以 $O(1)$ 顺便维护 $add(\cdot)$ 和 $sub(\cdot)$。

对于 $i < \min(j, k)$ 的情况，只需要倒着把上述过程做一遍即可。

对于 $j < i < k$ 的情况，只需要在做 $i < \min(j, k)$ 的情况时，和 $i > \min(j, k)$ 的信息结合起来就好了。

### 2. $B$ 和 $C$ 在 $r$ 的一棵子树下，$A$ 在另一棵子树下

类似第一种情况，我们不妨假设 $A$ 所在子树 $u_i$ 在 $B$ 和 $C$ 所在子树 $u_j$ 的后面，即 $i > j$。反过来枚举也可以处理 $i < j$ 的情况。

假设 $B$ 和 $C$ 的最近公共祖先为 $X$，那么我们在 DFS 子树 $u_j$ 的时候，可以用启发式合并的方法在 $X$ 出求出 $d=\max(\text{dist}(B,X),\text{dist}(C,X))$ 的二元组 $(B, C)$ 的数目，记为 $w(d)$。

那么我们要求 $\text{dist}(A,r) + \text{dist(X,r)} > d$，也就是说 $\text{dist}(A,r) > d - \text{dist(X,r)}$。

我们用树状数组或者线段树之类的数据结构维护 $cnt(d - \text{dist(X,r)}) = w(d)$ 的和，然后在 DFS 子树 $u_i$ 的时候做个区间查询即可。

### 3. $A$ 和 $B$ 或者 $C$ 在 $r$ 的一棵子树下，$C$ 或者 $B$ 在另一棵子树下

不妨只考虑左边的情况，两者是对称的，最后答案乘以 $2$ 即可。

同样，假设 $A$ 和 $B$ 所在子树 $u_i$ 在 $C$ 所在子树 $u_j$ 的后面，即 $i > j$。反过来枚举也可以处理 $i < j$ 的情况。

假设 $A$ 和 $B$ 的最近公共祖先为 $X$，我们在 DFS 子树 $u_i$ 的时候，可以用启发式合并的方法在 $X$ 出求出 $d=\text{dist}(A,X) > \text{dist}(B,X)$ 的二元组 $(A, B)$ 的数目，记为 $w(d)$。

那么我们要求 $\text{dist}(C,r) + \text{dist(X,r)} < d$，也就是说 $\text{dist}(B,r) < d - \text{dist(X,r)}$。

我们用树状数组或者线段树之类的数据结构维护 $cnt(d - \text{dist(X,r)}) = w(d)$ 的和，然后在 DFS 子树 $u_j$ 的时候做个区间查询即可。

总体复杂度是 $O(n \log^2 n)$。