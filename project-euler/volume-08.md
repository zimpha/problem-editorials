# Volume 08

## 351. Hexagonal orchards
很容易推出答案是$6((n^2 + n)/2 - \sum\limits_{k=1}^n \phi(k))$. 用筛法求出$\phi(x)$即可.

## 352. Blood tests

## 353. Risky moon

## 354. Distances in a bee's honeycomb

## 355. Maximal coprime subset

## 356. Largest roots of cubic polynomials

## 357. Prime generating integers
可以算出$n$要是一个square free number, 否则可以找到一个$d$使得$\gcd(d,n/d) \ne 1$. 于是枚举所有的square free number, 然后暴力枚举$d$即可.

## 358. Cyclic numbers
可以在wiki上搜到一些关于[Cyclic number](https://en.wikipedia.org/wiki/Cyclic_number)的结论. 知道有$m = \frac{10^{p - 1} - 1}{p}\text{ mod }10^5 = 56789$, 化简一下有$99999 \equiv 56789p\text{ mod }10^5$, 于是$p\text{ mod }10^5 = 09891$.

然后有$\frac{1}{p}=0.00000000137...$, 又知道$10$必须是$p$的原根. 于是就可以根据这些条件计算出可行的$p$. 另外也可以发现最后答案就是$\frac{9(p-1)}{2}$, 当然也可以直接暴力求解.

## 359. Hilbert's New Hotel
[oeis](http://oeis.org/A083362)上有这个数列, 根据规律做些优化就好了.

## 360. Scary Sphere

## 361. Subsequence of Thue-Morse sequence

## 362. Squarefree factors

## 363. Bézier Curves

## 364. Comfortable distance

## 365. A huge binomial coefficient
用lucas定理, 然后中国剩余定理合并就好了.

## 366. Stone Game III

## 367. Bozo sort

## 368. A Kempner-like series

## 369. Badugi

## 370. Geometric triangles

## 371. Licence plates
显然可以把数分成3组, $\{000,001,...,499\}$, $\{501,502,...,999\}$和$500$. 令$f(x)$表示没看见过$500$, 并且已经收集到$x$种不同数字的期望次数, $g(x)$则是看见过一次$500$, 并且已经收集到$x$种不同数字的期望次数. 递推式很好求:$$\begin{aligned}
g(k) &= \frac{(998-2k)g(k+1)+1000}{999-k} \\
f(k) &= \frac{(998-2k)f(k+1)+g(k)+1000}{999-k}\end{aligned}$$初始值$f(500)=g(500)=0$, 答案就是$f(0)$.

## 372. Pencils of rays

## 373. Circumscribed Circles

## 374. Maximum Integer Partition Product

## 375. Minimum of subsequences

## 376. Nontransitive sets of dice

## 377. Sum of digits, experience 13

## 378. Triangle Triples
求出$dT(i)=d(\frac{n}{2})d(n+1)$, 然后就直接用树状数组优化dp就好了. 可以考虑先离散化$dT$, 这样可以速度更快.

## 379. Least common multiple count

## 370. Amazing Mazes!

## 381. (prime-k) factorial
威尔逊定理的推广:$$
\begin{cases}
(p-1)! \equiv -1 \text{ mod }p, \\
(p-2)! \equiv 1 \text{ mod }p \\
(p-3)! \equiv \frac{p - 1}{2}\text{ mod }p \\
(p-4)! \equiv (-1)^{\frac{p}{3}+1}\frac{p+1}{6}\text{ mod p} \\
(p-5)! \equiv rh + \frac{r^2-1}{24}\text{ mod }p, h=\frac{p}{24}, r=p-24h \end{cases}$$

## 382. Generating polygons

## 383. Divisibility comparison between factorials

## 384. Rudin-Shapiro sequence

## 385. Ellipses inside triangles

## 386. Maximum length of an antichain

## 387. Harshad Numbers
先dfs计算出所有的`right truncatable Harshad number`, 然后一个个枚举判断即可.

## 388. Distinct Lines

## 389. Platonic Dice
一层层展开, 暴力dp就好了.

## 390. Triangles with non rational sides and integral area

## 391. Hopping Game

## 392. Enmeshed unit circle

## 393. Migrating ants

## 394. Eating pie

## 395. Pythagorean tree

## 396. Weak Goodstein sequence
首先在wiki上找到[Goodstein's theorem](https://en.wikipedia.org/wiki/Goodstein%27s_theorem). 在很下面有个计算序列长度的算法, 这个算法同样可以套在`weak Goodstein sequence`中, 于是算一下就好了. 算法中用到一个[Fast-growing hierarchy](https://en.wikipedia.org/wiki/Fast-growing_hierarchy), 同样参考wiki即可.

## 397. Triangle on parabola

## 398. Cutting rope

## 399. Squarefree Fibonacci Numbers

## 400. Fibonacci tree game
