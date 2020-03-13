# XIX Open Cup. Grand Prix of Moscow

+ [ ] [A. Anatoly Shalyto](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/A/)
+ [ ] [B. Basirovich Maxim](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/B/)
+ [ ] [C. CTAHKEB** ANDREW](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/C/)
+ [ ] [D. Dr. Bill Poucher](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/D/)
+ [ ] [E. Elena Andreeva](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/E/)
+ [ ] [F. Filipp Rukhovich](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/F/)
+ [ ] [G. Gleb Evstropov](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/G/)
+ [ ] [H. Hristenko Oleg](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/H/)
+ [x] [I. Ivan Smirnov](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/I/)
+ [ ] [J. Juke Artem](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/J/)
+ [ ] [K. Kunyavskiy Pavel](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/K/)
+ [ ] [L. Lidia Perovskaya](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/L/)
+ [ ] [M. Mikhail Tikhomirov](https://official.contest.yandex.ru/opencupXIX/contest/12353/problems/M/)

## B. Basirovich Maxim

题意：给出一个长度为$n$的序列$a_0,a_1,\dots,a_{n-1}$，以及每个数属于哪个集合$b_0,b_1,\dots,b_{n-1}$，总共有$k$个集合。你需要选择一个非递增序列$c_0,c_1,\dots,c_{n-1}$，令$d_p=\sum_{i \in S_p} c_i a_i$，使得$\frac{\min(d_1,d_2,\dots,d_{k-1}}{d_0}$最大。

$2 \le n \le 10^5, 2 \le k \le 4, 0 \le b_i < k, b_0=0$

题解：令$f_i=c_i-c_{i+1}$，$g_{i,p}=\sum_{j \le i, j \in S_p} a_i$，那么$d_p=\sum_{i=0}^{n-1}f_i g_{i,p}$。考虑这个$n$个$4$维点$(g_{i,0},g_{i,1},g_{i,2},g_{i，3})$，如果$\sum f_i = 1$，那么$(d_0,d_1,d_2,d_3)$是这$n$个点的一个convex combination，也就是在这$n$个点构成的凸包内。

现在我们二分答案$\lambda$，把每个坐标$x_i$减去$\lambda \cdot x_0$。变成求这$n$个三维点是否存在一个convex combination每一维坐标都大于等于$0$。一个做法是求出这个$n$个点的三维凸包，然后随便判一判。另一个做法是做一次对偶，变成判定$n$个半空间的交是否有界。这个只需要枚举哪一维无界，带入一个较大的值，转成半平面交问题即可。有个随机的[线性判定半平面交做法](https://petr-mitrichev.blogspot.com/2016/07/a-half-plane-week.html)。

## I. Ivan Smirnov

题意：给出一个括号序列$s$的`RLE`形式，长度为$n$。有$q$个询问，每次是另一个括号序列$t$的`RLE`形式，长度为$m$。问$s$和$t$能否merge成一个合法括号序列。

$1 \le n, q \sum m_i \le 3 \times 10^5, 1 \le a_i \le 10^{12}$

题解：对于一个括号序列，如果把`(`看成$1$，`)`看成$-1$，令$a_i$是长度为$i$的前缀的和。令$x_i=\max_{0 \le j \le i}(a_i)$，$y_i=\min_{0 \le j \le i}(a_i)$。即前缀和的最大值和最小值。对于两个括号序列，如果存在一个第一个序列的$i$和第二个序列的$j$，满足$x_i+y_j < 0$并且$x_j+y_i <0$，那么肯定是不能成功合并的。

把`(`看成$-1$，`)`看成$1$，从后往前求个后缀和的最大值和最小值$x^\prime_i$和$y^\prime_i$，类似上面的：如果存在一个第一个序列的$i$和第二个序列的$j$，满足$x^\prime_i+y^\prime_j < 0$并且$x^\prime_j+y^\prime_i <0$，那么肯定是不能成功合并的。

另外，如果总和不是$0$的话，也是不能合并的。