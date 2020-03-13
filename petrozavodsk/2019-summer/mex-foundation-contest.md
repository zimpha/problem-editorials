# Petrozavodsk Summer 2019. MEX Foundation Contest

- [ ] [A. The One Polynomial Man](https://codeforces.com/gym/102412/submit/A)
- [ ] [B. Alexey the Sage of The Six Paths](https://codeforces.com/gym/102412/submit/B)
- [ ] [C. Steel Ball Run](https://codeforces.com/gym/102412/submit/C)
- [x] [D. The Jump from Height of Self-importance to Height of IQ Level](https://codeforces.com/gym/102412/submit/D)
- [ ] [E. Minimums on the Edges](https://codeforces.com/gym/102412/submit/E)
- [ ] [F. IQ Test](https://codeforces.com/gym/102412/submit/F)
- [ ] [G. AtCoder Quality Problem](https://codeforces.com/gym/102412/submit/G)
- [ ] [H. Mex on DAG](https://codeforces.com/gym/102412/submit/H)
- [ ] [I. Find the Vertex](https://codeforces.com/gym/102412/submit/I)
- [ ] [J. Yet Another Mex Problem](https://codeforces.com/gym/102412/submit/J)

## D. The Jump from Height of Self-importance to Height of IQ Level

题意：有一个长度为$n$的排列$h_1,h_2,\dots,h_n$。有$q$个操作，给出$3$个整数$l_i$，$r_i$和$k_i$，每次把区间$[l_i,r_i]$循环右移$k_i$次。每次操作完，求出是否存在三个数$i < j < k$，使得$h_i < h_j < h_k$。

$1 \le n, q \le 120000, 1 \le h_i \le n, 1 \le l_i \le r_i \le n, 0 \le k_i \le r_i-l_i+1$

题解：考虑用平衡树维护这个序列，然后每个节点维护以下信息：

+ 区间的最小值$mi$，区间的最大值$mx$，区间的大小$size$

+ $mi^\prime$表示最小的$p_y$，使得存在一个$x$，满足$x < y$且$p_x < p_y$

+ $mx^\prime$表示最大的$p_x$，使得存在一个$y$，满足$x < y$且$p_x < p_y$。

+ 以及$yes$表示区间里是否存在一组合法的解

那么在合并两个节点$left$和$right$的时候$mi$，$mx$和$size$都很容易维护，考虑如何维护$mi^\prime$，$mx^\prime$以及$yes$

+ 如果$left.yes$或者$right.yes$其中一个是`true`，那么我们可以return了。

+ 否则先用$left.mi^\prime,left.mx^\prime$和$right.mi^\prime,right.mx^\prime$更新一下当前节点的$mi^\prime$和$mx^\prime$。同时我们也可以这一步知道是否存在一个合法的解。

+ 然后考虑$x \in left$，$y \in right$怎么做，不妨先求$mi^\prime$。观察可以发现在$right$里面，大于$left.mi$的数一定形成了一个递减序列，否则前两个情况就满足了。于是我们可以二分出大于$left.mi$的最小值，用来更新$mi^\prime$。然后$mx^\prime$也是类似，在$left$里，小于$right.mx$的数也形成了一个递减序列，我们同样可以二分找到小于$right.mx$的最大数。

复杂度$O(n \log^2 n)$。
