# December Challenge 2019

+ [x] [Plus Multiply](https://www.codechef.com/DEC19A/problems/PLMU)
+ [x] [Easy Subsequence Selection](https://www.codechef.com/DEC19A/problems/SUBSPLAY)
+ [x] [That Is My Score!](https://www.codechef.com/DEC19A/problems/WATSCORE)
+ [x] [Binary XOR](https://www.codechef.com/DEC19A/problems/BINXOR)
+ [x] [Chefina and Ranges](https://www.codechef.com/DEC19A/problems/CHFRAN)
+ [x] [Addition](https://www.codechef.com/DEC19A/problems/BINADD)
+ [x] [Sticky Notes](https://www.codechef.com/DEC19A/problems/STICNOT)
+ [x] [Binomial Fever](https://www.codechef.com/DEC19A/problems/BINOFEV)
+ [ ] [Test Generation](https://www.codechef.com/DEC19A/problems/TESTGEN)
+ [x] [Scoring Pairs](https://www.codechef.com/DEC19A/problems/APAIRS)

## Plus Multiply (PLMU)

题意：略

题解：略

## Easy Subsequence Selection (SUBSPLAY)

题意：给出一个字符串$s$，找出一个最大的$k$，使得存在两个相同的子序列$a$和$b$，他们下标集合的公共元素不超过$k-1$。

$1 \le |s| \le 10^5$

题解：只有一个位置不同时是最好的。也就是枚举相邻的相同字符，剩下的都可以作为子串的一部分。

## That Is My Score! (WATSCORE)

题意：略

题解：略

## Binary XOR (BINXOR)

题意：给出两个长度为$N$的二进制数$A$和$B$，你可以随便重排$A$或者$B$。求出$A \text{ XOR } B$有多少种可能的结果，对$10^9+7$取模。

$1 \le N \le 10^5$

题解：最后结果中只有`0`和`1`的个数有意义，那么仅需要求出$x$个`1`和$N-x$和`0`能够达到即可。

`1`只有可能是`0`和`1`的异或，令$u$个`1`来自$A0$异或$B1$，$v$个个`1`来自$A1$异或$B0$。那么可以列出方程$u+v=x,u-v=A0-B0$。解出来判定合法即可。

## Chefina and Ranges (CHFRAN)

题意：给出$N$个区间$[l_1,r_1],[l_2,r_2],\dots,[l_N,r_N]$，你需要删掉最少的区间，使得能够把这些区间分成两个集合。如果两个区间有交，则他们在同一个集合里面。

$1 \le N \le 10^5, 1 \le l_i \le r_i \le 10^9$

## Addition (BINADD)

题意：对于两个二进制串$A$和$B$，用下面算法实现加法，求循环执行次数：

```
function add(A, B):
    while B is greater than 0:
        U = A XOR B
        V = A AND B
        A = U
        B = V * 2
    return A
```

$1 \le |A|, |B| \le 10^5$

题解：考虑每次$A \text{ AND } B$，实际上是把所有的进位拿出来。然后$A+B$最多产生$|A|+|B|$次进位。因此只需要暴力维护$A$和$B$里面当前有哪些位置是$1$即可，然后暴力模拟这个函数。

## Sticky Notes (STICNOT)

题意：给出一棵$N$个点的树，第$i$点上有个权值$a_i$，第$i$条边上有个权值$b_i$。你可以把$a$和$b$重排，然后修改若干个$a_i$，使得最后对于每个点$v$与和它相邻的边$e$，都有$a_v \ge b_e$。求最小修改次数。

$2 \le N \le 10^5, 1 \le a_i, b_i \le 10^9$

题解：先二分修改次数，肯定是修改最小的$x$个$a$。之后考虑从叶子开始，一层一层把值填上，先填$a$，然后再把$b$填在父亲这条边上。最后能填完就是可行的。

## Binomial Fever (BINOFEV)

题意：给出$N,p,r$，求$S=\sum\limits_{i=0}^{N} \binom{p^i}{r}$，对$998244353$取模。

$1 \le N \le 10^9, 1 \le p < 998244353, 1 \le r \le 10^6$

题意：把$\binom{x}{r}$展开就是$\frac{x(x-1)\dots (x-r+1)}{r!}$，显然$\frac{1}{r!}$可以提取出来，上面是一个$r$次的多项式。不妨先用FFT求出这个多项式记为$f(x)=\sum_{i=1}^{r}a_ix^i$，那么求和式子变成

$$
\frac{1}{r!}\sum_{i=0}^{N}\sum_{j=1}^{r}a_j (p^i)^j=\frac{1}{r!}\sum_{j=1}^{r}a_j(\sum_{i=0}^{N}(p^j)^i)
$$

对于每个$j$，里面每项都是等比数列求和。

现在考虑如何求$f(x)$，令$F_n(x)=\prod_{i=0}^{n-1}(x-i)$，那么显然有$F_{2n}(x)=F_n(x)F_n(x-n)$。

假设$F_n(x)=\sum_{i=0}^{n}a_ix^i$，那么

$$
\begin{aligned}
F_n(x-n)&=\sum_{i=0}^{n-1}a_i (x-n)^i\\
&=\sum_{i=0}^{n-1}a_i\sum_{j=0}^i{i\choose j}(-n)^{i-j}x^j\\
&=\sum_{i=0}^{n-1}(\sum_{j=i}^n {j\choose i}(-n)^{j-i}a_j)x^i
\end{aligned}
$$

括号内的部分拆开之后，可以分成差相等的两个部分，意味着可以翻转之后卷积。

这样就可以$O(n \log n)$求出$F_n(x)$了。

## Scoring Pairs (APAIRS)

题意：定义对于两个长度为$D$的十进制串$X$和$Y$(短的用`0`补齐)，$score(X, Y)$为：将$Y$位数重排后，$\sum |X_i-Y_i|$的最小值。

给出$L$和$R$，求出$\sum_{i=L}^{R} \sum_{j=L}^{R} score(i,j)$，对$10^9+7$取模。

$1 \le L \le R \le 10^{18}$

题解：首先不妨把$X$和$Y$都补全到$19$位，然后对于一对$X$和$Y$，只要把所有数字排序，然后对应的减一减就是最优的。那么其实就可以每一位单独考虑，令$f(i,d)$表示排序后第$i$为是$d$的数的个数。答案就是

$$
\sum_{i=0}^{18} \sum_{x=0}^{9} \sum_{y=0}^{9} f(i,x) \cdot f(i, y)
$$

计算$f(i,d)$就比较简单了。枚举$d$，然后做数位dp。令$dp(i,a,b,el,er)$表示处理了前$i$位，比$d$大的数填了$a$个，比$d$小的填了$b$个，和$L$的大小关系是$el$，和$R$的大小关系是$er$的数的个数。转移很简单。

## Test Generation (TESTGEN)

题意：造一组数据卡掉[CNNCT2](https://www.codechef.com/OCT19A/problems/CNNCT2)的$4$个错误做法，用不能超过$100$条边。

## (Challenge) Cubical Virus (CUBVIRUS)
