# Volume 11

## 501. Eight Divisors
令$\pi(n)$表示小于等于$n$的素数个数, 那么$$f(n) = \pi\left(\sqrt[7]n\right) + \sum_{p \le \sqrt[3]n}\left(\pi\left(\frac{N}{p^3}\right)\right) - \pi(\sqrt[4]N) + \sum_{p < \sqrt[3]n} \sum_{p < q < \sqrt{N/p}} \left(\pi\left(\frac{N}{pq}\right) - \pi(q)\right)$$

计算$\pi(n)$可以参考[Prime-counting function](https://en.wikipedia.org/wiki/Prime-counting_function).

## 502. Counting Castles

## 503. Compromise or persist

## 504. Square on the Inside
根据pick定理, 暴力枚举$a,b,c,d$之后可以方便算出内部格点数目, 然后统计下就好了.

## 505. Bidirectional Recurrence

## 506. Clock sequence

## 507. Shortest Lattice Vector

## 508. Integers in base $i-1$

## 509. Divisor Nim
打表下就可以发现$sg_i$等于$i$在二进制下末尾$0$的个数, 枚举$x$, 那么很容易计算出$i$满足$sg_i=x$. 然后答案就是$\sum\limits_{i \oplus j \oplus k \ne 0}cnt_i \times cnt_j \times cnt_k$.

## 510. Tangent Circles
根据[Descartes' theorem](https://en.wikipedia.org/wiki/Descartes%27_theorem)可以很容易算出$r_C$的值. 然后稍微化简下可以知道$r_A = v^2g, r_B = u^2g, r_C = u^2v^2g/(u+v)^2, \gcd(u,v)=1$. 枚举$u,v$就好了.

## 511. Sequences with nice divisibility properties
显然$a_i$是$n$的约数, 考虑$f(i,j)$表示$n+a_1+a_2+...+a_i$对$k$取模是$j$的方案数, 转移方程很显然, 然后利用$O(k^2\log n)$的线性递推做就好了.

## 512. Sums of totients of powers
显然$\varphi(n^i) = \varphi(n)n^{i-1}$, 于是$\sum\limits_{i=1}^{n}{\varphi(n^i)}\equiv\varphi(n)\sum\limits_{i=0}^{n-1}{n^i}\equiv\varphi(n)\sum\limits_{i=0}^{n-1}{(-1)^i}\equiv\varphi(n)(n\ \text{mod}\ 2)$. 令$\varphi(n)=\sum\limits_{i=1}^{n}{\varphi(i)}$, 那么就有$g(n) = \varphi(n) - \sum\limits_{q=1}^{\left\lfloor{}log_2(n)\right\rfloor}{2^{q-1}g\left(\left\lfloor\frac{n}{2^q}\right\rfloor\right)}$, 直接递归计算就好了.

## 513. Integral median
可以知道这个公式$4m_c^2=2(a^2+b^2)-c^2$, 令$a=u-v,b=u+v,c=2C$, 得到$u^2+v^2=m_c^2+C^2$, 也就是求$u^2+c^2=d^2+c^2$, 限制条件有$$u + v \le 2c \le n, \\ u > c, \\ u > v \ge 0.$$

移项化简得到$(u-c)(u+c)=(d-v)(d+v)$, 不妨令$x_1=u-c,y_1=u+c,x_2=d-v,y_2=d+v$, 那么有$$\begin{aligned}u &=\frac{x_1+y_1}{2}, \\ c &=\frac{y_1-x_1}{2}, \\ d &=\frac{x_2+y_2}{2}, \\ v &=\frac{y_2-x_2}{2}.\end{aligned}$$

令$x_1=gx,x_2=gy, \gcd(x,y)=1$, 那么$y_1=ky,y_2=kx$. 可以用Stern-Brocot Tree枚举$(x,y)$, 然后枚举$g$, 根据上面的不等式可以算出$k$的范围. 这样直接暴力可以在1分钟内出解了. 注意到, 实际上$(x,y,g)$就是枚举了所有的$(x_1,x_2)$, 因此可以考虑直接枚举$(x_1,x_2)$然后用openmp加速, 大概可能很快出解.

## 514. Geoboard Shapes

## 515. Dissonant Numbers

## 516. $5$-smooth totients
令$n=\prod p_i^{e_i}$, 显然如果$p_i \ne 2,3,5$, 那么$e_i=1$且$p_i-1$只包含$2,3,5$这三个质因子. 于是可以枚举出所有的$p$, 然后再dfs一遍计算答案就好了.

## 517. A real recursion

## 518. Prime triples and geometric sequences
化简一下可以得到$a=kx^2-1,b=kxy-1,c=ky^2-1, x < y, \gcd(x, y)= 1$, 然后枚举$k,x,y$就好了.

## 519. Tricolored Coin Fountains

## 520. Simbers

## 521. Smallest prime factor

## 522. Hilbert's Blackout

## 523. First Sort I
可以很明显第发现, 如果第$p_i$前面有$x$数比它小, 那么需要调整$2^{k-1}$次才能排好这个位置. 于是枚举$i, p_i, k$算下方案数就好了.

## 524. First Sort II

## 525. Rolling Ellipse

## 526. Largest prime factors of consecutive numbers

## 527. Randomized Binary Search

## 528. Constrained Sums

## 529. $10$-substrings

## 530. GCD of Divisors

## 531. Chinese leftovers
枚举$n$和$m$, 然后用同余方程合并解决就好了.

## 532. Nanobots on Geodesics

## 533. Minimum values of the Carmichael function

## 534. Weak Queens

## 535. Fractal Sequence

## 536. Modulo power identity

## 537. Counting tuples

## 538. Maximum quadrilaterals

## 539. Odd elimination

## 540. Counting primitive Pythagorean triples
我们知道互素勾股数对的这个公式$x^2+y^2=z^2$, $x=2ab,y=a^2-b^2,z=a^2+b^2$, 其中$\gcd(a,b)=1,a \text{ mod } 2 \ne b \text{ mod } 2$. 根据这个公式, 这个题有了很多计数的方法.

### 方法一

考虑枚举$a$ $(2 \le a \le \sqrt{n})$, 那么如果$a$是偶数, 只需要计算集合$\{w | \gcd(a, w) = 1 \text{ and } 0 < w <= \min(\sqrt{N-a^2}, a - 1) \}$的大小. 如果$a$是奇数, 那么只需要计算集合$\{ w | \gcd(a, w) = 1 \text{ and } 0 < w <= \frac{\min(\sqrt{N-a^2}, a - 1)}{2} \}$的大小.

问题变成给出一个$x$和$y$, 问区间$[1,y]$内有多少数和$x$互质. 这个可以容斥做, 考虑$x$的质因数集合$\{p_1,p_2,..,p_k\}$, 那么答案显然就是$y-\sum\limits_{i} \frac{y}{p_i} + \sum\limits_{i < j}\frac{y}{p_ip_j}+...$.

### 方法二
令$$C(n)=\sum\limits_{a < b, a^2+b^2 \le n}=\sum_{2 q^2< n}\left(\left\lfloor\sqrt{n-q^2}\right\rfloor-q\right)$$那么$$P(n)=\sum_d \mu(d) C\left(\frac{n}{d^2}\right) - \sum_{d\,odd} \mu(d) C_{odd}\left(\frac{n}{d^2}\right)$$其中$$C_{odd}(n) = \sum_{2 q^2< n, q\,odd}\left(\left\lfloor\frac{\sqrt{n-q^2}+1}{2}\right\rfloor-\frac{q+1}{2}\right)$$

如果定义$$C_{oe}(n)=\sum_{p\,odd,q\,even}\mathbf{1}_{p^2+q^2\le n}$$那么$$P(n)=\sum_{d\,odd}\mu(d)C_{oe}\left(\frac{n}{d^2}\right)$$形式上更加简洁.

### 方法三
令$$\begin{aligned}
Q\left(n\right) & =\#\left\{ \left(x,y\right):\gcd\left(x,y\right)=1,x>0,y>0,x^{2}+y^{2}\leq n,x>y\right\} \\
Q'\left(n,k\right) & =\#\left\{ \left(x,y\right):\gcd\left(x,y\right)=k,x>0,y>0,x^{2}+y^{2}\leq n,x>y\right\}
\end{aligned}$$那么$$P\left(n\right)=\sum_{i\geq0}\left(-1\right)^{i}Q\left(\frac{n}{2^{i}}\right),\ Q\left(1\right)=0$$

令$$N(r^2)=\#\left\{ \left(x,y\right):x>y,x^{2}+y^{2}\leq r^{2},x>0,y>0,x>y\right\}$$那么有$$
\begin{aligned}
N\left(n\right) & =\sum_{k\geq1}Q'\left(n,k\right)\\
N\left(n\right) & =Q\left(n\right)+\sum_{k\geq2}Q'\left(n,k\right)
\end{aligned}$$化简下得到$N\left(n\right)=Q\left(n\right)+\sum_{k\geq2}Q\left(\left\lfloor \frac{n}{k^{2}}\right\rfloor \right)$, 于是$Q\left(n\right)=N\left(n\right)-\sum_{k\geq2}Q\left(\left\lfloor \frac{n}{k^{2}}\right\rfloor \right)$

## 541. Divisibility of Harmonic Number Denominators

## 542. Geometric Progression with Maximum Sum

## 543. Prime-Sum Numbers
根据[哥德巴赫猜想](https://en.wikipedia.org/wiki/Goldbach%27s_conjecture), 所有大于2的奇数都可以表示成2个素数的和. 于是答案可以分成4部分:

1. $P(x,1)=1$, 显然$x$是素数, 于是答案是$\pi(n)$.

2. $P(x,2)=1$, $x$是一个奇数, 如果$n > 2$那么答案是$\pi(n-2)-1$, 否则答案是$0$.

3. $P(x,k)=1$, $x$是一个偶数并且$k \ge 2$, 那么$k$不能超过$\frac{x}{2}$, 答案是$\frac{1}{2} \cdot \lfloor \frac{n}{2} \rfloor \cdot \lfloor \frac{n-2}{2} \rfloor$.

4. $P(x,k)=1$, $x$是一个奇数且$k \ge 3$, 那么$k$最大能到$\frac{x-1}{2}$, 于是答案是$\frac{1}{2}\cdot \lfloor \frac{n-5}{2} \rfloor \cdot \lfloor \frac{n-3}{2} \rfloor$.

前两种可以直接算, 后两种就等差数列求个和好了.

## 544. Chromatic Conundrum

## 545. Faulhaber's Formulas
可以知道$D(k)$就是第$k$个伯努利数的分母. 第$n$个伯努利数的分母可以这么计算出来: $\prod_{d \mid n} (d+1)[d + 1\text{ is prime}]$. 然后通过简单的计算可以知道$308 \mid n$, 也就是说$n=308i$. 同样我们知道如果某个$308i$不满足条件, 那么$308ij$也是不满足条件的. 于是我们可以用筛法来求出所有可行的$i$.

## 546. The Floor's Revenge

## 547. Distance of random points within hollow square laminae
从边长为$a$和$b$的矩形中选两个点, 距离期望公式如下:
$$f(a,b)=\frac{1}{15}\left[\frac{a^3}{b^2}+\frac{b^3}{a^2}+\sqrt{a^2+b^2}\left(3-\frac{a^2}{b^2}-\frac{b^2}{a^2}\right)+\frac{5}{2}\left(\frac{b^2}{a}\log{\frac{a+\sqrt{a^2+b^2}}{b}}+\frac{a^2}{b}\log{\frac{b+\sqrt{a^2+b^2}}{a}}\right)\right]$$
然后枚举每个$x,y$以及左上角的位置, 这部分的答案贡献可以用容斥算出来.

## 548. Gozinta Chains
很容易写出递推式$f(n)=\sum\limits_{d|n,d < n}f(d)$, 显然如果令$n=\prod\limits_{i=1}^{k}p_i^{t_i}$, 答案之和$\{t_i\}$构成的集合有关, 于是可以先生成每个集合, 并且算出每个集合$S$对应的答案$f(S)$. 然后考虑每个$f(S)$的质因数分解, 如果指数部分构成的集合和$S$相同, 那么$f(S)$就是一个合法的$n$.

## 549. Divisibility of factorials
考虑$n=\prod\limits_{i=1}^{k}p_i^{t_i}$, 那么只要$m!$整除每个$p_i^{t_i}$就好了, 这个可以二分答案确定, 对所有的$p_i^{t_i}$取最大的$m$就是$s(n)$的值.

## 550. Divisor game
可以$O(n\log n)$暴力算出每个$sg(n)$, 然后可以观察到$sg(n)$的最大值不超过$64$, 于是就可以直接矩阵乘法搞了. 也可以用`fwt`做异或卷积.
