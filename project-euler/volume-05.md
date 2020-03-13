# Volume 05

## 201. Subsets with a unique sum

用背包计算出和为$S$的数的方案数就好了, 可以用`__int128`, 也可以用long long, 然后自然溢出. 更合理的方法是找几个大质数取模, 然后crt合并.

## 202. Laserbeam

把平面用正三角形平铺, 把$C$放在原点, 那么其他可能是$C$点的坐标$(x,y)$满足$\mid x - y \mid \text{ mod } 3 = 0$. 显然, 反射$n$就是相当于, 从原点到$(x,y)$这个点和$n$条线段有交, 并且这个点没有被挡住, 也就是说$\gcd(x,y)=1$.

可以很容易算出来, 从原点到点$(x,y)$的连线恰好经过$2(x+y)-3$条线段, 也就是要解下面这个方程的解数:
$$
\begin{eqnarray}
x+y=\frac{n+3}{2} \\ \mid x - y \mid \text{ mod } 3 = 1 \\ \gcd(x, y) = 1 \end{eqnarray}$$不妨令$x=3k+2$, 那么实际上是解$\gcd(3k+1,\frac{n+3}{2})=1$的$k$的个数, 枚举出$\frac{n+3}{2}$的质因数, 直接用容斥原理和扩展欧几里得计算.

论坛里面给出了一个[公式解](https://projecteuler.net/thread=202;post=22368), 令$m=\frac{n+3}{2}$, 那么答案就是$\frac{\phi(m)-2^r}{3}$, 其中$\phi(m)$是欧拉函数, $r$是$m$满足模3余2的质因子个数.

## 203. Squarefree Binomial Coefficients

暴力分解阶乘的质因数就好了.

## 204. Generalised Hamming Numbers

总个数不是很多, 于是可以一个质数一个质数地扩展上去.

## 205. Dice Game
背包计算出摇出和为$x$的概率$P_{\text{Peter}}(x)$和$P_{\text{Colin}}(x)$, 答案就是$\sum_{x > y}P_{\text{Peter}}(x)P_{\text{Colin}}(y)$.

## 206. Concealed Square

直接暴力枚举那个要求的数就好了, 在$[101010101, 138902662]$内.

## 207. Integer partition equations

令$x=2^t$, 那么$x^2-x=k$. 如果$t$是整数, 显然$x$是$2$的幂次. 从小到大枚举$x$, 维护$2$的幂次的个数, 以及当前$k$的值.

## 208. Robot Walks
观察下可以知道, 总共有$5$种不同的圆弧, 一个显然的结论就是这些圆弧的数目都要相同才能构成一个环路. 于是可以以当前每种圆弧数目和当前位于那个圆弧上作为状态$(i_0,i_1,i_2,i_3,i_4,d)$, 转移比较显然, 这里不表.

其实上面的状态还可以简化, $d$是不需要的, 我们不妨假设永远在$i_0$圆弧上, 往左和往右转实际上就是把$(i_0,i_1,i_2,i_3,i_4)$这个$5$元组左移和右移(类似相对运动这种), 于是状态最多只有$14^5=537824$种.

## 209. Circular Logic

考虑枚举$(a,b,c,d,e,f)$这个6元组的值, 显然$\tau(a,b,c,d,e,f)$和$\tau(b,c,d,e,f,a\text{ XOR }(b\text{ AND }c))$不能同时为0. 把$(a,b,c,d,e,f)$当做图中的一个节点, 那么就在$(a,b,c,d,e,f)$和$(b,c,d,e,f,a\text{ XOR }(b\text{ AND }c))$之间连一条边.

实际上就是求这个$2$-SAT的方案数, 画出图来可以发现, 这个图是由几个环组成的, 长度分别为$\{46,6,6,3,2,1\}$. 对于长度为$n$的环, 我们很容易得出答案就是$f(n)=1+\sum\limits_{k=1}^{n/2}\frac{n\binom{n-k-1}{k-1}}{k}$.

## 210. Obtuse Angled Triangles

分别从$O$和$C$做线段$OC$的垂线, 显然答案被分成了$3$部分. 左右两部分十分简单, 就是$$\sum\limits_{i=0}^{r/4}4i+\sum\limits_{i=0}^{r/2-1}i+(\frac{r}{2})^2+(2r + 1)\frac{r}{2}$$

至于中间部分, 显然要求出以$OC$中点为圆心, 半径为$\frac{r}{8}$的圆内整点个数. 直接暴力枚举$x$坐标计算即可. 最后还需要减去和$OC$共线的那些点.

计算圆内整点个数实际上有$O(r^\frac{2}{3})$的做法, 需要参考论坛里面这个[帖子](https://projecteuler.net/thread=540#229299).

## 211. Divisor Square Sum

$\sigma_2(n)$是个积性函数, $\sigma_2(p^k)=1 + p^2 + p^4 + ... + p^{2k}$. 可以直接$O(n \log n)$筛出来, 也可以用上面公式, 先线性筛出所有质数, 以及每个数的最小质因子, 然后暴力分解质因数就好了.

## 212. Combined Volume of Cuboids
枚举当前$z$坐标的值, 在$o-xy$上做矩形并就好了.

## 213. Flea Circus
每只跳蚤都是独立的, 于是可以枚举每只跳蚤, 计算出$5o$步以后在每个位置$(x,y)$的概率$p_i(x,y)$. 然后每个格子也是独立的, 只需要计算出每个格子$50$步以后不被占据的概率, 然后全部加起来就好了. 也就是说答案就是$$\sum\limits_{x,y}\prod\limits_{i}(1-p_i(x,y))$$

## 214. Totient Chains
线性筛计算出$\phi(n)$, 然后暴力枚举`totient chain`的长度就好了.

## 215. Crack-free Walls

$dp(i,S)$表示当前处理到第$i$行, 状态为$S$的方案数, $S$用三进制储存, 然后dfs暴力转移就好了.

## 216. Investigating the primality of numbers of the form $2n^2-1$

暴力枚举每个$n$, 然后用`miller-rabin`测试跑的还是挺快的. 出题人用的是筛法, 考虑枚举奇质数$p$, 那么$p \mid 2n^2-1$当且仅当$n^2=\frac{p+1}{2} \text{ mod } p$. 显然$n < p$中最多只有两个解$x_0$和$x_1$, 那么就可以筛去所有的$x_0+kp$和$x_1+kp$, 这些显然都是合数.

## 217. Balanced Numbers
令$f(i,s)$和$g(i,s)$表示前$i$位数位和为$s$(前半部分加, 后半部分减)的个数以及数字和, 转移只需要枚举当前位是什么数字就好了.

## 218. Perfect right-angled triangles
用了神奇的`Tree of Primitive Pythagorean Triples`, 最后答案居然是0. 证明如下:

由于$a^2+b^2=c^2, \gcd(a,b,c)=1$, 可以令$a=u^2-v^2,b=2uv,c=u^2+v^2=w^2$其中$\gcd(u,v)=1$, 显然$(u,v,w)$又是一对互素勾股数. 于是令$u = x^2 - y^2, v = 2xy$, 那么$S= \frac{ab}{2} = (u-v)(u+v)uv= 2(u-v)(u+v)(x-y)(x+y)xy$显然$3 \mid S$, $4 \mid S$. 由于$u^2+v^2=w^2$, 那么$u^2 \equiv v^2 \text{ mod } 7$或者$de \equiv 0 \text{ mod } 7$, 所以$7 \mid S$.

## 219. Skew-cost coding
考虑从根节点开始, 给做儿子代价加$1$, 给右儿子代价加$4$, 那么最后叶子的代价和就是这种`code`的$costs$, 于是为了达到最小$cost$, 显然每次需要选择一个$cost$最小的叶子进行扩展. 然后可以注意到每次权值的种类不多, 于是维护一个$(weight, cnt)$的$2$元组, 不断扩展就好了.

## 220. Heighway Dragon
搜了搜[Dragon curve](http://mathworld.wolfram.com/DragonCurve.html), 可以在Wolfram MathWorld上找到. 令$f_0=1,g_0=0$, 那么$n$阶的`Dragon curve`是$f_n=f_{n-1}+1+g_{n-1},g_n=f_{n-1}+0+g_{n-1}$. 递归结构很明显了, 于是只要随便算算就好了.

## 221. Alexandrian Integers

打表可以在[oeis](https://oeis.org/A147811)上找到`Alexandrian Integers`的形式为$p(p + d)(p + \frac{p^2+1}{d}), d \mid p^2 + 1$. 枚举一个$p$的上界(大概$10n$)就够了, 然后暴力分解质因数$p^2+1$, 枚举出所有$d$, 求出所有可行的`Alexandrian Integers`, 排个序, 找出第$n$大, 可是这样非常慢. 有若干个加速的方法:

第一个是用$(ac-bd)^2 + (ad+bc)^2 = (a^2 + b^2)(c^2 + d^2)$(叫做[Brahmagupta–Fibonacci identity](https://en.wikipedia.org/wiki/Brahmagupta%E2%80%93Fibonacci_identity)), 考虑对题目中定义直接化简, 可以得到$(p+r)(q+r)=r^2+1$, 本来做法和上面一样是要枚举$r^2+1$的约数. 但是可以令$ac-bd=1,r=ad+bc$, 那么$p+r=a^2+b^2,q+r=c^2+d^2$然后$a,b,c,d$的可以用[Stern-Brocot tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)生成.

上面方法可以进一步简化, 令$x=a^2+b^2 < y = c^2+d^2$, $r=ad+ac, p+r=a^2+b^2,q+r=c^2+d^2$其实可以变成$p=ac+bd,q=p+x,r=p+y$(考虑Stern-Brocot tree相邻两项就可以得到), 当往左走的时候, $z = (a+c)^2 + (b+d)^2 = x + y + 2p$, 会得到
$$
\begin{aligned}
p^\prime &= a(a+c) + b(b+d) = p + x = q \\ q^\prime &= p^\prime+x = p + 2x = 2q-p \\ r^\prime &= p^\prime + z = 3p + 2x + y = 2q+r \end{aligned}$$同样往右走的时候会得到
$$
\begin{aligned}
p^{\prime\prime} &= r \\ q^{\prime\prime} &= 2r-p \\ r^{\prime\prime} &= 2r+q \end{aligned}$$于是只要从初始值$(p,q,r)=(1,2,3)$出发按照这两个转移遍历就好了.

## 222. Sphere Packing
令$f(S,i)$表示当前使用的球集合为$S$, 最后一个球为$i$的最小长度, 枚举下一个没有被使用的球$j$, 计算贡献就好了.

## 223. Almost right-angled triangles I
移项可以得到$(a+1)(a-1)=(c-b)(c+b)$, 枚举$a$, 对$(a+1)(a-1)$做质因数分解, 枚举它的约数就可以求出$b$和$c$. 虽然这个方法挺快的, 但还是不够快, 参考#221, 我们可以猜测$(a,b,c)$也可以用一些转移直接求出来.

事实上这个转移矩阵就是`Tree of Primitive Pythagorean Triples`里面的三个矩阵, 只需要考虑初始值$(a,b,c)=(1,1,1) \text{ or }(1,2,2)$即可. 这里详细讲了如何构造这三个矩阵[The Trinary Tree(s) underlying Primitive Pythagorean Triples](http://www.cut-the-knot.org/pythagoras/PT_matrix.shtml).

## 224. Almost right-angled triangles II
和#223类似, 用`Tree of Primitive Pythagorean Triples`里面的三个矩阵就好了, 初始值为$(a,b,c)=(2,2,3)$. 事实上, 这个矩阵应该适用与任何$a^2+b^2=c^2\pm h$吧.

## 225. Tribonacci non-divisors
大约猜了猜$T(n) \text{ mod } m$的周期差不多是$100m$, 于是枚举每个$m$, 暴力枚举周期内的数, 判断是否存在$T(i) \text{ mod } m =0$.

## 226. A Scoop of Blancmange
这个圆和这条曲线的一个交点是$(0.5, 0.5)$, 然后二分出另一个交点, 计算$y(x)$可以暴力枚举$n$, 直到不够精度(大概$10^{-15}$就差不多了)为止. 然后再用simpson积分搞一下.

## 227. The Chase
显然只和当前两个骰子的最短距离有关. 令$E(d)$表示, 当前两个骰子最短距离为$d$的期望步数, 枚举转移, 然后可以列出方程组, 高斯消元解一下就好了.

## 228. Minkowski Sums
对于给出来的两个凸包$P$和$Q$, 求他们的`Minkowski sum`很简单, 把所有边按照极角排序, 然后依次连接起来就好了. 对于题目中的$S(n)$极角序可以用整数来表示, 就是$\frac{360i}{n}$. 于是这题事实上就是求集合枚举所有分数$\frac{360i}{j}$ $(0 \le i < j)$, 去个重.

## 229. Four Representations using Squares

开了个大小为$2 \times 10^9$的bitset, 然后暴力枚举. 一些优化的地方, $n=a^2+b^2$ 当且仅当$n$可以分解成$(4k+1)c^2$或者$2c^2$; $n = a^2+ 3b^2$当且仅当$n$可以分解成$(3k+1)c^2$. 这个[帖子](https://projecteuler.net/thread=229;post=26432)有详细的说明.

## 230. Fibonacci Words
随便递归下就好了.

## 231. The prime factorisation of binomial coefficients

直接暴力枚举质因数分解就好了.

## 232. The Race
这个显然只能倒着分析, 令$p(i,j)$表示当前两人的得分分别是$i$和$j$, 且当前是第二个人掷骰子的获胜概率, 我们知道边界$p(100,i)=0,p(i,100=1$. 考虑枚举第二个人要掷$t$次骰子, 得到$s=2^{t-1}$分的概率$q$是$\frac{1}{2^t}$, 那么我们可以得出$p_s(i,j)=\frac{1-q}{2}p(i+1,j)+\frac{q}{2}(p(i+1,j+s)+p(i,j+s))+\frac{1-q}{2}p_s(i,j)$
注意当$s+j \ge 100$的时候, 中间哪项要变成$\frac{q}{2}$, 因为已经轮不到第一个选手掷骰子了.

## 233. Lattice points on a circle
可以找到这样的一个规律, $f(n)=8g(n)+4, g(n)=\frac{(\prod_i 2f_i+1)-1}{2}$, 其中$n=2^e\prod_i p_i^{f_i} \prod_j q_j^{t_j}$ $(p_i \equiv 1 \bmod 4, q_j \equiv 3 \bmod 4)$.

于是推导一下知道$\prod_i 2f_i+1=105=3\times 5 \times 7$, 可行的$f_i$有$\{(1,2,3), (3,7), (2,10)\}$. 筛出素数, 暴力枚举就好了.

## 234. Semidivisible numbers
大概只要筛出不超过$\sqrt{999966663333}$的素数就好了, 然后枚举$lps$和$ups$, 我们可以知道对应这对$(lps,ups)$的$n$所在的区间为$[lps^2+1,ups^2-1]$. 容斥算出不同同时被$lps$和$ups$整除的数之和就好了.

## 235. An Arithmetic Geometric sequence
显然可以二分答案, 然后用[Horner's method](https://en.wikipedia.org/wiki/Horner%27s_method)就可以保证精度相对较高地计算.

## 236. Luxury Hampers
考虑枚举`Beluga Caviar`中坏掉的数目$x_1,y_1$, 那么实际上$m$就可以算出来了, 同理我们可以知道$\frac{x_i}{y_i}$的值, 这样就可以确定出所有可能的$(x_i,y_i)$, 然后检查第二个条件就好了. 通过计算可以发现, 这样大概有$10^{13}$的计算量, 显然跑不出来, 然后考虑折半枚举, 分别枚举出$\{(x_2,y_2), (x_3,y_3)\}$和$\{(x_4,y_4), (x_5,y_5)\}$的组合, 问题变成求出是否存在$\frac{x_1+s_x+e_x}{y_1+s_y+e_y}\cdot\frac{18880}{15744}=m=\frac{u}{v}$, 其中$s_x=x_2+x_3$, $s_y=y_2+y_3$,$e_x=x_4+x_5$,$e_y=y_4+y_5$. 把式子化简得到$18880v(x_1+s_x)-15744us_y=15744u(y_1+e_y)-18880ve_x$
于是只要维护出左右的值, 分别排个序, 归并检查是否有相同就好了. 这样的计算量大概只有$10^9$.

## 237. Tours on a 4 x n playing board
$T(n)=2T(n-1)+2T(n-2)-2T(n-3)+T(n-4)$.

## 238. Infinite string tour

打表可以发现这个字符串的周期大概是$10^7$级别, 一个周期内的数字和$m$大概是$10^8$级别的, 那么考虑暴力计算出$p(k)$ $(1 \le k \le m)$, 显然有$p(k+pm)=p(k)$, 随便计算下就好了. 由于这个数列有够随机, 暴力计算$p(k)$的过程十分快, 似乎$p(k)$的范围是$10^2$左右.

## 239. Twenty-two Foolish Primes
枚举哪3个质数位置不变, 剩下来就是要计算$f(n,m)$表示长度为$n$的排列中, 前$m$个数一定要错排的方案数. 用容斥很容易得到$
f(n,m)=n!-\sum_{k=1}^{m}\binom{m}{k}f(n-k,m-k)$答案就是$
\frac{\binom{25}{3}f(97,22)}{100!}
$
## 240. Top Dice
$f(n,last,cnt,sum)$表示前$n$个骰子, 最后一个数字是$last$, 到目前位置$last$已经出现了$cnt$次, 以及当前和为$sum$的方案数, 考虑枚举下一个位置填$x \le last$, 那么:

1. 当$x=last$的时候, $f(n+1,last,cnt+1,new\_sum)\leftarrow \frac{n+1}{cnt+1}f(n,last,cnt,sum)$
2. 当$x < last$的时候, $f(n+1,x,1,new\_sum)\leftarrow (n+1)f(n,last,cnt,sum)$.

## 241. Perfection Quotients
$k$不是很大, 最大大概$7$吧, 于是可以考虑枚举$k$, 搜出可行的答案. 注意到$\sigma(n)=\prod \frac{p^{e+1}-1}{p-1}$, $n=\prod p^e$, 于是有$\frac{2k+1}{2} \frac{\prod p^e}{\prod \frac{p^{e+1}-1}{p-1}}=1$, 于是可以考虑每次枚举$p$, 给当前结果$\frac{x}{y}$乘上$\frac{p^e(p-1)}{p^{e+1}-1}$. 显然$p \mid y$, 我们每次都把先$y$中$p$消掉, 也就是选择那些能使新得到$y$中没有因子$p$的$e$. 这样每次枚举的$p$基本上都是互不相同的. 为了确实保证每个$p$没有被重复枚举, 加个visited数组保存那些素数被枚举过了就好了(可以猜测可行的素数范围不是很大, 大概$1000$以内). 这样爆搜可以在$1$s内出解.

## 242. Odd Triplets
首先通过打表知道, 只有$n=4k+1$的时候才是有解的, 然后忽略$n=1$, 把其他数按照二进制分组, 先$2^0$个, 然后$2^1$个, 然后$2^2$, 依次类推. 然后可以注意到, 第$k$的`Odd Triplets`实际上是就是第$k-1$组以及第$k-1$组翻个倍组成的, 那么第$2^k$组的`Odd Triplets`数目$f(k)=3f(k-1)$.

我们大概就有了一个递归结构, 随便谢谢就好了.

## 243. Resilience

显然$R(d) = \frac{\phi(d)}{d - 1}$, 为了使$d$最小, 最优答案是连续的素数相乘$p_1 \times p_2 \times ... \times p_k$, 然后再乘一个较小的数$q$ $(q \le p_k)$. 于是暴力枚举乘到哪个素数, 然后暴力枚举那个$q$就好了.

## 244. Sliders
用$1$表示红色, $0$表示蓝色, 加上空白格子的位置信息就可以表示一个棋盘的配置, 于是随便dp一下就好了.

## 245. Coresilience
简单推导一下可以知道$n$必须是奇数, 然后我打出$10^6$内的所有合法解, 发现$n$必须是squarefree的. 于是考虑暴力枚举所有squarefree的$n$, 判断$n$是否可行.

不妨假设当前枚举到$x$, 一个合法解$n=xp$, 那么有$k=\frac{xp-1}{xp-\phi(x)(p-1)}$, 移项化简得到$p = \frac{1+k\phi(x)}{x - kd}$, 首先, 我们是知道$p$的范围的, $p_{\max}=\frac{10^{11}}{x},p_{\min}=\text{max-prime-factor}(x)$. 于是我们就可以得到一个合法的$k$的范围. 很显然$k$的范围比较小, 于是通过枚举$k$可以求出$p$, 然后再素数判定下$p$就好了. 而且, $k$一定要是偶数(因为$xp-1$是偶数, $xp-\phi(x)(p-1)$是奇数), 可以再减少一般枚举量.

官方做法是特殊处理`semiprime`($n=pq$那些case), 对于其他square free的$n$, 用上述方法做. 对于`semiprime`, 有$p+q-1 \mid pq-1$, 于是$$
\begin{aligned}
pq-1 &= qk+k(p-1) \\ q(p-k) &= k(p-1)+1 \\ q &=\frac{k(p-1)+1}{p-k}\end{aligned}$$令$d = p-k$, 那么$q =\frac{(p-d)(p-1)+1}{d}$, 也就是$(p-d)(p-1)+1 \equiv 0\text{ mod }d$, 得到$p(p-1)+1 \equiv 0\text{ mod }d$, 因此$d \mid p(p-1)+1$.

枚举$p(p-1)+1$的约数可以用#216的那种筛法, 可以做到$O(n \log n)$.

## 246. Tangents to an ellipse
参考了[这里](http://www.nabla.hr/PC-EllipseAndLine2.htm)的公式, 可以很方便计算$\angle RPS$的值, 然后考虑枚举$x$, 显然对于固定的$x$, $y$越大, 角度越小, 于是就可以二分了. 似乎$P$点的轨迹构成了另一个椭圆, 也许求出方程会更方便.

## 247. Squares under a hyperbola
先暴力dfs计算出$(3,3)$的最小边长$e$, 然后再一边dfs, 暴力计算出有多少正方形边长大于等于$e$.

## 248. Numbers for which Euler’s totient function equals $13!$
注意到$13!=2^{10}\times 3^5 \times 5^2 \times 7 \times 11 \times 13=6227020800$, 由于$\phi(p)=p-1, \phi(p^k)=p^{k-1}(p-1)$, 于是我们要找出满足$p-1 \mid 13!$的那些素数$p$, 这些都是候选的质因子, 考虑$p^k$, 还需要加入$2^2, 2^3,..., 2^{11}$, $3^2,3^2,...,3^6$, $5^2,5^3,5^4$, $7^2,11^2,13^2$这些数, 然后爆搜就好了. 满足条件的数最多只有$182752$个, 全部都搜出来也没事.

也可以考虑用优先队列维护, 然后从小到大扩展每个数.

## 249. Prime Subset Sums

他们的和最大不超过$1600000$, 于是直接背包就好了.

## 250. $250250$

$dp(i, j)$表示前$i$个数选某些数构成子集, 和对250取模的值为$j$的方案数, 直接转移就好了.
