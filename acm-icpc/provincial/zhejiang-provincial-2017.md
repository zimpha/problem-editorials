# The 14th Zhejiang Provincial Collegiate Programming Contest

+ [ ] [A. Cooking Competition](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370085)
- [ ] [B. Problem Preparation](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370086)
- [ ] [C. What Kind of Friends Are You?](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370087)
- [ ] [D. Let's Chat](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370088)
- [ ] [E. Seven Segment Display](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370089)
- [ ] [F. Heap Partition](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370090)
- [ ] [G. Yet Another Game of Stones](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370091)
- [ ] [H. Binary Tree Restoring](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370092)
- [ ] [I. Domino Tiling](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370093)
- [ ] [J. Card Game](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370094)
- [ ] [K. Final Defense Line](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370095)
- [ ] [L. Chiaki Sequence](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370096)
- [x] [M. Sequence to Sequence](https://zoj.pintia.cn/problem-sets/91827364500/problems/91827370097)

## L. Chiaki Sequence

## M. Sequence to Sequence

题意：有两个长度为$n$的序列$s_1,s_2,\dots,s_n$和$t_1,t_2,\dots,t_n$。有两种操作：

+ 选一个区间$[l,r]$，对于$i \in [l,r], s_i \ne 0$的$i$，把$s_i$减一。

+ 选一个区间$[l,r]$，对于$i \in [l,r], s_i \ne 0$的$i$，把$s_i$加一。

求从$s$变成$t$的最小操作次数。

$1 \le n \le 10^5, 0 \le s_i, t_i \le 10^9$

题解：首先可以证明一定可以先做减的操作，然后统一做加的操作。证明的话，你考虑两个相邻操作$(l_i,r_i,+1)$和$(l_{i+1},r_{i+1},-1)$，分析下区间$[l_i,r_i]$和区间$[l_{i+1},r_{i+1}]$的位置关系，都可以把减操作搞到加操作前面。

然后，如果第$i$个位置减的次数$d_i$知道了，我们显然是可以算出最少需要多少次减操作的：$D_i=D_{i-1}+\max(d_i-d_{i-1},0)$。同样，如果知道了第$i$个位置减的次数，那么这个位置之后要加的次数$a_i=t_i-s_i+d_i$，我们也可以算出最少需要多少次加操作：$A_i=A_{i-1}+\max(a_i-a_{i-1},0)$。

同时注意到，对于那些连续$t_i=0$的位置$s_i$，我们需要在这些位置上总共操作$\max(s_i)$次减操作。

综合上面三个，我们可以用动态规划来解决这个问题。令$prev_i$表示最大的$j < i$使得$t_j \ne 0$，$u_i=s_i-t_i$，$dp(i,d)$表示已经把$s[1..i]$变成了$t[1..i]$，在位置$i$上总共有$d$次减操作的最少操作次数，可以发现

$$
dp(i,d)=\min_{k}(dp(prev_i,d^\prime)+\max(0,d-d^\prime)+\max(-u_i+d-(-u_{prev_i}+d^\prime), 0) + \max(\max(s[prev_i+1..i-1])-\max(d,d^\prime), 0))
$$

这样就有了一个朴素的$O(n A^2)$的dp。之后可以发现，$dp(i,\cdot)$其实是由三段一次函数组成的，第一段是一个斜率为$0$的线段，第二段是一个斜率为$1$的线段，第三段是一个斜率为$2$的线段。并且每次转移可以做到$O(1)$，因此有一个$O(n)$的做法。

假设第一段的$y$值是$base_i$，接下来段与段之间交点的$x$坐标是$a_i$和$b_i$，那么可以分类讨论确定下一个$i$的这三个值。具体分析可以参考这篇[论文](https://drops.dagstuhl.de/opus/volltexte/2016/6078/pdf/LIPIcs-CPM-2016-16.pdf)。

别解：参考[这个](https://icpc.camp/new-meta/2017/04/29%20%e6%b5%99%e6%b1%9f%e7%9c%81%e8%b5%9b2017)。
