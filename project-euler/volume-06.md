# Volume 06

## 251 Cardano Triplets
两边同时立方, 然后化简可以得到$b^2c = \frac{(a + 1)^2 (8a - 1)}{27}$, 令$a=3x+2$, 那么有$b^2c=(x+1)^2(8x+5)$. 于是可以想到一个暴力的方法: 枚举$x$, 然后对$(x+1)^2(8x+5)$分解质因数, 这样就可以得到所有的$(b,c)$了. 这样比较慢, 大概需要$10$几分钟吧.

令$g=\gcd(b,x+1)$, 那么$b=gp,x+1=gq, \gcd(p, q)=1$, 于是式子可以化简为$p^2c=q^2(8x+5)$, 由于$\gcd(p, q)=1$, 那么$8x+5$可以表示为$rp^2$, 于是进一步化简得到$a=3gq-1,b=gp,c=q^2r$, 其中$\gcd(p, q)=1, 8gp=rp^2+3$.

于是就可以考虑枚举$g,p,q,r > 0$使得$\gcd(p, q)=1, 8gp=rq^2+3$并且$3gq+gp+q^2r+1 \le 10^{8}$. 不妨枚举$p,q$(显然$q$是奇数, $p$是偶数), 如果找到了$(g,r)$的一组最小解$(g_0,r_0)$, 那么其他解要满足$g=g_0+q^2k,r=r_0+8pk$. 于是只要找到符合条件的$k$就好了. 由于$rp^2=8x+5,c=q^2r$, 显然$p,q$都是$O(\sqrt{10^8})$, 可以直接暴力枚举, $(g_0,r_0)$可以用扩展欧几里得算法求. 这样大概能在$10$s内出解.

## 252 Convex Holes
这个就是最大空凸包. 枚举所有最大空凸包的最低最左点. 对于每个枚举到的点$v$, 先将$v$上方的点按照极角排好序. 令$dp(i,j)$表示满足下面条件的最大凸包: 在凸包上$v$顺时针过来的第一个点是$i$, 并且$i$顺时针过来第一个点$k$不在$i\to j$的左手域, $k$可以等于$j$. 这样复杂度可以做到$O(n^3)$.

## 253 Tidying up
考虑加完点后, 每个联通分量的大小, 显然只需要考虑这些大小构成的`multiset`就好了. 于是就可以用这个作为状态进行dp, 同时记录当前的联通块数目, 实际上还需要加入最左边和最右边两个联通分量的大小.

## 254 Sums of Digit Factorials
注意到$sf(n)=i$, 如果$i < 63$, 显然$n \le 9999999$就足够表示了, 于是这部分可以直接暴力. 那么当$i \ge 63$的时候, 可以证明, $f(n)$一定是$x999...$这种形式, 其中$x=n \text{ mod } 9$, $9$的个数为$\lfloor \frac{n}{9} \rfloor$. 那么, 现在问题是知道了$f(n)$的值, 如何快速求出最小的$n$. 这个只要用阶乘进制来表示$f(n)$就好了, 先用$9!$, 然后$8!,7!,\cdots,1!$, 直接贪心即可.

## 255 Rounded Square Roots
可以猜测到, 显然可以把$[10^{13},10^{14})$划分成若干个小区间$[l_i,r_i]$, 小区间内每个数需要的次数是一样的.

根据$\lfloor \frac{a+\lceil \frac{n}{a} \rceil}{2} \rfloor=b$, 可以得到$a + \lceil \frac{n}{a} \rceil \in [2b, 2b+1] \Rightarrow \lceil \frac{n}{a} \rceil \in [2b-a,2b-a+1]$, 于是可以得到$n$的范围是$n \in [a(2b-a-1)+1,a(2b-a+1)]$.

根据上面的式子, 对区间进行分治就好了.

## 256 Tatami-Free Rooms
可以在oeis上搜到Tatami-Free Tiling的方案数是[A068920](http://oeis.org/A068920), 上面给出了一个[链接](http://oeis.org/A068920/a068920.txt), 从这个链接里可以获得如何快速计算$a \times b$是不是Tatami-Free. 于是暴力枚举每个数, 然后枚举约数判断就好了. 一个优化是这个数约数个数要至少是$400$个, 通过线性筛预处理, 可以少枚举很多.

[Counting Fixed-Height Tatami Tilings](http://webhome.cs.uvic.ca/~ruskey/Publications/Tatami/TatamiDraftSubmitted.pdf)这篇paper似乎提供了一些更加有趣的性质, 有空可以研究下.

## 257 Angular Bisectors
根据角平分线定理, 可以得出$\frac{\text{area}(ABC)}{\text{area}(AEG)}=\frac{(a+c)(a+b)}{bc}, a \le b \le c$. 显然可以得出$\frac{(a+c)(a+b)}{bc} = k \in \{2, 3, 4\}$.

当$k=4$的时候, 显然$a=b=c=k$, 答案为$\lfloor \frac{n}{3} \rfloor$.

当$k=2$的时候, 可以算出$(a,b,c)=k(uv,v^2+uv,2u^2+uv)$, 其中$\gcd(u,v)=1, u < v < 2u, v \text{ mod } 2 = 1$.

当$k=3$的时候, 分成两种情况:

1. $(a,b,c)=k(uv,\frac{v^2+uv}{2},\frac{3u^2+uv}{2})$, 其中$\gcd(u,v)=1, u < v < 3u, u \equiv v \equiv 1 \text{ mod } 2, v \text{ mod } 3 \ne 0$.

2. $(a,b,c)=k(2uv,v^2+uv,3u^2+uv)$, 其中$\gcd(u,v)=1, u < v < 3u, u \text{ mod } 2 \ne v \text{ mod } 2,  v \text{ mod } 3 \ne 0$.

于是用Stern-Brocot Tree枚举互质的$(u,v)$即可.

## 258 A lagged Fibonacci sequence
直接套用$O(m^2\log n)$的线性递推即可. 原理解释[Cayley–Hamilton theorem](https://en.wikipedia.org/wiki/Cayley%E2%80%93Hamilton_theorem).

## 259 Reachable Numbers
就是一个爆搜. 令$dp(i,j)$表示只用$i$到$j$这些数字能构成的结果集合. 枚举中间的分界点$k$, 暴力合并$dp(i,k)$和$dp(k,j)$即可.

## 260 Stone Game
直接暴力dp就可以过掉这个题了, 令$dp(x,y,z)$表示这个状态是否必胜, 然后枚举$7$种转移, 暴力转移. 结果用`bitset`存就可以存下了.

## 261 Pivotal Square Sums
化简下式子可以得到$m(2n+m+1)^2-(m+1)(2k-m)=m(m+1)$, 令$x=m(2n+m+1),y=2k-m$, 于是有$x^2-m(m+1)y^2=m^2(m+1)$, 这个是一个`pell`方程, 只要找出了所有的基础解, 就可以用递推式$(x,y)\to ((2m+1)x+2m(m+1)y,2x+(2m+1)y)$了.

求基础解没有找到什么好方法, 只能暴力. 考虑$m \mid x$, 那么稍微化简下可以得到$m \mid y^2$, 也就是说$h(m) \mid y$, 其中$h(m)=\max\{d | d \mid m, d \le \sqrt{m}\}$. 于是可以根据这个暴力枚举$y$, 然后检查$x$是否存在就可以找出所有的基础解.

## 262 Mountain Range
显然, 这个函数是关于平面$x=y$对称的. 然后用[Mathematica](https://www.wolframalpha.com/input/?i=Plot%5B%5B5000-0.005%5Bx%5E2%2By%5E2%2Bxy%5D%2B12.5%5Bx%2By%5D%5D%2Fe%5Eabs%5B0.000001%5Bx%5E2%2By%5E2%5D-0.0015%5Bx%2By%5D%2B0.7%5D,%7Bx,0,1600%7D,%7By,0,1600%7D%5D)画出这个函数的图像, 可以发现在$x=0$和$x=1600$两个平面处是瓶颈, 通过二分或者三分可以求出这两个最高点是$(0, 895.483409898745, 10396.4621933)$和$(1600, 666.56468, 9571.5395)$, 于是$f_{\text{min}}=10396.4621932841041097408663$.

再次使用[Mathematica](https://www.wolframalpha.com/input/?i=Plot%5B%5B5000-0.005%5Bx%5E2%2By%5E2%2Bxy%5D%2B12.5%5Bx%2By%5D%5D%2Fe%5E%5B0.000001%5Bx%5E2%2By%5E2%5D-0.0015%5Bx%2By%5D%2B0.7%5D%3D10396.4621932841041097408663,%7Bx,0,1600%7D,%7By,0,1600%7D%5D)画图, 可以观察到, 最短距离显然是从$A$到达曲线的某个点$P$, 然后从$P$沿着曲线到达点$Q$, 最后从$Q$直接到$B$, 其中$AP$和$BQ$是两条切线. 通过二分可以求出这两个切点分别是$P=(624.6518830602000, 48.2528759250369), Q=(1536.0420725402400, 873.0401231174810)$.

直线距离直接计算就好了, 剩下来的曲线部分可以考虑定步长simpson, 枚举$x$, 用二分确定出$y$, 算下相邻两部之间的距离, 求个和就好了.

## 263 An engineers' dream come true
首先可以从wiki找到如何判定[Practical number](https://en.wikipedia.org/wiki/Practical_number): 令$n=p_1^{\alpha_1}p_2^{\alpha_2}...p_k^{\alpha_k}$ $(p_1 < p_2 < \cdots < p_k)$, 那么$n$是practical number当且仅当, 对于所有$2 \le i \le k$都有, $p_{i}\leq 1+\sigma (p_{1}^{\alpha _{1}}p_{2}^{\alpha _{2}}\cdots p_{i-1}^{\alpha _{i-1}})=1+\prod\limits_{j=1}^{i-1}{\frac {p_{j}^{\alpha _{j}+1}-1}{p_{j}-1}}$, 并且$n$是偶数, 也就是$p_1=2$.

暴力显然比较慢, 考虑利用整除性分析$n$的性质.

1. 由于$n-3$是素数, 那么$n$显然不能是$3$的倍数, 不妨令$n=3m+1$. 那么$n-4,n+8$是$3$的倍数, $n-8,n,n+4$不是$3$的倍数. 如果$n=3m+2$, 那么$n-4,n+8$不是$3$的倍数, $n-8,n,n+4$是$3$的倍数.

2. 由于$n$是practical number, 于是$n$要是$4$的倍数, $n-8, n-4, n+4, n+8$也是$4$的倍数.

3. 由于$n-9,n-3,n+3,n+9$都是素数, 那么$n$一定是$5$的倍数. $n-8, n-4, n+4, n+8$不是$5$的倍数.

4. 同样由于$n-9,n-3,n+3,n+9$都是素数, $n$一定是模$7$余$0,1$或者$6$.

5. 由于$n+4$是practical number, 那么$n+4$要是$8$的倍数, 于是$n=8m+4$. 然后由于$n-8$是practical number, 那么$n-8$要是$7$的倍数. 所以可以得到$n=7m+1$.

综上可以知道$n=840m+820$或者$n=840m+20$. 于是暴力枚举$m$, 检查$n$是不是practical number以及素数就好了.

## 264 Triangle Centres
不妨令三个顶点坐标是$(x_1,y_1),(x_2,y_2),(x_3,y_3)$, 那么可以知道$x_1 + x_2 + x_3 = 5, y_1 + y_2 + y_3 = 0$. 然后由于这三个点都在圆周上, 有$x_1^2 + y_1^2 = x_2^2 + y_2^2 = x_3^2 + y_3^2$. 消去$y_2,x_3,y_3$, 可以得到下面这个方程: $$
4((x_1-5)^2+y_1^2)x_2^2 + 4(x_1-5)((x_1-5)^2+y_1^2)x_2 + (x_1-5)^4-2(x_1^2+10x_1-25)y_1^2-3y_1^4=0$$

考虑枚举$x_1,y_1$, 可以直接解出$x_2$, 然后其他数也可以解出来了, 直接判断合法性就好了.

## 265 Binary Circles
直接爆搜每个位置是0还是1, 然后开个数组记录每个被访问数即可.

## 266 Pseudo Square Root
$190$以内的素数只有$42$个, 考虑折半枚举, 分别枚举每个素数乘还是不乘, 把结果取对数后用`double`存储. 然后排序后, 用双指针或者二分都可以.

## 267 Billionaire
猜测了下这个概率是可以三分的. 假设有$n$次硬币向上, 那么收益是$(1+2*f)^n(1-f)^{1000-n}$, 也就是要$(1+2*f)^n(1-f)^{1000-n} \ge 10^9$, 取对数得到$n \ge \frac{9\ln(10) - 1000\ln(1 - f)}{\ln(1 + 2f) - \ln(1 - f)}$. 显然要使概率最大, 只要使$n$最小即可, 于是根据$\frac{9\ln(10) - 1000\ln(1 - f)}{\ln(1 + 2f) - \ln(1 - f)}$进行三分即可.

## 268 Counting numbers with at least four distinct prime factors less than
首先可以容斥计算出至少被$100$以内一个质数整除的个数. 然后减去只被$1$,$2$, $3$个整除的个数即可. 这些同样可以枚举质数, 然后进行容斥, 可是这样跑的很慢呢. 考虑如何才能同时进行容斥. 只要算出系数, 就可以只用一边容斥就好了. 于是可以先通过一次dfs算出每一个容斥项的系数, 然后再容斥计算既可.

## 269 Polynomials with at least one integer root
根据[Rational root theorem](https://en.wikipedia.org/wiki/Rational_root_theorem), 可以知道根一定是$P_n(0)$的约数. 如果每个多项式只有一个整数根, 那么就直接计算就好了. 如果有多个可以考虑用容斥原理来计算.

对于给定的一些根, 如何快速计算多项式数目呢? 第一种方法是考虑折半枚举, 分成前后各$8$位, $O(10^8 \log 10^8)$的复杂度还是可以接受的, 大概几分钟就计算出来了. 另一种方法是考虑dp. 不妨假设只有一个根$r$, 那么$P(x)$可以表示为$P(x)=(x-r)Q(x)$, 算出合法的$Q(x)$数目, 那么$P(x)$的数目也是知道的. 那么只要枚举$Q(x)$的系数, 用多项式乘法计算出$P(x)$的系数就好了. 计算过程中要求$P(x)$的系数一直小于$10$, 这个就可以数位dp做了. 有多个根的话, 在dp数组上多开几个维度就好了.

## 270 Cutting Squares
和普通的凸包三角剖分计数一样, 直接固定一条边, 然后枚举另一个三角顶点的位置就好了. 当割出一条斜边之后, 那么就可以直接拿这条斜边当固定的边, 计算会方便很多.

## 271 Modular Cubes, part 1
分解后可以知道$13082761331670030=2\cdot 3 \cdot 5 \cdot 7 \cdot 11 \cdot 13 \cdot 17 \cdot 19 \cdot 23 \cdot 29 \cdot 31 \cdot 37 \cdot 41 \cdot 43$. 考虑$x^3 \equiv 1 \text{ mod } p$的解, 我们可以找出一些只有唯一解的那些$p$, 有$\{2, 3, 5, 11, 17, 23, 41\}$, 显然可行的$x$需要满足$x=5290230k$, 于是暴力枚举$k$即可.

## 272 Modular Cubes, part 2
如果把$x=1$算进去, 那么$C(n)$其实是一个积性函数, 令$n=\prod p_i^{e_i}$, 那么$C(n)=\prod C(p_i^{e_i})$. 根据[Cubic reciprocity](http://en.wikipedia.org/wiki/Cubic_reciprocity)的一些性质, 可以知道$C(p^k)=3, p \equiv 1 \text{ mod } 3$, $C(3^k)=3, k \ge 2$, 其余素数幂次都是$C(p^k)=1$.

考虑到$242=3^5-1$, 我们需要$5$个满足$C(p^k)=3$的素数. 最小的$4$个满足$C(p^k)=3$的素数是$\{9,7,13, 19\}$, 算了一下其他素数的上限是$\frac{10^{11}}{15561}=6426322$. 于是找出$6426322$以内的素数, 进行爆搜就好了(加一些可行性剪枝后跑的飞快).

## 273 Sum of Squares
首先处理出每个素数$p=a^2+b^2$, 显然这个是唯一分解的. 然后考虑用$(a^2+b^2)(c^2+d^2)=(ac-bd)^2+(ad+bc)^2=(ac+bd)^2+(ad-bc)^2$来合并就好了. 由于$150$以内满足条件的素数不太多, 直接暴力合并就好了. 如果素数变得更多, 可以考虑用折半枚举的方法来合并.

## 274 Divisibility Multipliers
答案就是$\sum\limits_{p < 10^7} \text{inv}(10, p)$, 其中$inv(x,m)$表示$x$模$m$的逆元.

## 275 Balanced Sculptures
直接爆搜, 然后判断合法性. 可以用[Redelmeier method](http://en.wikipedia.org/wiki/Polyomino#Algorithms_for_enumeration_of_fixed_polyominoes)来枚举polyominoes. 就是维护$3$个集合$P,C,F$, 分别表示polyomino里面的点, 候选点集, 以及不能被选上的点. 每次从$C$中取出一个点, 可以扩展到$P$或者$F$中, 这样就可以不重不漏地枚举了.

## 276 Primitive Triangles
令$f(n)$表示周长为$n$的整数边长三角形数目, 这个可以在[oeis](https://oeis.org/A005044)上找到公式. 令$g(n)$是互素的那些三角形个数, 那么显然有$f(n)=\sum\limits_{d=1}^{n}g(\lfloor \frac{n}{d} \rfloor)$, 移个项得到$g(n)=f(n)-\sum\limits_{d=2}^{n}g(\lfloor \frac{n}{d} \rfloor)$, 递归计算即可.

## 277 A Modified Collatz sequence
令$a_1=x$, 那么显然$a_n$可以表示为$\frac{ux+v}{w}=y$, 也就是$ux+v=wy$, 显然$u,v,w$可以通过序列递推得到, 于是只要用扩展欧几里得解一个不定方程就好了.

## 278 Linear Combinations of Semiprimes
就是要求[Frobenius number](https://en.wikipedia.org/wiki/Coin_problem), 对于$2$个数$g(a_1,a_1)=a_{1}a_{2}-a_1-a_2$; 对于$3$个数, $g(a,b,c)=\text{lcm}(a,c)+\text{lcm}(b,c)-a-b-c$, 如果$c \mid \text{lcm}(a,b), \gcd(a,b,c)=1$.

题目中的数恰好满足条件, 于是$f(pq,pr,qr)=2pqr-pq-pr-qr$.

## 279 Triangles with integral sides and an integral angle
那个角度只可能是$60^{\circ}$, $90^{\circ}$和$120^{\circ}$, 于是用之前题目的结论就好了.

## 280 Ant and seeds
马尔科夫链的一些知识. 令$M$是概率转移矩阵, 其中第一行是吸收态(结束节点). 令$A=I-M$, 那么$A^{-1}$的第一行和就是答案. 矩阵很大$10265 \times 10265$, 不好直接求逆. 考虑$b$是一个全$1$的列向量, 令$A^{-1}b=X$, 那么$X_0$就是我们要求的答案. 上面式子两边同乘以$A$, 得到$AX=b$. 于是只要解个方程组就好了. 可以考虑用[稳定双共轭梯度法](https://en.wikipedia.org/wiki/Biconjugate_gradient_stabilized_method)进行迭代.

## 281 Pizza Toppings
可以得到公式$f(n,m)=\frac{1}{mn}\sum\limits_{d \mid n}\frac{(dm)!\phi(\frac{n}{d})}{(d!)^m}$, 当$n=1$的时候需要特判下$f(1,m)=(m-1)!$. 于是暴力枚举$n,m$即可. 公式推导, 参考[Necklaces with Fixed Density](http://theory.cs.uvic.ca/inf/neck/NecklaceInfo.html).

## 282 The Ackermann function
当$n=0,1,2,4$的时候可以直接快速幂算出答案, $n=5,6$时答案显然是一样的, 考虑用$A^B \equiv A^{B \text{ mod } \phi(m) + \phi(m)} \text{ mod } m$来加速.

## 283 Integer sided triangles for which the area/perimeter ratio is integral
实现这篇paper [Heronian Triangles Whose Areas Are Integer Multiples of Their Perimeters](http://forumgeom.fau.edu/FG2007volume7/FG200718.pdf)的算法就好了.

## 284 Steady Squares
参考这个[Automorphic number](https://en.wikipedia.org/wiki/Automorphic_number)会得到这个题的做法.

每个长度都最多只有$2$个符合条件的数, 其中一个解满足$r(1)=7, r(n+1) \equiv r(n)^2 \text{ mod }n^{14}$, 另一个解满足$r(1)=8, r(n+1) \equiv r(n)^7\text{ mod } n^{14}$. 并且, 除了个位(和为$15$), 其他每一个位上数字之和都是$13$.

## 285 Pythagorean odds
显然有$k - 0.5 < (ka+1)^2+(kb+1)^2 < k + 0.5$, 化简之后可以得到合法的$(a,b)$就是两个圆环在第一象限的面积, 直接计算就好了.

## 286 Scoring probabilities
显然$q$是可以二分的, 于是只要二分答案, 然后通过dp计算出概率就好了.

## 287 Quadtree encoding (a simple compression algorithm)
维护正方形$4$个顶点的颜色, 颜色相同可以直接返回, 否则分成4份递归计算.

## 288 An enormous factorial
直接根据阶乘的中质因子$p$个数的公式计算就好了.

## 289 Eulerian Cycles

1 0 3 2 5 4 7 6
1 0 3 2 7 6 5 4
1 0 5 4 3 2 7 6
1 0 7 4 3 6 5 2
1 0 7 6 5 4 3 2
3 2 1 0 5 4 7 6
3 2 1 0 7 6 5 4
5 2 1 4 3 0 7 6
5 4 3 2 1 0 7 6
7 2 1 4 3 6 5 0
7 2 1 6 5 4 3 0
7 4 3 2 1 6 5 0
7 6 3 2 5 4 1 0
7 6 5 4 3 2 1 0


## 290 Digital Signature
直接数位dp就好了, 令$f(i,carry,sum)$表示搞到了第$i$位, 后面的进位是$carry$, $n$的数字和减去$137n$的数字和是$sum$的方案数, 直接枚举当前位的数, 然后转移即可.

## 291 Panaitopol Primes
$p$的形式是$n^2+(n+1)^2$, 枚举$n$, 测试是不是素数就好了. 证明如下:

令$d = \gcd(x,y)$, 那么$x = dx^\prime, y = dy^\prime$. 于是$p(x^3 + y^3) = (x^4 - y^4)$变成$p(x^{\prime 2} - x^{\prime} y^{\prime} + y^{\prime 2}) = d(x^\prime - y^\prime)(x^{\prime 2} + y^{\prime 2})$

由于$x^{\prime 2} - x^{\prime} y^{\prime} + y^{\prime 2}$和$(x^\prime - y^\prime)(x^{\prime 2} + y^{\prime 2})$互质, $p = (x^\prime - y^\prime)(x^{\prime 2} + y^{\prime 2})$, $d = x^{\prime 2} - x^{\prime} y^{\prime} + y^{\prime 2}$. 于是只有当$x^\prime - y^\prime = 1$时$p$才可能是质数.

## 292 Pythagorean Polygons
首先枚举所有的三元组$(x,y,d)$满足$x^2+y^2=d^2, d \le n$, 那么这些三元组可能构成凸包上的边. 考虑把这些边按照逆时针顺序排序(按照向量$(x,y)$的方向). 那么凸包上的边一定是按照顺序取出若干条向量依次拼接而成的, 于是就可以考虑用dp来计算.

令$f(i,x,y,d)$表示用了前$i$条线段, 从$(0,0)$出发, 当前到了$(x,y)$, 且现在边长和为$d$. 转移的话就是枚举下一条选哪条线段, 注意为了能够组成凸包, 方向相同的线段需要一起处理. 最后答案就是$\sum\limits_{i=1}^{n}f(m,0,0,i)$, 其中$m$表示总共有$m$条线段. 记得还要减去只有两条边的凸包.

## 293 Pseudo-Fortunate Numbers
暴力枚举所有的`admissible number`, 然后暴力枚举$m$即可. $m$的个数不是很多.

## 294 Sum of digits - experience #23
列出转移矩阵, 做矩阵快速幂即可.

## 295 Lenticular holes
考虑枚举两个交点构成的格点矩形的大小为$a \times b$ $(b <= a)$, 显然$\gcd(a,b)=1$. 考虑对角线的方程是$ay+bx=ab$, 那么圆心显然在直线$ax-by=\frac{a^2-b^2}{2}$上, 于是可以知道$a$和$b$都是奇数. 接下来用扩展欧几里得算法可以求出合法的整点$(x,y)$, 也就是圆心的位置. 由于内部不能有整点, 也就是说距离直线$ay+bx=ab$最近的整点$(p_x,p_y)$不能在圆内, 这样就可以求出一系列合法的半径.

对于一条直线, 我们可以算出总的贡献, 但是这样是有重复的, 有些半径会在多个直线上出现. 通过简单的测试发现, 一个半径最多只会在$8$条直线上出现, 于是考虑用容斥原理减去重复计算的答案.

## 296 Angular Bisector and Tangent
简单的推导可以知道$CE=\frac{ac}{a+b}$. 令$a=gx,b=gy$, 其中$\gcd(x,y)=1$, 那么有$CE=\frac{cx}{x+y}$, 显然$c$要是$x+y$的倍数, 令$c=k(x+y)$. 于是暴力枚举每个$(x,y)$, 根据$a \le b \le c$和$a+b > c$可以列出一个关于$k$和$g$的线性规划方程组, 求出区域, 然后计算整点个数就好了.

## 297 Zeckendorf Representation
找个[规律](http://oeis.org/A007895)可以发现很明显的递归结构.

## 298 Selective Amnesia
考虑Robin的策略, 其实就是一个队列, 一直加在队尾, 长度超过$5$后从队首拿掉. 于是所有数都以Robin的数为基准进行重标号. 使得Robin的数一直是$\{1,2,...\}$. Larry那边, 如果有和Robin一样的数, 就按照Robin的标号, 否则新增一个新的标号. 例如: Robin是$\{1,6,7,8,9\}$, Larry是$\{9,8,7,4,3\}$, 那么可以重新标号为$\{1,2,3,4,5\}$和$\{5,4,3,6,7\}$.

算了下这样的状态只有$400$多个, 于是用map存状态进行dp就好了.

## 299 Three similar triangles
可以分成$2$种情况.

1. $AC \nparallel BD$

显然$P$是三条角平分线的交点, 令$P=(x,x)$, 于是有$P$到$BD$的距离恰好是$x$, $x = \frac{|dx + bx - bd|}{\sqrt{b^2 + d^2}}$, 得到$x^2(b^2+d^2) = (dx+bx-bd)^2$, 枚举$b^2+d^2=c^2$就好了.

2. $AC \parallel BD$

可以知道$(b-a)(d-a) = 2a^2$, 枚举$a$, 然后质因数分解就好了.

## 300 Protein folding
枚举每一个长度为$15$的字符串, 然后开始爆搜. 一些优化方法:

1. 第一步一定往上走,第二步一定往左或者往上走.
2. 卡住走的范围, 一开始我卡只能走$5 \times 5$的矩形, 但是比答案少了$4$, 后来卡了$6 \times 6$就好了.
3. 显然没必要每个字符串都搜, 一个串的reverse和这个串的答案是一样的.

还有一些可行性剪枝可以加, 但是上面的应该已经足够在合理的时间跑出答案了.

还有一种方法. 首先暴力生成所有的折叠方式, 除去旋转/翻转同构的话, 这个总共有$12495$. 然后就直接暴力枚举每个串, 填上去就好了. 复杂度是$2^{15} \times 12495$, 应该能够比上面的爆搜更快.
