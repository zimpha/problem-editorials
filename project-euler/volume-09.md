# Volume 09

## 401. Sum of squares of divisors
$$\sum_{k=1}^n k^2 \lfloor \frac{n}{k} \rfloor =\sum_{k=1}^{\lfloor \frac{n}{\lfloor \sqrt n \rfloor + 1} \rfloor} k^2 \lfloor \frac{n}{k} \rfloor +\sum_{d=1}^{\lfloor \sqrt n \rfloor} d \left( \sum_{\lfloor n / (d + 1) \rfloor < k \leq \lfloor n / d \rfloor} k^2 \right)$$
其中
$$\sum_{\lfloor \frac{n}{d + 1} \rfloor < k \leq \lfloor \frac{n}{d} \rfloor} k^2 =
f(\lfloor \frac{n}{d} \rfloor) - f(\lfloor \frac{n}{d + 1} \rfloor)$$
其中$f(n) = \frac{1}{6} n (n + 1) (2n + 1)$.

## 402. Integer-valued polynomials

## 403. Lattice points enclosed by parabola and line

## 404. Crisscross Ellipses

## 405. A rectangular tiling

## 406. Guessing Game

## 407. Idempotents
一个很暴力的方法是考虑枚举$a$, 那么显然$n \mid a(a-1)$, 于是可以枚举$a(a-1)$的约数$x > a$, 用$a$更新$M(x)$即可.

考虑另一个方向, 令$n=\prod p_i^{e_i}$, 那么$a^2 \equiv a \text{ mod }n$当且仅当$a \equiv 0 \text{ mod } m_1, a \equiv 1 \text{ mod } m_2$, 其中$m_1\cdot m_2=n, \gcd(m_1,m_2)=1$. 于是枚举$n$, 以及枚举$m_1$, 就可以算出$m_1$, 然后就可以得到$a=m_1\cdot \mathrm{inv}(m_1,m_2)$, 其中$\mathrm{inv}(m_1,m_2)$表示$m_1$在$\text{ mod }m_2$下的逆元.

## 408. Admissible paths through a grid

## 409. Nim Extreme

## 410. Circle and tangent line

## 411. Uvarphill paths

## 412. Gnomon numbering

## 413. One-child Numbers

## 414. Kaprekar constant

## 415. Titanic sets

## 416. A frog's trip

## 417. Reciprocal cycles II

## 418. Factorisation triples

## 419. Look and say sequence

## 420. $2\times 2$ positive integer matrix

## 421. Prime factors of $n^{15}+1$

## 422. Sequence of points on a hyperbola

## 423. Consecutive die throws

## 424. Kakuro

## 425. Prime connection
显然在计算$F(N)$过程中, 用到的数的范围不会超过$10N$. 于是处理出$10^8$以内的素数, 用dijkstra计算出通过relative关系到达$x$的路径中最大值的最小值$f(x)$, 那么$F(N)=\sum\limits_{p < N}[f(p)>p]$.

## 426. Box-ball system

## 427. $n$-sequences

## 428. Necklace of circles

## 429. Sum of squares of unitary divisors
显然$S(n)$是一个积性函数, 可以得到$S(p^e)=1+p^{2e}$. 分解阶乘质因数, 然后算下就好了.

## 430. Range flips

## 431. Square Space Silo

## 432. Totient sum

## 433. Steps in Euclid's algorithm

## 434. Rigid graphs

## 435. Polynomials of Fibonacci numbers
简单推导下可以得到$F_n(x) = \frac{f_{n}x^{n+2} + f_{n+1}x^{n+1} - x}{x^2+x-1}$. 关于取模, 可以用这个公式解决$\frac{a}{b} \text{ mod } m = \frac{a \text{ mod } bm}{b}$.

## 436. Unfair wager

## 437. Fibonacci primitive roots

## 438. Integer part of polynomial equation's solutions

## 439. Sum of sum of divisors

## 440. GCD and Tiling

## 441. The inverse summation of coprime couples

## 442. Eleven-free integers

## 443. GCD sequence
打表观察可以发现如果$\gcd(n,g(n-1)) \ne 1$, 必然有$g(n)=3n$. 如果已知$g(n)=3n$, 那么下一个满足条件的$n$可以这么确定: 找出$n^2-1$的最小质因子$p \ge 3$, 那么下一个就是$n+\frac{p-1}{2}$.

用这个方法跳到$10^{15}$附近, 然后加上间隔就好了.

## 444. The Roundtable Lottery

## 445. Retractions A

## 446. Retractions B

## 447. Retractions C

## 448. Average least common multiple
化简下可以得到$S(n) = \sum\limits_{k=1}^n \lfloor \frac{n}{k}\rfloor \cdot f(k)$, 其中$f(n)=n\varphi(n)$. 于是我们需要求$F(n)=\sum\limits_{i=1}^{n}i\varphi(i)$, $F(n)$的递推式可以变成$$
F(n) = \frac{n(n+1)(2n+1)}{6} - \sum\limits_{k=2}^n k \cdot F(\lfloor \frac{n}{k}\rfloor)$$递归+记忆化计算即可.

## 449. Chocolate covered candy

## 450. Hypocycloid and Lattice points
