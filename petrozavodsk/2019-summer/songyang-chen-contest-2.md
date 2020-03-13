# Petrozavodsk Summer 2019. Songyang Chen Contest 2

+ [ ] [A. Salty Fish](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/A1/)
+ [ ] [B. Nonsense Time](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/B1/)
+ [ ] [C. Milk Candy](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/C1/)
+ [ ] [D. Radar Scanner](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/D1/)
+ [ ] [E. Snowy Smile](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/E1/)
+ [ ] [F. Faraway](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/F1/)
+ [x] [G. Support or Not](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/G1/)
+ [ ] [H. TDL](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/H1/)
+ [x] [I. Three Investigators](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/I1/)
+ [ ] [J. Road Manager](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/J1/)
+ [x] [K. Monster Hunter](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/K1/)
+ [x] [L. Game Prediction](https://official.contest.yandex.ru/ptz-summer-2019/contest/13458/problems/L1/)

## G. Support or Not

题意：给出空间中$n$个球，第$i$个在$(x_i,y_i,z_i)$，半径为$r_i$。定义两个球$i$和$j$的距离如下

$$
d(i,j)=\max(0, \sqrt{(x_i-x_j)^2+(y_i-y_j)^2+(z_i-z_j)^2}-r_i-r_j)
$$

给出$k$，输出前$k$小的距离。

$2 \le n \le 10^5, 1 \le k \le \min(100, \frac{n(n-1)}{2}), 0 \le x_i, y_i, z_i \le 10^6, 1 \le r_i \le 10^6$

题解：考虑二分答案$\lambda$，给每个半径都加上$\frac{\lambda}{2}$，转变成求是否存在至少$k$对$(i,j)$他们之间的距离是$0$。

假设全部球的半径都是$R$，那么建立以$2R \times 2R \times 2R$的立方体为单位建立坐标系统，考虑把球$i$放入$(\lfloor \frac{x_i}{2R} \rfloor, \lfloor \frac{y_i}{2R} \rfloor, \lfloor \frac{z_i}{2R} \rfloor)$对应的立方体里面。那么对于一个球$i$，只会和相邻的$3 \times 3 \times 3$的$27$个立方体里的球相交。然后显然，如果一个立方体里存在$O(\sqrt{k})$个球的话，我们一定能够找到$k$对相交的球。

但是现在球的半径不一样，那么先从最大的半径$mR$出发，只考虑$R_i \ge mR$的球。然后把$mR$减半，重复上面过程。这样结论也是成立的，并且只会做$O(\log mR)$次。

假设我们二分的结果是到$\lambda$，但是这时候求出来的$k$对球可能不是我们想要的答案。但是，第$k$个的距离肯定是$\lambda$。我们考虑把$\lambda$减$1$，再做上述过程。那么假设求出来的不足$k$对，不够的肯定都是$\lambda$。如果够的话，就直接输出这$k$对即可。

## I. Three Investigators

题意：给出一个长度为$n$的序列$a_1,a_2,\dots,a_n$，对于每个前缀，你需要选出最多$5$不相交的上升子序列，使得他们的权值和最大。

$1 \le n \le 10^5, 1 \le a_i \le 10^9$

题解：考虑权值都是$1$的话，就是个杨表题。每次插入一个数，然后求出前$5$行的长度之和。那么对于这个题的话，考虑把第$i$个数拆成$a_i$个$a_i$，每次操作把这$a_i$个数挨个插进去，之后再求前$5$行的长度之和的话就是我们这题的答案。

考虑到杨表里很多元素都是一样的，我们其实可以只维护每个数$x$出现次数$y$。然后你插入$a$和$b$的话，就是找到比$a$大的$b$个数，从当前杨表里删除，插到下一个杨表里面。可以发现每次插入一对$(a,b)$的话，最多只会使一对$(x,y)$分裂。因此均摊下来复杂度是$O(2^5 n \log n)$的。

## K. Monster Hunter

题意：有一棵$n$个点的有根树，$1$是根。除了根节点，每个节点$i$有个怪物，打这个怪兽需要消耗$a_i$的HP，之后会获得$b_i$的HP。必须把祖先节点上的怪物都打死后，才能打当前点的怪物。问最少需要多少HP才能打掉所有的怪物。

$2 \le n \le 10^5, 0 \le a_i, b_i \le 10^9$

题解：考虑没有任何限制的情况，我们肯定优先打$a_i < b_i$的，然后是$a_i = b_i$的，最后是$a_i > b_i$的，其他情况：

+ 对于所有$a_i < b_i$的怪物，那么肯定先打$a_i$比较小的；

+ 对于所有$a_i=b_i$的怪物，谁先打无所谓，不如也先打$a_i$比较小的；

+ 对于所有$a_i > b_i$的怪物，我们肯定要先打$b_i$比较大的。

那么假设按照上述规则，我们排出了一个打怪顺序$p_1,p_2,\dots,p_n$，考虑$p_1$：

+ $p_1$的父亲已经被打死了，那么我们直接打这个怪物即可。

+ $p_1$的父亲还没有死，那么如果我们打死了$p_1$的父亲后，我们肯定要先来打$p_1$，于是可以考虑把这两只怪合并。

上述两种情况下，我们都把问题从$n$的规模缩小到了$n-1$。因此需要拿一个优先队列来维护最先应该被打的怪即可。

接下来考虑如何合并两个怪$(a_1,b_1)$和$(a_2,b_2)$，成为$(a_3,b_3)$。显然有$a_3 \ge a_1$，因为我们要先打死第一个。这个时候我们的HP为$a_3-a_1+b_1 \ge a_2$，得到$a_3 \ge a_2+a_1-b_1$。于是$a_3=\max(a_1,a_2+a_1-b_1)$，那么$b_3=a_3+b_1+b_2-a_1-a_2$。

## L. Game Prediction

题意：有$n$个数$a_1,a_2,\dots,a_n$。有$q$个询问，每次给出一个区间$[l_i,r_i]$，要求用$a[l_i..r_i]$这些数玩如下博弈：每次可以从左端或者有端拿走一个数，每个人目的是最大化自己拿走数的和。求最优操作下，先手和后手数的和多大。

$1 \le n \le 10^5, 1 \le q \le 2 \times 10^5, 1 \le a_i \le 10^9, 1 \le l_i \le r_i \le n$

题解：参考这篇论文[An Optimal Algorithm for Calculating the Profit in the Coins in a Row Game](https://www.mimuw.edu.pl/~idziaszek/termity)的结论，加上数据随机，我们可以把问题规模缩成$O(\log n)$的。直接线段树暴力维护即可。

别解：参考这个[回答](https://forum.icpc.camp/d/30-petrozavodsk-summer-2019-day-1-l-game-prediction)

> First of all, I would like to recall the central property of the game: We can replace three consecutive elements $a_{i - 1}$, $a_i$ and $a_{i + 1}$ with $(a_{i - 1} - a_{i} + a_{i + 1})$ without changing the value of the game, if $a_{i - 1} \leq a_i \geq a_{i + 1}$ holds. Repeating the replacement, we ultimately end up with a sequence $b$ such that $b_1 > \dots > b_i < \dots < b_n$ for some $i$, which is called the *reduced sequence* as follows.  Let the sorted version of the sequence $b$ is $b'$. The value of the game is essentially $b^\prime_1 - b^\prime_2 + b^\prime_3 - \dots$.
> 
> Now back to the $O((n + q) \sqrt{n} \log n)$ algorithm. Partition the sequence into $\frac{n}{b}$ consecutive blocks of size $b$. We first compute the reduced sequence of the range $[i \cdot b, j]$ by adding elements to the right. This is can be done in $O(\frac{n^2}{b})$.
> 
> To answer a query, we start from a precomputed reduced sequence, and add $O(b)$ elements to its left. This should be done with the help of a binary search, leading to $O(b \log n)$ time overall. The other difficulty is how to calculate the value of the game. I will elaborate the idea in the following paragraphs.
> 
> Consider how to add an element $x_1$ to the left of the reduced sequence $b_1 > \dots > b_i < \dots < b_n$. First, if $x_1 > b_1$, nothing should be done except for adding the element $x_1$ directly to the left. If $x_1 \leq b_1$, the sequence will be reduced further by replacing $b_1$, $b_2$ with $x_3 = x_1 - b_1 + b_2$. And the so on process is repeated on $x_2, b_3, b_4, \dots, b_i$. We can see that $x_j$ is of form $x\_1 - b_1 + b_2 + \dots - b_{2j - 1} + b_{2j}$ and $x_j$ is compared with $b_{2j + 1}$. The check turns out to be $(x_1 - b_1) + (b_2 - b_3) + \dots + (b_{2j} - b_{2j + 1}) > 0$. As $b_{2k} > b_{2k + 1}$ always holds, we can do binary search to find the point where we have to stop. 
> 
> Now we turn to the most involved part. For a reduced sequence $b_1 > \dots > b_i < \dots < b\_n$, we need to know the value of the game with the removal of a prefix. We further divide the reduced sequence into two chains: the downward chain $b_1, b_2, \dots, b_i$ and the upward chain $b_i, \dots, b_n$. For the downward chain, we build a binary search tree of intervals $[b_{j + 1}, b_j)$, and for each intervals we store the count of elements in the upward chain lying in its interval. By doing so, we can compute the game value with a part of downward chain $b_j, \dots, b_i$ and the upward chain $b_i, \dots, b_n$. We can see that during the computation of the game value, the upward chain is naturally divided into two parts: the part in $[b_i, b_j]$ and the part in $(b_j, \infty)$. The former part can be queried on the search tree, while the later part can be easily computed by binary search on the upward chain.
> 
> To conclude, setting $b = O(\sqrt{n})$ yields to $O((n + q) \sqrt{n} \log n)$.
