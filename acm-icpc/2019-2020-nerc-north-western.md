# 2019-2020 ICPC, NERC, North-Western Russia Regional Contest

+ [ ] [A. Accurate Movement](https://contest.yandex.ru/QF2019/contest/15017/problems/A/)
+ [ ] [B. Bad Treap](https://contest.yandex.ru/QF2019/contest/15017/problems/B/)
+ [ ] [C. Cross-Stitch](https://contest.yandex.ru/QF2019/contest/15017/problems/C/)
+ [x] [D. Double Palindrome](https://contest.yandex.ru/QF2019/contest/15017/problems/D/)
+ [ ] [E. Equidistant](https://contest.yandex.ru/QF2019/contest/15017/problems/E/)
+ [x] [F. Foreach](https://contest.yandex.ru/QF2019/contest/15017/problems/F/)
+ [ ] [G. Golf Time](https://contest.yandex.ru/QF2019/contest/15017/problems/G/)
+ [ ] [H. High Load Database](https://contest.yandex.ru/QF2019/contest/15017/problems/H/)
+ [ ] [I. Ideal Pyramid](https://contest.yandex.ru/QF2019/contest/15017/problems/I/)
+ [ ] [J. Just the Last Digit](https://contest.yandex.ru/QF2019/contest/15017/problems/J/)
+ [ ] [K. King’s Children](https://contest.yandex.ru/QF2019/contest/15017/problems/K/)
+ [ ] [L. Lengths and Periods](https://contest.yandex.ru/QF2019/contest/15017/problems/L/)
+ [ ] [M. Managing Difficulties](https://contest.yandex.ru/QF2019/contest/15017/problems/M/)

## A. Accurate Movement

## B. Bad Treap

## C. Cross-Stitch

## D. Double Palindrome

题意：给出$n$和$k$，求出有多少长度不超过$n$的字符集为$k$的字符串，可以分解成两个回文串相接。

$1 \le n \le 10^5, 1 \le k \le 26$

题解：对于一个字符串$s$，如果它是两个非空回文串$u$和$v$相接得到的，那么对于每个$i$，有$s_i=s_{|u|-1-i \bmod |s|}$。然后如果$s$有另外一个双回文划分$x$和$y$，也有$s_i=s_{|x|-1-i \mod |s|}$。不妨假设$|x| < |u|$，我们可以得到$s_i=s_{|x|-1-i \mod |s|}=s_{|u|-|x|+i \mod |s|}$，也就是说$|u| - |x|$是$s$的一个周期。然后根据`weak periodicity lemma`，$\gcd(|s|, |u|-|x|)$也是$s$的一个周期，因此$s$可以表示成$p^k$ ($k \ge 2$)。

如果$p$是$s$的最小周期，那么存在非空回文串$u_1,u_2,\dots,u_{k}$和$v_1,v_2,\dots,v_k$，使得$s=u_1v_1=u_2v_2=\dots=u_kv_k$，并且$p$恰好存在一个双回文划分。证明如下：

由于$p$不是power，那么根据上面的结论$p$最多存在一个双回文划分。令$s=uv$，$u$和$v$是非空的回文串，那么有$\max(|u|, |v|) \ge |p|$。如果$|u| \ge p$，那么$p[0, |u| \bmod |p| - 1]=u^R[0, |u| \bmod |p| - 1]=(p[0,|u| \bmod |p| - 1])^R$，也就是说$p[0, |u| \bmod |p| - 1]$是回文串，同样和以得到$p[|u| \bmod p, |p| - 1]$是回文串。当$|v| \ge p$的时候也可以得到类似的结论。

令$f(n)$表示长度为$n$的，恰好存在一个双回文划分的字符串。$g(n)$为所有串的双回文划分方案之和，那么有$g(n) = \sum_{d|n} \frac{n}{d} f(d)=\sum_{i=0}^{n} k^{\lceil \frac{i}{2} \rceil} \cdot k^{\lceil \frac{n-i}{2} \rceil}$。

最后答案就是$\sum_{i=1}^{n}\sum_{d|i}f(d)$。

## E. Equidistant

## F. Foreach

题意：给出两个长度为$n$的数组$s$和$t$。你有两种操作：

+ 选择一个在$s$中存在的数$x$，找一个最早的$i$，使得$s_i=x$，然后把$s_i$变成另一个在$s$中存在的数$y$。
+ 把$s_n$变成另一个在$s$中存在的数$y$。

给出一个长度不超过$10^4$的操作序列，把$s$变成$t$。

$1 \le n \le 50, 1 \le s_i, t_i \le 100$

题解：可以先考虑一些trivial的情况：

1. $s$和$t$一开始就是一样的，不需要任何操作
2. $t$中有一个数$x$没有在$s$中出现，这样是无解的。
3. $t$中恰好有$n$个不同的数，且$s \ne t$，这样也是无解的。因为我们在把$s$的一个数变成另一个数的时候，$s$里面本质不同的数最多只有$n-1$个。

除了上面讨论的几种情况，其他都是有解的，下面给出构造方法。首先，如果$s$中有一些数$x$不在$t$中出现，显然这些位置可以直接修改。然后我们可以假设$s$和$t$出现数的集合是一样的了。其次，最后一个数比较特殊，大部分情况下可以先拿来当寄存器用。于是可以考虑从倒数第二个数开始从后往前依次操作每个数。

假设当前操作到第$i$个数，如果$s_i=t_i$可以直接跳过，否则我们先需要把$s[1,i-1]$里面出现的$s_i$都改成其他数（任选一个不等于$s_i$的即可），因为只有当$s_i$成为第一个出现的数的时候我们才能改。接下来分几种情况：

1. $s_i=x$在$s[i+1,n]$中出现过，那么可以直接把$s_i$修改成$t_i$，因为如果之后有需要用到$s_i$的话，我们都可以用另一个数代替。
2. $s_i=x$在$s[i+1,n]$中没有出现过，也就是说$x$在整个数组里面只出现过一次。那么必然存在一个$y$，在数组里面至少出现了两次，我们考虑这两个$y$和$x$的相对位置来进行操作，假设最后一个数是$z$：
   + `yyxz`和`yxyz`和`yxy`：我们都可以通过把第一个$y$变成$z$(第三种$z=y$)，先变成$y$，然后把最后一个数变成$x$，最后再把$x$变成目标数。
   + `xyy`：先把最后一个数变成$x$，然后把$x$修改成目标数即可
   + `xyyz`：这个比较复杂，因为我们不能通过一个比较完美的操作来达成目的。我的做法是先把第一个$y$变成$x$，然后把$x$变成目标数。这个时候$x$在整个数组中还是只出现一次(变成`txyz`了)，我们可以等到$x$没有其他用处的时候，再把这个$x$变成$y$。这里还有一个特殊情况，就是$i=0$的时候，这个只需要特判构造下即可。

当上面处理完之后，我们在考虑$s_n$，显然直接变成$t_n$就好了。

## G. Golf Time

## H. High Load Database

## I. Ideal Pyramid

## J. Just the Last Digit

## K. King’s Children

## L. Lengths and Periods

## M. Managing Difficulties
