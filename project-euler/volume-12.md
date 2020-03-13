# Volume 12

## 551. Sum of digits sequence
令$ds(n)$表示$n$的数位和, 考虑$a_n=c \cdot 10^{k}+r$, 那么只要$\delta_m < 10^{k}$, 其实$a_{n+m}=c \cdot 10^{k} + \delta_m$, 其中$\delta_0 = r, \delta_{m+1}=\delta_{m}+ds(\delta_{m})+ds(c)$.

不妨令$dp(len,pre,init)$表示从$\delta_0=init$开始, 根据递推式$\delta_{m+1}=\delta_{m}+ds(\delta_m)+pre$, 直到$\delta_m \ge 10^{len}$的最小$m$, 以及当前$\delta_m$的值($dp(len,pre,init)$的值是一个pair).

$dp(len,pre,init)$的转移比较容易, 考虑枚举$init$当前最高位的数字$x$, 那么可以从$dp(len-1,pre+x,init)$转移过来, 具体来说$dp(len,pre,init)[0] += dp(len-1,pre+x,init)[0]$, $dp(len,pre,init)[1]=dp(len-1,pre+x,init)[1]$. 初始边界值是$dp(0,pre,1)=(1,pre), dp(0,pre,init)=(0,init-1)$.

知道了$dp(len,pre,init)$数组之后, 我们显然就可以通过从高到低依次枚举$a_n$的每一位来确定$a_n$.

## 552. Chinese leftovers II
这个题实际上就是要求$A_i \text{ mod } p_j$. 令$q_n$为前$n$个素数的乘积, 那么有下面一个同余方程:$$
\begin{cases}
A_{n+1} \equiv A_n \text{ mod } q_n \\
A_{n+1} \equiv n + 1 \text{ mod } p_{n+1}\end{cases}$$

不妨令$A_{n+1}=A_n+k_nq_n, 0 \le k_n < p_{n+1}$, 那么可以得到$k_n \equiv (n+1-A_n)q_n^{-1} \text{ mod } p_{n+1}$.

那么假设我们得到了$A_n \text{ mod } p_i$的值, 显然就可以递推出$A_{n+1} \text{ mod } p_i$的值了. 由于$300000$以内只有$25997$个素数, 于是可以直接$O(n^2)$暴力更新.

## 553. Power sets of power sets
令$f(n,m)$表示选出来集合的并恰好有$n$种不同数字, 且分成了$m$个连通分量的方案数. 显然$C(n,k)=\sum\limits_{i=1}^{n}f(i,k)$. 考虑如何计算$f(n, m)$, 一个显然的递推式就是$f(n,m)=\sum\limits_{i=1}^{n-1}\binom{n-1}{i-1}f(n-i,m-1)f(i,1)$, 表示单独拿出来一个大小为$i$的联通块, 为了不重复计数, 这个联通块必须包含最小的数. 剩下的问题就是如何计算$f(n,1)$了.

令$g(n)$表示选出若干集合, 他们的并是全集$\{1,2,...,n\}$的方案数, 这个打了下表可以知道就是[A003465](http://oeis.org/A003465), 于是$g(n)=\sum\limits_{k=0}^{n}(-1)^k\binom{n}{k}2^{2^{n-k}-1}$. 知道了$g(n)$以后, $f(n,1)$的式子就显而易见了$f(n,1)=g(n)-\sum\limits_{i=1}^{n-1}f(i,1)g(n-i)\binom{n-1}{i-1}$.

这样我们就有了一个$O(n^2k)$的算法, 滚动数组一下很快就跑出来了. 但是这题还可以用生成函数做的更好.

令$T(n)=2^{2^n-1}$, 定义三个生成函数$f(x)$, $g(x)$和$h(x)$: $$
\begin{aligned}
f(x) &:= \sum\limits_{n=0}\frac{T(n)}{n!}x^n, \\
g(x) &:= \sum\limits_{n=0}\frac{T(n+1)-T(n)}{n!}x^n, \\
h(x) &:= \frac{g(x)}{f(x)}. \\
\end{aligned}$$

那么, 我们可以知道$C(n,k)$的生成函数是:$$\begin{aligned}
C_0(x) &:= \sum\limits_{n=0}\frac{1}{n!}x^n, \\
C_k(x) &:= \sum\limits_{n=0}\frac{C(n, k)}{n!}x^n = \frac{x}{1-x}\sum\limits_{n=0} d_k(n) x^n, \\
\end{aligned}$$

其中$D_k(x) = \sum\limits_{n=0} \frac{d_k(n)}{n!} x^n =h(x) \cdot C_{k-1}(x)$.

于是用FFT/NTT就可以在$O(kn\log n)$的复杂度解决了.

## 554. Centaurs on a chess board
可以考虑下题目中的$n^2$是如何得到的. 考虑把$2n \times 2n$的棋盘以$2 \times 2$为单位划分成$n \times n$, 那么显然任意一个$2 \times 2$的小块最多只能包含一个centaur. 于是一个$2n \times 2n$的棋盘最多只能放$n^2$个centaur. 然后通过简单的推导可以知道$C(n)=8 \binom{2n}{n}-(3n^2+2n+7)$. 然后用lucas定理计算$C(F_i)$即可.

## 555. McCarthy 91 function
和之前的#340 Crazy Function一样, 可以知道这个东西是一个分段函数. 打个表就可以发现$M_{m,k,s}(n)$以$k-s$为周期, 每个周期内是一个公差为$1$的等差数列, 最高项是$m+k-2s$. 于是找不动点其实就是找一个区间$[m-(x+1)(k-s),m-x(k-s)]$, 使得$m-x(k-s)=m+k-2s$, 化简下得到$x = \frac{2s-k}{k-s}$. 于是只要枚举$u=k-s$, 然后再枚举$xu=2s-k$就可以解出$k,s$. 求出区间后就是一个等差数列求和的问题.

## 556. Squarefree Gaussian Integers
可以回想起#193的公式, 这个题稍微改下那个公式就好了: $f(n) = \sum\limits_{z\text{ such that }|z|^2\leq n} \mu(z) g\left(\dfrac{n}{|z|^2}\right)$. 其中$g(n)$表示有多少proper Gaussian integer$z$满足$|z|^2 \le n$. 至于$\mu(z)$看着参考这个数列[A120630](http://oeis.org/A120630).

## 557. Cutting triangles
根据梅涅劳斯定理, 可以得到$bc(2a+b+c+d)=a^2d$, 枚举$S=a+b+c+d$以及$a,d$, 然后就可以计算出$b,c$了.

## 558. Irrational base
这个题的方法有很多.

### 方法一
注意到$x^3=x^2+1$是数列$a_{n}=a_{n-1}+a_{n-3}$的特征方程. 我们知道有个[Zeckendorf's theorem](https://en.wikipedia.org/wiki/Zeckendorf%27s_theorem), 可以用Fibonacci数表示一个整数. 我们还知道有个[Golden ratio base](https://en.wikipedia.org/wiki/Golden_ratio_base), 可以用base-$\varphi$来表示一个整数. 事实上base-$\varphi$和Fibonacci-base是可以对应的. 于是猜测可以用$a_k$来代替$r^k$. 为了处理出$r^{-k}$, 可以把$i^2$一开始乘上一个较大的$a_m$, 然后贪心做, 从打到小依次减过去, 当然需要保证相邻两项差大于等于$3$. 这个算法的解释可以在论坛中看到, [这个](https://projecteuler.net/thread=558;post=241511)以及[这个](https://projecteuler.net/thread=558;post=241526).

### 方法二
显然可以得到$r^{-1}=r^2-r,r^3=r^2+1,r^4=r^2+r+1$, 于是每个$r^k$其实都可以用$a+br+cr^2$来表示. 然后可以发现$x=a+br+cr^2 < 0$当且仅当它的范数小于$0$. 于是, 我们有了比较两个数大小的手段, 可以算出$a+br+cr^2$的范数是下面这个矩阵的行列式值$$
\left( \begin{array}{ccc}
a & c     & b+c \\
b & a     & c \\
c & b+c & a+b+c \end{array} \right)$$
于是定义出加,减,乘,除, 大小比较等操作符. 就可以贪心地求出需要的项数. 参考论坛里面[这个](https://projecteuler.net/thread=558;post=241406).

### 方法三
参考Golden ratio base, 我们知道如果当前表示不够优的话, 可以用一些规则来使得这个表示变得更优. 首先我们知道$n^2=\sum\limits_{i=1}^{n}2i-1$, 也就是说如果知道了$n^2$的表示, 以及$2n+1$的表示, 直接相加可以得到一个$(n+1)^2$的表示, 而$2n+1$的表示可以由$2n-1$的表示得到.

考虑这几个式子$r^n + r^{n-2} = r^{n+1}, r^n + r^{n-1} = r^{n+1} + r^{n-4}, 2r^n = r^{n+1} + r^{n-2} + r^{n-7}$, 我们可以根据这三个式子来优化一个不是最优的式子. 于是只要知道$1$和$2$的表示, 理论上就可以求出其他所有的表示. $2$的表示为$r^{-7}+r^{-2}+r$.

## 559. Permuted Matrices

我们首先需要知道$P(k,r,n)$的公式, 显然可以考虑用容斥原理. 对于一个$k$, 总共有$\lfloor \frac{n}{k} \rfloor$个数是$k$的倍数, 令$f_i$表示至少有$i$个$k$的倍数的位置是ascent的方案数, 那么就有$P(k,r,n)=\sum\limits_{i=0}^{\lfloor \frac{n}{k} \rfloor}(-1)^{i}f_i$.

考虑如何计算$f_i$, 显然其中有$i$个位置要是ascent, 剩下有$\lfloor \frac{n}{k} \rfloor-i$个位置可以是ascent也可以是decent, 其余位置都必须是ascent. 显然可以发现, 这个被划分成$\lceil \frac{n}{k} \rceil-i$段, 每一个段内部都是递增的. 于是等价于计算$\sum\limits_{a_1+a_2+...+a_l=n}\binom{n}{a_1,a_2,...,a_l}^r$, 其中$l=\lceil \frac{n}{k} \rceil-i$, 注意到$a_1,a_2,...,a_{l-1}$都必须是$k$的倍数.

于是整理下可以得到$$P(k,r,n)=\sum\limits_{\begin{array}{r}a_1+a_2+...+a_m=n \\ k \mid a_1,a_2,..,a_{m-1} \\ a_i \ge 1 \end{array}} (-1)^{\lceil \frac{n}{k} \rceil-m}\binom{n}{a_1,a_2,...,a_l}^r$$

然后这个东西其实可以直接$O(\frac{n^2}{k^2})$来dp, 令$dp(i)$表示计算前$i$个数的答案, 显然$dp(i)=\sum\limits_{0 \le j < i, k \mid i - j}(-1)^{\frac{i-j}{k}}dp(j)\frac{1}{((j-i)!)^r}$. 初始条件为$dp(0)=(n!)^r$. 总的复杂度是$\sum\limits_{k=1}^{n}\frac{n^2}{k^2}=O(n^2)$.

其实这个可以做到更优的复杂度, 令$$f_{k, r}(x) := \sum_{n=1}^{\infty} \frac{x^{kn}}{(kn)!^r},\, g_{r}(x) := \sum_{n=1}^{\infty} \frac{x^n}{n!^r}$$

根据$\sum\limits_{i=0}^\infty (-f_{k, r}(x))^i = \frac{1}{1 + f_{k, r}(x)}$, 可以得到$$P(k, r, n) = (n!)^r \cdot (-1)^{(n-1)/k} \cdot [x^n]\frac{g_{r}(x)}{1 + f_{k, r}(x)}$$

然后就可以用FFT\/NNT做到$O(\frac{n}{k}\log^2 \frac{n}{k})$, 于是总的复杂度是$O(n \log^2 n)$. 如果用了一些多项式求逆的技巧, 应该还可以做到$O(n\log n)$.

## 560. Coprime Nim
打表观察可知如果$n$是偶数那么$sg(n)=0$, 如果$n$是质数或者$1$那么$sg(n)=\pi(n)+1$, 否则$sg(n)=sg(mp(n))$其中$mp(n)$是$n$的最小质因子. 计算出每个$x$在$sg$中出现的次数$cnt(x)$, 然后就是对$cnt$做$k$次异或卷积, 用`fwt`就好了.

## 561. Divisor Pairs
首先可以知道$S((P_m\#)^n)=(\frac{(n+1)(n+2)}{2})^m-(n+1)^m$. 当$n$的形式是$4k$时, $S((P_m\#)^n)=(4k+1)^m((2k+1)^m-1)=2k \cdot (4k+1)^m\cdot ((2k+1)^{m-1}+(2k+1)^{m-2}+\cdots+1)$, 由于$m$是奇数, 只有$2k$会对答案有贡献. 当$n$的形式是$4k-1$时, $S((P_m\#)^n)=(2k)^m((4k+1)^m-(2k)^m)$, 令$p=4k+1$, $q=2k$, 那么$(4k+1)^m-(2k)^m=p^{m-1}+p^{m-2}q+\cdots+q^{m-1}$是奇数, 于是只有$(2k)^m$会对答案有贡献. 当$n$形式为$4k-2$或者$4k-3$时, $S((P_m\#)^n)$是奇数, 不会对答案有任何贡献.

于是, 当$n=4k$时, $E(m,n)=e_2(k)+1$; 当$n=4k-1$时, $E(m,n)=m(e_2(k)+1)$. 其中$e_2(k)$表示$k$的二进制表示中末尾$0$的个数. 于是, $Q(n)=(m+1)\sum\limits_{i=1}^{\frac{n}{4}}e_2(i)$

## 562. Maximal perimeter
首先根据pick定理, 可以知道这个三角形的面积必然是$\frac{1}{2}$. 不妨假设$\vec{AB}=(x_1,y_1),\vec{AC}=(x_2,y_2)$, 那么显然有$x_1y_2-x_2y_1=1$. 也就是说如果知道了$x_2,y_2$, 可以用扩展欧几里得算法求出$(x_1,y_1)$. 考虑到$C$点肯定和圆周非常接近, 于是可以考虑直接暴力枚举$(x_2,y_2)$.

## 563. Robot Welders
可以猜测每个数的最大质因子不会超过$25$, 就是$\{2,3,5,7,11,13,17,19,23\}$. 于是可以dfs生成所有在$10^{17}$以内的数, 暴力枚举约数就好了. 也可以考虑枚举最长边, 显然不会超过$10^8$, 然后根据$1.1$的限制枚举短边, 这个应该会快很多.

## 564. Maximal polygons
假设我们已经知道了多边形的每条边长, 那么面积最大的多边形显然一定是圆的内接多边形(称作[Cyclic Polygon](http://mathworld.wolfram.com/CyclicPolygon.html)). 这个圆可以通过二分计算出来.

于是可以暴力枚举变长和为$50$的所有多边形, 然后计算贡献. 枚举的时候需要按照边长度递增或递减枚举, 边长度集合一样的多边形一起计算就好了.

## 565. Divisibility of sum of divisors
如果$n=\prod p_i^{e_i}$, 那么$\sigma(n)=\prod (1+p_i+p_i^2+...+p_i^{e_i})$. 考虑$2017$是质数, 那么符合条件的$(p_i,e_i)$, 一定满足$2017 \mid (1+p_i+p_i^2+...+p_i^{e_i})$. 当$e_i=1$的时候, 需要枚举$2017$的倍数$2017k$, 判断$2017k-1$是不是质数; 当$e_i > 1$的时候, 显然有$p_i \le \sqrt{10^{11}}$, 暴力枚举即可.

找出这些$(p_i,e_i)$之后, 就可以直接套用容斥原理计算答案了.

## 566. Cake Icing Puzzle

首先如果$c$是平方数, 那么显然直接暴力枚举就好了, 步数不会特别大.

如果$c$不是完全平方数, 步数一定是散的倍数. 首先一直模拟这个过程, 直到不会产生新的小块. 那么接下来的操作一定是现在的一个排列, 并且每个数都有两种状态, 于是可以参考排列的环分解, 我们可以找到一些数, 最后答案是这些数的LCM. 模拟的时候可以用treap维护切得过程.

还有一个比较暴力的方法. 我们可以一开始随机一个初始点$t$, 然后所有操作有只操作这个点$t$, 当$t$回到一开始的初始位置并且状态也是一样的话, 那么我们就找到了一个周期. 多随机一些次数, 就能得到所有的周期. 但是这个方法只能准确求出最后答案特别大的数的周期. 对于其他数, 枚举的时候会有一些其他因子混进来. 考虑到如果$T$是一个周期, 那么$T$的约数也可能是周期, 于是可以在之前找出来的周期的$T$基础上, 枚举$T$的约数, 找到最小的也是周期的约数就好了. 这样就可以排除掉一些无用的因子.

## 567. Reciprocal games I

很容易推出$J_{A}(n)=\frac{1}{2^n}\sum\limits_{k=1}^{n}\frac{1}{k}{n \choose k}$, $J_{B}(n)=\sum\limits_{k=1}^{n}\frac{1}{k{n \choose k}}$. 根据$\binom{n}{k}=\binom{n-1}{k}+\binom{n-1}{k-1}$, 可以得到$J_{A}(n)$的递推式: $J_{A}(n)=\frac{J_{A}(n-1)}{2}+\frac{1}{n}-\frac{1}{n2^n}$.

根据这个[链接](http://math.stackexchange.com/questions/627432/sum-of-reciprocals-of-binomial-coefficients-sum-limits-k-0n-1-dfrac1), 我们可以知道$J_{B}(n)=\frac{1}{2^n}\sum\limits_{k=1}^{n}\frac{2^k}{k}$, 于是$J_{B}(n)=\frac{J_{B}(n-1)}{2}+\frac{1}{n}$

于是就可以直接一遍for算出$S(m)$了.

## 568. Reciprocal games II

根据\#567的公式, 可以知道$D(n)=\frac{H_n}{2^n}$, 于是直接套用$10^{\{\log_{10}{D(n)}\}+7}$就可以算出$7$位有效数字, 其中$\{x\}=x-[x]$, 是$x$的小数部分.

## 569. Prime Mountain Range

直接暴力是可以很快跑出来的, 这里不谈.

可以观察到一个性质, 如果第$m$个山顶可以被第$n$ $(n < m)$个山顶看到, 那么一定存在另一个山顶$j$ $(n < j < m)$能够被$n$看到. 如果于是维护每个山顶能被看到的集合$S(i)$, 对于一个新的山峰$j$, 先检查能不能被$j-1$看到, 递归检查集合$S(j-1)$里面的山峰.

## 570. Snowflakes

经过一些推导, 可以算出$A(n) = 3\cdot4^{n-1} - 2\cdot3^{n-1}$, $B(n)=(4n+26)3^{n-1}+(9n-69)2^{2n-3}$. 然后, 再次推导下可以得到$G(n) = 6 \gcd(2\cdot4^{n-2}-3^{n-2}, 7n+3)$,  显然$7n+3$不大, 直接一次取模之后就可以普通gcd了.

还有另外一个暴力的方法. 不妨一开始令$G(i)=1$, 考虑如果$d \mid G(n)$, 那么其实可以把$G(n)$乘上$d$. 于是可以想到, 可以令$d$是素数或者素数的幂次, 这样就可以算出所有$G$了. 关键是对于一个$p$, 如何找出那些$n$使得$p \mid G(n)$. 显然, $p \mid A(n)$并且$p \mid B(n)$. 注意到满足$p \mid A(n)$的那些$n$肯定构成了等差数列, 满足$p \mid B(n)$的$n$也一定是构成了等差数列. 对于一个$p$, $A(n)$的等差数列可以用BSGS算出来, $B(n)$在$A(n)$上继续扩展就好了. 对于$p^k$, 只要在$p^{k-1}$的基础上扩展就好了.

## 571. Super Pandigital Numbers

$12!$枚举下答案就好了, 足够找到$100$多个解.

## 572. Idempotent matrices

显然这个矩阵的特征值只能是$0$或者$1$, 于是考虑$\mid M - \lambda I\mid = 0$, 可以得到这个多项式$$-c e g+b f g+c d h-a f h-b d i+a e i+(b d-a e+c g+f h-a i-e i) \lambda+(a+e+i) \lambda^2-\lambda^3$$

这个多项式只可能是$-\lambda^3$, $-\lambda^3+\lambda^2$, $-\lambda^3+2\lambda^2-\lambda$或者$-\lambda^3+3\lambda^2-3\lambda+1$, 考虑待定系数法:$$-c e g+b f g+c d h-a f h-b d i+a e i=w, \ b d-a e+c g+f h-a i-e i = v, \ a + e + i=u$$

其中$(u,v,w)$只可能是$(0,0,0)$, $(1,0,0)$, $(2,-1,0)$或者$(3,-3,1)$.

然后根据$M^2=M$, 可以得到以下等式$$\begin{array}{r}cg+hf=i-i^2 \\ cg=a-a^2-bd \\ ch=b-ab-be \\ fg=d-ad-ed \\ fh=e-bd-e^2 \\ (1-a-i)c=bf \\ (1-e-i)f = cd \\ (1-a-i)g=hd \\ (1-e-i)h=bg\end{array}$$

考虑枚举$a,e,b,c$, 那么就可以确定其他值了.

## 573. Unfair race
$E(n)$的分母显然是$n^{n-1}$, 然后去oeis上搜了下分子, 马上就找到[公式](http://oeis.org/A001865)了:$$E(n)=\frac{1}{n^{n-1}}\sum\limits_{k=1}^{n} \frac{n! \cdot n^{n-k-1}}{(n-k)!}=n!\sum\limits_{k=1}^{n}\frac{1}{(n-k)! \cdot n^{k}}.$$

直接暴力递推过去就好了. 公式的[证明](https://projecteuler.net/thread=573;post=257074).

## 574 Verifying Primes
如果$p=A+B$, 那么暴力枚举$A$和$B$, 求出满足条件的最大的$q$, 判断$p < q^2$. 对于$p=A-B$, 可以发现$p$只需要被最小的$q$更新就好了. 于是可以知道$q$最大只要$67$就够了, 然后$67$以内的素数最多只有$19$个. 于是考虑枚举$q$, 然后令$A=ax,B=by$, 其中$\gcd(x,y)=1,\gcd(a,b)=1,ab=\prod\limits_{p < q}p$. 之后枚举$p$, 令$p=ax-by$, 可以用扩展欧几里得解出合法的$(x,y)$.
