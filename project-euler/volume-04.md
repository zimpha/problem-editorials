# Volume 04

## 151. Paper sheets of standard sizes: an expected-value problem
用5元组$(a_1,a_2,a_3,a_4,a_5)$分别表示各种大小的纸片的数目作为状态进行dp就好了.

## 152. Writing $1/2$ as a sum of inverse squares
对于一个奇素数$p$, 如果某些数是他的倍数, 那么这些数加起来之后的最简分数的分母一定不是$p$的倍数, 否则永远不可能凑出$1/2$. 经过测试发现, 只有$2,3,5,7,13$这些素数是有用的, 其中如果要用$13$, 那么$39$和$52$也要必选. 分为选不选$13$进行爆搜就好了.

## 153. Investigating Gaussian Integers
可以观察到, 如果$(a^2+b^2) \mid n \cdot gcd(a,b)$, 那么$a+bi$就是$n$的约数.

考虑枚举$gcd(a,b)=1$的那些数$a+bi$, 那么$ka+kbi$是$n$的约数, 当且仅当$k(a^2+b^2) \mid n$.

令$f(n)=\sum\limits_{d|n}{d}$, $g(n)=\sum\limits_{1 \le a, b \le n,  a^2+b^2=n}2a[(a,b)=1]$, 那么题目中的$s(n)=\sum\limits_{d|n}g(d)f(n/d)$. 显然$f(n)$和$g(n)$可以$O(n\log n)$求出来的, 那么$\sum s(n)$也就出来了.

## 154. Exploring Pascal's pyramid
那个式子展开之后, 其中$x^ay^bz^c, a+b+c=n$前面的系数是$\binom{n}{a,b,c}$, 暴力枚举下$a$和$b$即可.

## 155. Counting Capacitor Circuits
令$S(n)$为用了恰好$n$个等容量电容能构成的集合, $S(n)$可以用十分暴力的方法递推出来, 然后$D(n)=\mid \bigcap S(i) \mid$. 似乎也可以算出前10项, 然后去[oeis](https://oeis.org/A051389)上找答案.

## 156. Counting Digits

可以观察到如果$n$是答案, 那么$n+1$也很可能是一个答案. 可以猜想, 当$n-f(n,d)$比较大的时候, 下一个合法的$n^\prime$也比$n$大许多. 于是可以根据$n-f(n,d)$的大小调整step的值, 进行暴力枚举. 计算$f(n,d)$是很经典的数位dp, 这里不表.

讨论帖里面说$step$的值大约为$\frac{|n-c|}{log_{10}n}$, 稍微比这个小一点应该就好了.

## 157. Solving the diophantine equation $1/a+1/b= p/10^n$
令$a=kx,b=ky,(x,y)=1$, 那么上式可以化简成$(x+y)10^n=pkxy$.

考虑到$(x,y)=1$, 可以得到$xy|10^n$, 如果已知$x,y$, 那么满足上式的$k,p$数目就是$\sigma_0(\frac{(x+y)10^n}{xy})$. 暴力枚举$x,y$, 对$\frac{(x+y)10^n}{xy}$分解质因数.

## 158. Exploring strings for which only one character comes lexicographically after its neighbour to the left
对于某个$n$, 答案就是$\mathrm{Eulerian}(n, 2)=2^n-n-1$, 于是答案就是$\sum\limits_{n=1}^{26}\binom{26}{n}(2^n-n-1)$.

## 159. Digital root sums of factorisations
这个显然可以递推出来, $mdrs(n)=\max\limits_{d|n,d < n}\{mdrs(n/d)+\text{digital-root}(d)\}$, 复杂度$O(n\log n)$.

论坛里面提供了一个直接计算$mdrs(n)$的方法, 伪代码如下:
```python
def mdrs(n):
  prime_list = factorize(n)
  tuple = [0] * 9
  for p in prime_list:
    tuple[digital_root(p)] += 1
  res = 0
  while tuple[2] > 0 and tuple[4] > 0:
    tuple[2] -= 1
    tuple[4] -= 1
    res += 8
  while tuple[2] > 2:
    tuple[2] -= 3
    res += 8
  while tuple[3] > 1:
    tuple[3] -= 2
    res += 9
  while tuple[2] > 0 and tuple[3] > 0:
    tuple[2] -= 1
    tuple[3] -= 1
    res += 6
  for i in xrange(9):
    res += i * tuple[i]
  return res
```

## 160. Factorial trailing digits
$n!$末尾$0$的个数$d_{10}(n)$可以用这个公式求出来. 令$d_p(n)=\frac{n}{p}+\frac{n}{p^2}+...$, 那么$d_{10}(n)=\min(d_5(n),d_2(n))=d_5(n)$. 不妨考虑中国剩余定理, 分别求出$\frac{n!}{10^{d_{10}(n)}} \text{ mod }5^5$和$\frac{n!}{10^{d_{10}(n)}} \text{ mod } 2^5$. 由于后面这个值肯定是$0$, 可以只考虑前面的.

考虑把$n!$写成$n! \equiv a\cdot 5^b \text{ mod } 5^5$这种形式, 其中$1 \le a < 5^5$. 令$n=5q+r$, 那么$n!\equiv 5^qq!A_5(n) \text{ mod } 5^5$, 其中$A_5(n)=\prod\limits_{x < n, x \nmid 5}x$, $q!$也可以递归下去, 于是$b=d_5(n),a=A(n)A(n/5)A(n/25)...$, 注意到$x^2 \equiv 1 \text{ mod } 5^5$只有$x=\pm 1$这两个解, 于是$A(n) \equiv (-1)^{n/5}A(n \text{ mod } 5^5) \text{ mod } 5^5$.

考虑$\frac{n! \text{ mod } 5^{d_5(n)+5}}{5^{d_5(n)}}=\frac{n!}{5^{d_5(n)}}\text{ mod } 5^5$, 于是$\frac{n!}{10^{d_5(n)}}\equiv 2^{-d_5(n)}5^{d_5(n)}A(n)A(n/5)A(n/25)... \text{ mod } 5^5$. 求出来后中国剩余定理合并一下就好了.

## 161. Triominoes
状态压缩dp就好了.

## 162. Hexadecimal numbers
随便dp下就好了.

## 163. Cross-hatched triangles
利用前两项去[oeis](http://oeis.org/A210687)上可以找到公式$T(n)=\frac{1678n^33 + 3117n^2 + 88n - 345\text{Mod}(n, 2) - 320\text{Mod}(n, 3) - 90\text{Mod}(n, 4) - 288\text{Mod}(n^3 - n^2 + n, 5)}{240}$, 其中$\text{Mod}(n,m)=n \text{ mod } m$.

## 164. Numbers for which no three consecutive digits have a sum greater than a given value
随便数位dp下就好了.

## 165. Intersections
线段求出交点, 放到`set`里面搞一搞就好了.

## 166. Criss Cross
考虑这$16$个数分别是$a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p$, 可以列出若干个方程, 最后消元之后发现只有$8$个是有用的, 于是显然只要确定了$8$个数, 剩下$8$个数就确定了.

不妨枚举$a,b,c,d,e,g,i,k$, 令$s=a+b+c+d$, 那么
$$\begin{aligned}
m &=s-a-e-i \\ o &=s-c-g-k \\ j &=s-d-g-m \\ l &=s-i-j-k
\end{aligned}$$
还有$f,h,n,p$没有确定, 再枚举下$f$, 那么
$$\begin{aligned}
h &=s-e-f-g \\ n &=s-b-f-j \\ p &=s-m-n-o \end{aligned}
$$
这样$16$个数都确定了, 剩下只要检查$s=d+h+l+p$和$s=a+f+k+p$是否都成立即可, 其他等式都已经满足了.


## 167. Investigating Ulam sequences

可以证明, $U(2, 2n+1)$的差分序列最终会变成一个有周期的. 然后[观察](https://en.wikipedia.org/wiki/Ulam_number)可以知道, $U(2, 2n+1)$这个序列恰好只有$2$个偶数(一个是$2$, 另一个不妨设为$e$), 于是在这两个偶数之后, 其他数肯定由偶数+奇数得到的, 也就是说重复的和最多只有2个.

于是, 就可以用优先队列维护所有候选的可能在$U(2, 2n+1)$的数, 每次新加入一个数$x$到$U(2, 2n+1)$, 那么在优先队列中新插入两个数$x+2$和$x+e$, 这样就可以很快得到$U(2, 2n+1)$.

然后处理出差分序列, 用`kmp`找周期就好了, 最长的周期有$2\times 10^6$那么大, 尽量搞出比较多的项数再求周期比较好.

论坛里面有人指出$U(2, 2n+1)$的差分序列的周期长度是$2^{2n+1}$差不多. 这篇[paper](http://projecteuclid.org/download/pdf_1/euclid.em/1048709116)里面证明了这些东西. 似乎还存在$O(v2^{v/2})$的算法可以求出$U(2,v)$差分序列的周期.

## 168. Number Rotations
设这个数有$n+1$位, 那么这个数可以表示为$10S+d$, 旋转后这个数为$d10^{n}+S$, 令$d10^{n}+S=k(10S+d)$, 化简下得到$d(10^n-1)=(10k-1)S$, 可以发现$d,k$都是个位数, 于是暴力枚举$n,d,k$就好了.

## 169. Exploring the number of different ways a number can be expressed as a sum of powers of $2$
找出前几项, 可以到[oeis](http://oeis.org/A002487)上找到公式, $f(2k)=f(k)+f(k-1),f(2k+1)=f(k)$

## 170. Find the largest $0$ to $9$ pandigital that can be formed by concatenating products
这个数一定是$98$开头, 于是只需要$8!$枚举后面部分, 之后$2^9$枚举划分, 求出划分后的数, 那个乘数一定是这些数的最大公约数的约数, 然后可以发现这个数最多不超过$48$, 且一定是$3$的倍数. 利用上面条件, 暴力枚举.

## 171. Finding numbers for which the sum of the squares of the digits is a square
由于$0 < n < 10^{20}$, $f(n) \le 180$, 于是随便数位dp下就好了.

## 172. Investigating numbers with few repeated digits
$4^{10}$枚举每个数字出现的次数, 先判断数字个数之和恰好是18, 之后枚举第一个数字是什么, 然后用组合数统计下答案就好了, 需要注意不能有前导零.

## 173. Using up to one million tiles how many different "hollow" square laminae can be formed?
令里外的正方形边长分别是$a,b$, 那么有$a^2-b^2 \le n$并且$a$和$b$同奇偶, $a^2 \le n + b^2$, 那么显然$a$最大不超过$n$, 暴力枚举$n$, 然后解出$b$的范围即可.

## 174. Counting the number of "hollow" square laminae that can form one, two, three, ... distinct arrangements
根据#173的答案可以发现, 合法的`hollow square`不多, 于是暴力枚举所有合法的$a,b$, 统计$a^2-b^2$出现的次数就好了.

## 175. Fractions involving the number of different ways a number can be expressed as a sum of powers of 2
通过[oeis](http://oeis.org/A002487)查表可以知道, $f(n)/f(n-1)$依次构成了[Stern-Brocot Tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)的每一项, 已知树上某一项, 可以利用欧几里得算法求出路径.

## 176. Right-angled triangles that share a cathetus
通过[oeis](https://oeis.org/A046079)查表知道, 如果$n=2^e\prod p_i^{f_i}$, 那么$f(n)=\frac{(2e-1)\prod (2f_{i}+1) - 1}{2}$, 然后题目给的数字比较小, 随便手算下就得出答案了.

## 177. Integer angled Quadrilaterals
令$a,b,c,d,e,f,g,h$分别为$\angle{CAD},\angle{BAC},\angle{ABD},\angle{CBD},\angle{ACB},\angle{ACD},\angle{BDC},\angle{ADB}$, 已知$a,b,c,d,e,f,g,h$的情况下, 如果$\sin{a}\sin{c}\sin{e}\sin{g}=\sin{b}\sin{d}\sin{f}\sin{h}$满足, 那么就是一个合法的四边形.

令$AC,BD$的交点为$O$, $o=\angle{AOB}$, 然后枚举$o,a,b,d$, 可以求出$c=180-b-o,h=o-a,e=o-d$, 剩下$f,g$还没有确定. 考虑正弦定理, 令$BO=1$, 那么$OC=\frac{\sin{d}}{\sin{e}},OD=\frac{\sin{a}\sin{c}}{\sin{b}\sin{h}}$, 之后利用余弦定理就可以知道$CD$的长度, 然后再次用正弦定理求出$\sin{g},\sin{f}$的值, 就可以用$\arcsin$求出$g,f$了. 判断$g$和$f$是不是整数, 以及检查下度数条件是否满足即可. 需要判断四边形是否相似, 直接用最小表示就好了, 需要注意的是需要用$8$个角做最小表示, 只用$4$个会不对.

## 178. Step Numbers
随便数位dp下就好了.

## 179. Consecutive positive divisors
筛法求出每个数的约数个数, 然后就没了.

## 180. Rational zeros of a function of three variables
化简下可以知道$f_n(x,y,z)=(x+y+z)(x^n+y^n-z^n)$, 只需要考虑$x^n+y^n=z^n$, 根据费马大定理, 只需要检查$n=\pm 1, \pm 2$的情况. 暴力枚举$x,y$, 求出$z$就好了.

## 181. Investigating in how many ways objects of two different colours can be grouped
$dp(i,j)=\sum\limits_{a=0}^{i}\sum\limits_{b=0}^{j}dp(i-a,j-b)[a+b>0]$.

## 182. RSA encryption
枚举每个$m$, 求出最小的$e$使得$m^e \text{ mod } n = 1$, 那么所有的$ke+1$都满足$m^{ke+1} \text{ mod } n=m$. 显然$e | \phi(n)$, 暴力枚举就好了.

论坛里面给出了一个更简单的做法, 答案就是$\sum\limits_{e=2}^{\phi(p, q)}(1 + gcd(e-1, p-1))(1 + gcd(e-1,q-1))$.

## 183. Maximum product of parts
对函数$f(x)=(\frac{n}{x})^x$, 求导之后可以发现, 当$x=e$的时候取到最值, 于是$k$只能是$\lfloor \frac{n}{e} \rfloor$和$\lceil \frac{n}{e} \rceil$之一. 要使得$M(n)$不循环, 那么$\frac{k}{(k,n)}$的质因子只能是2或者5.

## 184. Triangles containing the origin
方案显然是旋转对称的, 于是只考虑以下几种情况就好了, 令第I象限内总共有$s$个合法的点, $x$正半轴有$t$个点.

1. 三个点分别属于I, III, IV象限：考虑枚举I,III象限的点$A$和$B$, 要求$\vec{AB}\times \vec{AO} < 0$, 那么贡献是$s$.
2. 三个点分别属于II, II, IV象限：考虑枚举IV象限的点$A$和II象限的点$B$, 统计出有多少个$B$满足$\vec{AB}\times \vec{AO} < 0$, 记为$c^{-}(A)$；同样统计出有多少个$B$满足$\vec{AB}\times \vec{AO} > 0$, 记为$c^{+}(A)$, 那么贡献是$c^{-}(A)c^{+}(A)$.
3. 三个点分别属于I, II象限和$y$轴负半轴：对答案的贡献是$s^2t$.
4. 三个点分别属于I, III象限和$y$轴负半轴：和1类似, 枚举I,III象限的点$A$和$B$, 要求$\vec{AB}\times \vec{AO} < 0$, 那么贡献是$t$.
5. 三个点分别属于II, IV象限和$y$轴负半轴：答案和4一样.

## 185. Number Mind

一个暴力的方法, 分前8位和后8为枚举可能合法的位置, 之后暴力组合起来就好了.

正确的爆搜姿势应该是按照猜测数字一个个排除数字的可能性. 答案是: ```4640261571849533```.

## 186. Connectedness of a network
暴力枚举直到满足条件为止.

## 187. Semiprimes
先线性筛出$n$以内的所有素数, 同时计算出$\pi(n)$, 然后枚举第一个质数, 利用$\pi(n)$统计第二个即可.

## 188. The hyperexponentiation of a number
利用指数循环节$a^b \equiv a^{b \text{ mod } \phi(n)} \text{ mod } n$不断递归就好了.

## 189. Tri-colouring a triangular grid

数位dp, $f(i,s)$记录第$i$行正三角颜色状态为$s$时的方案数, 转移时枚举上一行的状态, 那么夹在中间的倒三角颜色方案数就可以计算出来了, 当做转移系数乘一下就好了.

## 190. Maximising a weighted product

用拉格朗日乘数法, 解一下方程可以知道$x_i=\frac{2i}{m+1}$.

## 191. Prize Strings

简单数位dp下就好了.

## 192. Best Approximations

实现[Best rational approximations](https://en.wikipedia.org/wiki/Continued_fraction#Best_rational_approximations)的算法就好了. 注意比较的时候直接用连分数比较大小比较方便.

## 193. Squarefree Numbers
$S(n)=\sum\limits_{i=1}^{\lfloor\sqrt{n}\rfloor}\mu(i)\lfloor\frac{n}{i^2}\rfloor$.

## 194. Coloured Configurations

先用`dfs`搜出两种类型各自的染色方案数, 之后就是一个组合数搞一下.

## 195. Inscribed circles of triangles with one angle of 60 degrees
类似之前的$120^{\circ}$, [Finding parametric equations for 120 and 60 degree triples](http://www.geocities.ws/fredlb37/node9.html), 可以得到如下公式:
>$(u,v,w)$是$60^\circ$三角形, 当且仅当存在两个互质的正整数$m$和$ n$ $(3\nmid m-n, m > n)$使得: $u=k\left(2mn+m^2\right), v=k\left(2mn+n^2\right), w=k\left(m^2+n^2+mn\right)$或者$u=k\left(m^2-n^2\right), v=k\left(2mn+m^2\right), w=k\left(m^2+n^2+mn\right)$其中$k$是一个正整数.

## 196. Prime triplets

用`miller rabin`求出前面$2$行和后面$2$行的素数, 然后暴力统计就好了.

## 197. Investigating the behaviour of a recursively defined sequence

打表后可以发现, $u+f(u)$最后会收敛成```1.710637717```.

## 198. Ambiguous Numbers

可以知道`ambiguous numbers`一定是`Farey`序列相邻两项的平均值, 于是用[Stern–Brocot tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)暴力枚举就好了.

## 199. Iterative Circle Packing

利用[Descartes' theorem](https://en.wikipedia.org/wiki/Descartes%27_theorem)可以方便求出相切的圆. 然后在迭代计算的时候, 尽量把相同相切结构的圆合到一起计算, 这样就可以很快出解了.

## 200. Find the 200th prime-proof sqube containing the contiguous sub-string "200"

筛出$10^6$以内的所有素数, 然后求出$10^{12}$以内的`sqube`, 显然个数不会太多. 然后枚举每个`sqube`, 判断是否包含"200"为子串, 如果包含, 在用素数测试判断是否是`prime-proof`.
