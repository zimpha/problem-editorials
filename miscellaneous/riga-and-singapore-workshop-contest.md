# Riga and Singapore Workshop Contest by 300iq

+ [ ] [A. Zero Sum](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/A)
+ [ ] [B. MST](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/B)
- [ ] [C. Tree Circles](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/C)
- [ ] [D. Angle Beats 2.0](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/D)
- [x] [E. LIS](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/E)
- [ ] [F. Good Coloring](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/F)
- [ ] [G. Circle Convertation](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/G)
- [ ] [H. Equal MEX](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/H)
- [ ] [I. Cactus is Money](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/I)
- [x] [J. Good Permutations](https://codeforces.com/group/6jlYbsz6PW/contest/252619/problem/J)

## E. LIS

题意：给出$4$个序列$a_1, a_2, \ldots, a_n$;  $b_1, b_2, \ldots, b_n$;  $x_1, x_2, \ldots, x_n$;  $y_1, y_2, \ldots, y_n$。

构建一个有向图：如果$i < j$并且$a_i \cdot x_j + b_i \geq y_j$，那么从$i$连一条边到$j$。求出这个有向图的最长路。

$1 \le n \le 150000, 0 \leq a_i, x_i \leq 300000, 0 \leq b_i, y_i \leq 10^{11}$

题解：令$dp_i$表示以$i$为结尾的最长路，考虑用一棵线段树维护凸壳。线段树节点$[l,r]$维护了满足$l \le dp_i \le r$的所有直线$y=a_i \cdot x + b_i$。

那么对于一个$(x_j,y_j)$，我们在线段树上二分出最大的满足条件的$dp_i$。显然用动态凸壳的模板就可以搞定了。复杂度$O(n \log^2 n)$。

## J. Good Permutations

题意：定义一个长度为$n$的排列$p$是好的，当且仅当恰好有$m$对$(i,j,k)$满足$1 \le i < j < k \le n$并且$p_i < p_j < p_k$。对于所有好的排列，求出所有的逆序对个数之和，对$998244353$取模。

$1 \le n \le 10^5, 0 \le m \le 3$

题解：注意到$(123)$-avoiding排列的个数是`Catalan number`，因此可以猜测这个数列在固定$m$的情况下也是[P-recursive](https://en.wikipedia.org/wiki/P-recursive_equation)的。

也就是说令$a(n)$是第$n$项的值，那么存在一个$k$和$k$个多项式$P_1(x), P_2(x), \dots, P_k(x)$，使得$a(n)=\sum_{i=1}^{k} P_i(n)\cdot a_{n-i}$。

假设我们找到了$a(n)$的前若干项，之后再用Min-25这篇[Find Linear Recurrence with Polynomial Coefficients](https://min-25.hatenablog.com/entry/2018/05/10/212805)的做法，找到$k$和$P_i(x)$，这个题就做完了。

令$f(n,j_1,j_2,j_3,j_4,m)$表示满足下面条件的恰好有$n$个元素的排列个数：

+ 满足$i < j$且$p_i < p_j$最早的$4$个$j$的位置分别是$j_1,j_2,j_3,j_4$，

+ 恰好有$m$对满足$i < j < k$且$p_i < p_j < p_k$的三元组

$g(n,j_1,j_2,j_3,j_4,m)$则是满足上面条件的所有排列的逆序对个数之和。

考虑$n$变成$n+1$的时候，你会把$n+1$插到哪些位置，同时你也可以快速维护出新的$j^\prime_1,j^\prime_2,j^\prime_3,j^\prime_4$和$m^\prime$。然后你有了一个$O(n^6)$的dp，本地跑跑可以跑到$n=50$。