# Dwango Programming Contest 6th

+ [x] [A. Falling Asleep](https://atcoder.jp/contests/dwacon6th-prelims/tasks/dwacon6th_prelims_a)
+ [x] [B. Fusing Slimes](https://atcoder.jp/contests/dwacon6th-prelims/tasks/dwacon6th_prelims_b)
+ [x] [C. Cookie Distribution](https://atcoder.jp/contests/dwacon6th-prelims/tasks/dwacon6th_prelims_c)
+ [x] [D. Arrangement](https://atcoder.jp/contests/dwacon6th-prelims/tasks/dwacon6th_prelims_d)
+ [x] [E. Span Covering](https://atcoder.jp/contests/dwacon6th-prelims/tasks/dwacon6th_prelims_e)

## A. Falling Asleep

题意：略

题解：略

## B. Fusing Slimes

题意：数轴上有$N$个点，从左往右第$i$个点在位置$x_i$处。进行以下操作$N-1$次，在第$i$次操作：

+ 随机选一次$1$到$N-i$的整数$k$
+ 把从左往右第$k$个点移动到第$k+1$个点处
+ 这两个点合并为同一个点

求出每个点移动距离之和乘以$(N-1)!$，对$10^9+7$取模。

$2 \le N \le 10^5, 1 \le x_1 < x_2 < \dots < x_N \le 10^9$

题解：考虑$x_{i+1}-x_i$对答案的贡献，肯定是存在一个$j \le i$使得$[j+1,i]$之间的数都先于$j$被取走，这个的概率是$\frac{1}{i-j+1}$。答案就是$\sum_{i}^{N-1}(x_{i+1}-x_i)\sum_{j=1}^{i}\frac{1}{j}$。

## C. Cookie Distribution

题意：有$N$个小孩，在接下来的$K$天，第$i$天你会随机选$a_i$个小孩，给他们每人一个饼干。

求出$c_i \times c_2 \times \dots \times c_N$的期望乘以$\binom{N}{a_1} \times \binom{N}{a_2} \times \dots \times \binom{N}{a_K}$，其中$c_i$是第$i$个人总共收到的饼干数目。对$10^9+7$取模。

$1 \le N \le 1000, 1 \le K \le 20, 1 \le a_i \le N$

题解：其实$c_i$可以写成一个$K$维`01`串，$c_{i,j}=1$表示这个小孩在这$j$天里收到饼干。在$sum_{i=1}^{N}c_{i,j}=a_j$的条件下，我们要求的东西就是求出有多少$N$元组$(j_1,j_2,\dots,j_N)$使得$a_{i,j_i}=1$。

令$dp(i,j)$表示处理到第$i$列，选出了$j$个$1$的方案数。枚举当前列新加入$k$个$1$即可，$\binom{N-j}{k} \cdot \binom{N-k}{a_i-k} \cdot dp(i,j) \to dp(i+1,j+k)$。

## D. Arrangement

题意：给出$N$个数$a_1,a_2,\dots,a_N$。你需要构造一个字典序的排列$b_1,b_2,\dots,b_N$，使得$i$右边那个数不是$a_i$。

$2 \le N \le 10^5, 1 \le a_i \le N$

题解：对于每个位置考虑从小到大试每个数是否能够放下。对于题目给树的数组，按照$i \to a_i$建立一个环套树。假设当前没被放下的最小值为$x$，那么$x$可以放在当前位置当且仅当以下情况不会出现：

+ $a_x$存在，且$a_x$的度数是剩下点个数减$1$。
+ 只剩三个点了，且删掉$x$后是一个二元环。

## E. Span Covering

题意：有一个$[0, X)$的区间，你有$N$个线段，第$i$个长度为$L_i$。你需要给每个$i$选择一个$j$ ($0 \le j \le X - L_i$)，然后用第$i$条线段覆盖$[j,j+L_i)$。求把$[0, X)$整个覆盖的方案数。

$1 \le N \le 100, 1 \le L_i \le X \le 500$

题解：考虑容斥，假设有至少$k$个点没有被覆盖，这个等价于要找出$k+1$个非负的整数$a_0,a_1,\dots,a_k$使得$a_0+a_1+\dots+a_k=X-k$。然后这个对答案的贡献是$(-1)^k\sum_{i=1}^{N} \sum_{a_j \ge L_i} (a_j - L_i+1)$。

假设$a_0 \ge a_1 \ge \dots \ge a_k$，可以用$dp(l,j,k)$表示用到权值大于$l$的数，$a_0,a_1,\dots,a_j$已经确定了，$a_0+a_1+\dots+a_j=k$的时候，上面式子的贡献。考虑枚举$i$出现了$x$次，那么有如下的贡献：$(-1)^x \cdot \binom{j+x}{x} \cdot dp(l,j,k) \to dp(l-1,j+x,k+ix)$。

如果存在$L_i=l$，可以发现$\sum_{a_j \ge L_i} (a_j - L_i+1)$其实就是$k-jl+j$。乘上去即可。

最后答案就是$\sum_{i=0}^{X}dp(0,i,X-i)$。

复杂度是$O(X^3 \log X)$的，足够过这个题了。

别解：考虑我们按照$L_1 \ge L_2 \ge \dots \ge L_N$的顺序依次确定每个线段的位置。在某个时刻，会有$k$个互不相交的已经被覆盖的区间$[l_1,r_1),[l_2,r_2),\dots,[l_k,r_k)$。我们的目的就是要使他们区间长度之和满足$\sum_{i=1}^{k}r_i-l_i=X$。

令$dp(i,j,k)$表示我们已经放下了$L_1,L_2,\dots,L_{i}$，构成了$j$个互不相交的区间，他们的长度之和为$k$的方案数。考虑加入$L_{i+1}$会发生的几种情况：

+ 这个直接作为一个新的区间，$dp(i,j,k) \to dp(i+1,j+1,k+L_{i+1})$
+ 这个线段只和之前某一个区间相交，这里分成了两种情况
  + 这个线段完全在某个区间里面，$(k-j(L_{i+1}-1)) \cdot dp(i,j,k) \to dp(i+1,j,k)$
  + 这个线段露出了一点，考虑枚举露出了$x$，那么，$2j \cdot dp(i,j,k) \to dp(i+1,j,k+x)$
+ 这个线段把两个区间合并了，你需要枚举新增的未被覆盖的长度$x$，$(j-1)(L_{i+1}-x+1) \cdot dp(i,j,k) \to dp(i+1,j,k+x)$

最终答案就是$dp(N,1,X)$。

这样直接做的复杂度是$O(N^2X^2)$的，注意到在放$L_i$的时候，$j \le \frac{X}{L_i}$。因此对于$dp(i,\cdot,\cdot)$的状态数是$O(\frac{X^2}{L_i})$的，总得复杂度可以变为$O(NX^2)$。

然后可以注意到对于一个$(i,j,k)$你都是对$dp(i+1,j,\cdot)$或者$dp(i+1,j+1,\cdot)$的一段区间加上某个数，可以用前缀和优化。复杂度变为$O(N^2X)$。