# Volume 07

## 301. Nim
显然只有当$n \oplus 2n \oplus 3n= 0$的时候才有$X(n,2n,3n)=0$, 直接$2^{30}$枚举$n$就好了. 似乎答案就是$fib(32)$.

## 302. Strong Achilles Numbers
xxx

## 303. Multiples with small digits
可以直接用bfs暴力算出答案, $f(9999)$有点大, 已经超过long long了, 但是可以用`__int128`存下, 还是可以暴力的.

## 304. Primonacci
找出$2 \times 10^7$以内的素数, 然后用区间筛法求出$[10^{14}, 10^{14}+10^{7}]$以内的素数, 然后矩阵乘法求fibonacci数就好了.

## 305. Reflexive Position

## 306. Paper-strip Game
xxx

## 307. Chip Defects
用容斥原理做, 求出小于$3$的概率, 然后减掉即可. 这部分概率就是满足$x+2y=k$, 表示有$x$个chip有$1$个defect, $y$个chip有$2$个defect. 对于一组$(x,y)$概率是$\frac{\binom{n}{x}\binom{n-a}{b}}{2^b}\frac{k!}{n^k}$. 取对数计算即可.

## 308. An amazing Prime-generating Automaton
xxx

## 309. Integer Ladders
xxx

## 310. Nim Square
xxx

## 311. Biclinic Integral Quadrilaterals

## 312. Cyclic paths on Sierpiński graphs
xxx

## 313. Sliding game
可以找出如下的公式$$
\begin{aligned}
S(n,m) &= 6m+2n-13, & n < m \\
S(n,m) &= 6n+2m-13, & n > m \\
S(n,m) &= 8n-11, & n = m \end{aligned}$$

于是枚举素数$p$, 分两种情况计算即可.

## 314. The Mouse on the Moon

## 315. Digital root clocks
按照题意直接模拟就好了.

## 316. Numbers in decimal expansions
xxx

## 317. Firecracker
一个物理题. 考虑两种最极端的情况:

1. 垂直往上, 这个我们可以算出一个最高点.
2. 水平射出, 我们可以算出一个最远点.

显然, 这个东西的切面就是连接这两个的抛物线. 然后这个抛物线旋转一周就的到了答案. 公式是: $
\frac{\pi(2gvh + v^3)^2}{4g^3}$

## 318. 2011 nines

## 319. Bounded Sequences

## 320. Factorials divisible by a huge integer

## 321. Swapping Counters
可以算出$M(n)=n(n+2)$, 于是令$n(n+2)=\frac{m(m+1)}{2}$, 化简一下得到$8n^2+16n+1 = k^2$ ($k$是和$m$有关的整数). 解一解可以得到如下递推式:$$
\begin{aligned}
n_i &=2n_{i-1}+k_{i-1}+2 \\
k_i &=8n_{i-1}+3k_{i-1}+8\end{aligned}$$初始解有$(n_0,k_0)=(0,1),(1,5)$.

## 322. Binomial coefficients divisible by 10

## 323. Bitwise-OR operations on random integers
很容易知道答案是$\sum\limits_{i=0}^{\infty}1-(1-0.5^i)^{32}$. 取个上界$100$精度就够了.

## 324. Building a tower

## 325. Stone Game II

## 326. Modulo Summations

## 327. Rooms of Doom

## 328. Lowest-cost Search

## 329. Prime Frog
可以很容易列出概率转移方程, 随便计算下就好了.

## 330. Euler's Number

## 331. Cross flips

## 332. Spherical triangles

## 333. Special partitions
xxx

## 334. Spilling the beans

## 335. Gathering the beans

## 336. Maximix Arrangements
暴力枚举$11!$就好了.

## 337. Totient Stairstep Sequences
令$f(x)$表示以$x$结尾的方案数, $f(x)=\sum\limits_{y < x}f(y)[\phi(y) < \phi(x)][\phi(x) < y]$. 令$sf(x)$是$f(x)$的前缀和, 那么$f(x)=\sum\limits_{y<x}f(y)[\phi(x) < y] - f(\phi(x))$. 前者用树状数组求和就好了.

## 338. Cutting Rectangular Grid Paper

## 339. Peredur fab Efrawg

## 340. Crazy Function
把那个式子化简化简可以得到$F(n) = n + 4(k+1)a-(3k+4)c, n \in [n - (k+1)a, n-ka]$. 于是就是一个等差数列求和.

## 341. Golomb's self-describing sequence

## 342. The totient of a square is a cube

## 343. Fractional Sequences
xxx

## 344. Silver dollar game

## 345. Matrix Sum
$dp(i,S)$表示前$i$行, 选了哪些列已经被选过了的最优值. 枚举下一行选哪个列即可.

## 346. Strong Repunits
枚举$b$, 那么显然这个数是$\frac{b^k-1}{b-1}, k \ge 1$. 于是只要把这些数存进一个map, 然后枚举哪些数出现了2次即可. 当然对于base $n$,$n+1$显然也是repunit, 这个需要判断下map中只出现一个数.

## 347. Largest integer divisible by two primes
对于每个数$n$, 可以质因数分解, 然后如果他只有两个质因数$(p,q)$, 那么更新下$(p,q)$的答案. 最后求个和就好了.

## 348. Sum of a square and a cube
枚举$i$和$j$, 使得$i^2+j^3$小于某个阈值(我取了$10^9$), 然后暴力算下即可.

## 349. Langton's ant

## 350. Constraining the least greatest and the greatest least
