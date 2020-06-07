# XX Open Cup. Stage 16. Grand Prix of Moscow

+ [ ] [A. Alice and Bob](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/A/)
+ [ ] [B. Brackets](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/B/)
+ [x] [C. Circles](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/C/)
+ [ ] [D. Deja Vu](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/D/)
+ [ ] [E. Easiest Sum](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/E/)
+ [ ] [F. Funny Salesman](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/F/)
+ [ ] [G. Graph Coloring](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/G/)
+ [ ] [H. Hidden Graph](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/H/)
+ [ ] [I. Insects](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/I/)
+ [ ] [J. Joining Points](https://official.contest.yandex.ru/opencupXX/contest/18195/problems/J/)

## C. Circles

题意：考虑$n$个数$s_1,s_2,\dots,s_n$，定义$f(s_1,s_2,\dots,s_n)$为最大的$x_1+x_2+\dots+x_n$使得$x_i+x_{i+1} \le s_i$并且$x_i \ge 0$。

给出$n$个整数$a_1,a_2,\dots,a_n$，求出$f(a_1,a_2,a_3), f(a_1,a_2,a_3,a_4), \dots, f(a_1,a_2,\dots,a_n)$。

题解：把原问题看成一个线性规划：$x_i+x_{i+1} \le s_i, x_i \ge 0, \max\{x_1+x_2+\dots+x_n\}$。

对偶一下得到，$y_i+y_{i+1} \ge 1, \min\{y_1 \cdot s_1 + y_2 \cdot s_2 + \dots + y_n \cdot s_n\}$。

可以发现最优值中$y_i \in \{0, 1, 2\}$，这是因为最优点一定在这$n$个半空间交的顶点上取到，显然在顶点上都有$y_i \in \{0, 1, 2\}$。

于是我们就可以直接dp了，令$dp(i,j,k)$表示前$i$个数，$y_1=j,y_i=k$的最优值。转移很简单，保证$y_{i+1} + y_i \ge 1$即可。

## D. Deja Vu

题意：给出$n$个数$x_1,x_2,\dots,x_n$，有$q$个操作：

+ 给出$i$和$y$，令$x_i=y$
+ 给出$l$，找出最小的$d$，使得存在$(a,b,c)$满足$l \le a < b < c < d$并且$x_a < x_b < x_c < x_d$。

$1 \le n, q \le 500000, 1 \le x_i \le 10^9, 1 \le i \le n, 1 \le y \le 10^9, 1 \le l \le n$

题解：假设没有修改操作，我们用离线来回答所有询问。

类似$O(n \log n)$求LIS的经典做法，对于每个位置$i$，我们维护三个数$a_i,b_i,c_i$，分别表示$i$到当前位置这些数中，长度为$1,2,3$的上升序列中结尾的最小值。

那么当加入当前位置的数$x$的时候，对于每个$i$会做如下的操作：

+ 如果$x \le a_i$，那么$a_i=x$
+ 否则，如果$x \le b_i$，那么$b_i=x$
+ 否则，如果$x \le c_i$，那么$c_i=x$
+ 否则，我们得到了一个合法的四元组。当前位置就是$l=i$的询问的答案。

可以发现，只考虑对$a_i$的更新的话，就是标准的`Segment Tree Beats`，但其实这些操作都可以用`Segment Tree Beats`的方式来维护。

在线段树的节点上维护$a.mx,a.smx$，分别表示$a$的最大值，次大值。

考虑当前节点，对于$a$的操作

1. 如果$x > a.mx$我们就需要用$x$来更新$b$和$c$了，$a$没有任何变化
2. 如果$a.smx < x \le a.mx$，令$a.mx = x$，但是对于$a.smx$我们需要更新$b$和$c$
3. 否则，递归进入左右子树应用上面的操作即可

为了能够更新$b$，我们需要维护$mx=(b.mx, b.smx)$和$smx=(b.mx,b.smx)$分别表示所有$a.mx$对应的$b$的最大值和$b$的次大值，所有非$a.mx$对应的$b$的最大值和$b$的次大值。

于是对于上述第一种情况，我们需要更新$mx=(b.mx, b.smx)$和$smx=(b.mx, b.smx)$；对于第二种情况，仅需要更新$smx=(b.mx, b.smx)$。

类似的，更新$b.mx$和$b.smx$的时候，也会分成三种情况。于是进一步的，我们其实需要分别维护$c.mx,c.smx$。实现起来比较繁琐，细节也很多，但基本上还是能够work的。

接下来考虑有修改操作。我们其实可以把每个询问按照时间顺序用线段树维护，每个操作则按照$i$的值分类，同时记录时间。

那么我们依次枚举每个下标$i$的时候，可以把$l=i$的那些询问在线段树上加上。然后把相应的修改操作都在线段树上做修改。修改完之后，把已经成功找到答案的询问操作从线段树上删掉即可。

类似的均摊分析可以得到复杂度是$O((n+q) \log n)$的。