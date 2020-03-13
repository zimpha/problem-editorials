# Volume 03

## 101. Optimum polynomial
最多枚举到$10$, 多项值插值一下.

## 102. Triangle containment
利用叉积判断即可.

## 103. Special subset sums: optimum
根据题目的信息, 我们可以利用$\{11, 18, 19, 20, 22, 25\}$构造出$\{20, 31, 38, 39, 40, 42, 45\}$这一组非最优解, 猜测最优解每项的上面这个解的差不会太大, 取$\pm 3$差不多就可以算出答案了$\{20, 31, 38, 39, 40, 42, 45\}$, 好吧其实就是构造出来的解.

## 104. Pandigital Fibonacci ends
考虑到$F_n=[\frac{\phi^n}{\sqrt{5}}]$, 于是$\log_{10}{F_n}=\log_{10}{\frac{\phi^n}{\sqrt{5}}}=n\log_{10}{\phi}-\log_{10}{\sqrt{5}}$. 考虑这个数的小数部分$t_n$, 可以得出$10^{t_n+8}$就是$F_n$的前$10$位. 于是暴力枚举即可.

## 105. Special subset sums: testing
把集合大小相同的一起排序, 然后依次枚举相邻两个数判断大小即可.

## 106. Special subset sums: meta-testing
简单的可以知道集合大小相同且不相交的集合对有$\sum\limits_{i=2}^{\frac{n}{2}}\frac{\binom{n}{i}\binom{n-i}{i}}{2}$. 对于集合大小为$i$的, 我们考虑哪些是不需要比较的. 不妨令在$B$集合的元素为(, 在$C$集合的为), 那么只有那些长度为$2i$的匹配括号是不需要比较的, 因为匹配, 所以可以找到一种匹配方案使得$C$中每个元素都大于$B$中每个元素. 匹配括号数目就是Catalan数$\frac{\binom{2i}{i}}{i+1}$. 于是答案就是$$\sum\limits_{i=2}^{\frac{n}{2}}\frac{\binom{n}{i}\binom{n-i}{i}}{2}-\frac{\binom{n}{2i}\binom{2i}{i}}{i+1}$$.

## 107. Minimal network
直接跑`prim`算法即可.

## 108. Diophantine reciprocals I
做些化简可以的得到$(x-n)(y-n)=n^2$, 于是解的个数只和$n^2$的约数有关. 考虑$n=\prod p_i^{a+i}$, 那么$n^2$约数个数为$\prod (2a_i+1)$. 暴力枚举$n$计算即可.

## 109. Darts
注意到$1\sim 20$可以有S, D, T, $25$只能有S和D, $0$只能有S. 暴力枚举每种组合即可.

## 110. Diophantine reciprocals II
类比#108的结论, 然后观察一下可以知道$a_1 \ge a_2 \ge ... \ge a_k$. 写个爆搜就好了.

## 111. Primes with runs
通过`factor`命令可以尝试出$M(10,d)=\{8, 9, 8, 9, 9, 9, 9, 9, 8, 9\}$, 于是直接暴力枚举未确定的位置然后判断是不是素数就好了.

## 112. Bouncy numbers
答案不是很大, $n$从小到大枚举计算就好了. 当然由于这个东西是单调递增的, 可以考虑二分答案, 然后数位dp计算.

## 113. Non-bouncy numbers
直接数位dp就好了, 记得减去全部位数相同的那些, 这个会多算一次.

## 114. Counting block combinations I
枚举红色的个数$s$, 以及块数$k$, 那么答案就是$f(n,m)=\sum\limits_{s=m}^{n}\sum\limits_{k=1}^{\lfloor \frac{s}{m} \rfloor}{\binom{s-mk+k-1}{k-1}\binom{j-s+1}{k}}$, 其中$m=3$.

## 115. Counting block combinations II
考虑#114中的式子, 从小到大枚举$n$即可.

## 116. Red, green or blue tiles
令$f(n,m)=\sum\limits_{k=1}^{\lfloor \frac{n}{m} \rfloor}{\binom{n-km+k}{k}}$, 那么答案就是$f(n,2)+f(n,3)+f(n,4)$.

## 117. Red, green, and blue tiles
枚举红绿蓝用的块数分别是$r,g,b$ $(2r+3g+4b \le n)$, 对答案的贡献是$\binom{r+g}{g}\binom{r+g+b}{b}\binom{n-r-2g-3b}{r+g+b}$.

## 118. Pandigital prime sets
枚举每个子集, 计算出这个子集能够搞出多少种不同的素数. 之后枚举整数划分, 利用之前的结果计数即可.

## 119. Digit power sum
枚举所有的$a^b$ $(2 \le a \le 1000, 1 \le b \le 50)$即可.

## 120. Square remainders
考虑二项式展开, $a^x (x \ge 2)$那些项都是可以忽略的, 那么只需要考虑$(-1)^{n-1}na+(-1)^n+an+1$, 如果$n$是偶数答案是$2$, 如果是奇数答案是$2an \text{ mod } a^2$, $n$从$1$枚举到$a^2$即可.

## 121. Disc game prize fund
假设赢的概率是$p$, 设置的奖金为$x$, 那么为了不赔钱, 需要满足$(x-1)p \le 1 - p$, 得到$x \le \frac{1}{p}$. 于是$x$的值应该取$\lfloor \frac{1}{p} \rfloor$. 考虑$dp$计算概率, 令$f(i,j)$表示玩了$i$轮, 蓝色球总共取了$j$次的概率, 显然有$f(i,j)=\frac{if(i-1,j)}{i+1}+\frac{f(i-1,j-1)}{i+1}$. 用`long long`模拟下分数类就好了.

## 122. Efficient exponentiation
枚举每个$k$, 爆搜即可.

## 123. Prime square remainders
同#120, 只有$n$为奇数是有用的, 然后可以观察到$n$的范围大概是$\sqrt{10^{10}}=10^5$左右, 筛出附近的素数判断下即可.

## 124. Ordered radicals
$rad(n)$可以直接用筛法求出来, 排个序直接算答案就好了.

## 125. Palindromic sums
完全平方数只有$\sqrt{n}$个, 于是连续和最多只有$n$个, 暴力枚举这些和然后判断是不是回文数, 记得去重即可.

## 126. Cuboid layers
找找规律可以发现一个$a\times b \times c$的cuboid包了第$n$层需要的cube数目为$C(a,b,c,n)=2(ab+bc+ca)+4(a+b+c+n-2)(n-1)$. 猜个上限$10^5$, 暴力枚举$a,b,c,n$使得$C(a,b,c,n)$不超过这个上限即可.

## 127. abc-hits
先用#124的方法求出所有的$rad(n)$, 然后将$rad$排个序. 由于任意两个数互质, 显然$rad(abc)=rad(a)rad(b)rad(c)$. 考虑枚举$c$, 然后根据$rad$从小到大枚举$rad(a)$, 显然有$rad(a)rad(c) < c$, 不满足的直接break就好了. 然后算出$b=c-a$检查下是否互质, 以及$rad(abc)$是否小于$c$确定合法的$c$.

## 128. Hexagonal tile differences
考虑每一圈的六边形边界, 可以通过简单的观察知道只有这些六边形的起点和终点才可能成为答案. 于是暴力枚举这些值, 判断是否满足条件即可.

## 129. Repunit divisibility
考虑到$A(n) > n$, 于是可以令$n=10^6$开始枚举, 然后很快就出答案了.

## 130. Composites with prime repunit property
暴力枚举答案即可.

## 131. Prime cube partnership
猜测了下$n$一定要是一个立方数, 并且$n+p$也要是一个立方数, 然后$n^3+np$显然会是一个立方数. 考虑$n=x^3,n+p=y^3$, 可以得到$p=(y-x)(x^2+xy+y^2)$. 由于$p$是素数, 显然$y=x+1$, 于是$p=3x^2+3x+1$. 暴力枚举$x$, 判断$p$是不是素数就好了.

## 132. Large repunit factors
$R(n)=\frac{10^n-1}{9}$, 考虑$R(n) \text{ mod } p=0$的情况, 有$\frac{10^n-1}{9}\equiv 0 \text{ mod } p$, 可以得到$10^n \equiv 1 \text{ mod } (9p)$. 于是从小到大枚举每个素数$p$判断即可.

## 133. Repunit nonfactors
利用#132的结论, 暴力枚举每个素数, 然后$n$从$1$枚举到$9p$（应该可以更少, 知道找到循环节为止）, 判断是否存在$n$满足$10^n \equiv 1 \text{ mod } (9p)$.

## 134. Prime pair connection
可以列出式子$10^{d(p_1)}x+p_1 \equiv 0 \text{ mod } p_2$, 这是个同余方程, 直接解就好了.

## 135. Same differences
令$x=y+d,z=y-d$, $(y+d)^2-y^2-(y-d)^2=4yd-y^2=y(4d-y)=n$, 于是$y$是$n$的约数, 暴力枚举$n$的约数$y$判断$\frac{n}{y}+y$是不是$4$的倍数即可算出方程解数.

## 136. Singleton difference
同上, 枚举约数的时候不要特别暴力即可.

## 137. Fibonacci golden nuggets
可以求出$A_F(x)=\frac{x}{1-x-x^2}$, 令$\frac{x}{1-x-x^2}=n$, 化简下得到$-nx^2 - (n+1)x + n = 0$, 根据求根公式, 可以得到$x = \frac{-(n+1) \pm \sqrt{(n+1)^2 + 4n^2}}{2n}$. 要令$x$是有理数, 那么$\sqrt{(n+1)^2 + 4n^2}$是整数. 暴力枚举找规律之后可以发现第$k$个golden nugget是$F(2k)F(2k+1)$.

## 138. Special isosceles triangles
令$b=2x$, 根据$2x \pm 1 = h$, 以及$x^2+h^2=L^2$可以得到$5x^2 \pm4x + 1 = L^2$. 参考[Dario Alpern’s Generic Two integer variable  equation solver](http://www.alpertron.com.ar/QUAD.HTM), 可以得出:
$$\begin{aligned}
x_{n+1} &= -9x_n -4L_n -4 \\
L_{n+1} &= -20x_n -9L_n -8
\end{aligned}$$
其中, 初始值$(x_0,L_0)=(0,1)$. 观察到$|L|$就是题目要求的答案, 算一下就好了.

## 139. Pythagorean tiles
考虑勾股数为$(a,b,c)$, 那么只要满足$b-a \mid c$就是合法的答案. 于是只要枚举所有互素勾股数就好了, 参考[Tree of primitive Pythagorean triples](https://en.wikipedia.org/wiki/Tree_of_primitive_Pythagorean_triples)即可.

## 140. Modified Fibonacci golden nuggets
可以求出$A_G(x)=\frac{x + 3x^2}{1-x-x^2}$, 类似#137, 令$\frac{x + 3x^2}{1-x-x^2}=n$, 化简得到$(3+k)x^2+(1+k)x-k=0$, 只要$(k+1)^2+4k(k+3)$是完全平方即可, 考虑这个不定方程$b^2 = (1+k)^2 + 4(3 k)k = 5k^2 + 14k + 1$, 同#138, 参考[Dario Alpern’s Generic Two integer variable  equation solver](http://www.alpertron.com.ar/QUAD.HTM), 可以得到如下递推式子:
$$\begin{aligned}
x_{n+1} &= -9x_{n}-4y_{n}-4 \\
y_{n+1} &= -20x_n-9y_n-8
\end{aligned}$$
初始值有这些:$\{(0, -1), (0, 1), (-3, -2), (-3, 2), (-4, -5), (-4, 5), (2, -7), (2, 7)\}$. 求解的时候只需要加入$x_i > 0$的那些就好.

## 141. Investigating progressive numbers, $n$, which are also square
不妨令$r < d < q$, 令公比为$k$, 那么有$d=kr,q=k^2r$.

令$k=a/b, (a,b)=1$. 那么有$d=ra/b,q=ra^2/b^2$. 考虑到$(a,b)=1$, 那么必有$b^2 \mid r$. 可以令$r=cb^2$, 那么$d=cab,q=ca^2$, $n=qd+r=c^2a^3b+cb^2 \le 10^{12}$, 于是可以得到$2\le a < 10^4, 1\le b < a, 1 \le c$.

暴力枚举所有可行的$a,b,c$, 然后判断$n$是不是完全平方数即可.

## 142. Perfect Square Collection
考虑枚举$x+y=a^2,x-y=b^2,x+z=c^2,b < c < a$, 然后解出$x,y,z$, 判断剩下的数是不是完全平方数即可.

## 143. Investigating the Torricelli point of a triangle
通过简单的推导, 可以知道$T$那三个角都是$120^{\circ}$, 根据余弦定理, 可以得到$p,q,r$和$a,b,c$的关系$a^2=q^2+r^2+qr$, $c^2=r^2+p^2+rp$, $b^2=p^2+q^2+pq$.

考虑构建这样一个图, 枚举所有可行的$(x,y)$使得$x^2+y^2+xy$是完全平方数, 在$x$和$y$之间连一条无向边. 那么只要找到图中的一个三元环就找到了一组合法的解$(p,q,r)$. 按照度数连边, 三元环可以$O(m\sqrt{m})$.

为了快速枚举所有可行的$(x,y)$, 可以参考[Finding parametric equations for 120 and 60 degree triples](http://www.geocities.ws/fredlb37/node9.html).

>$(a,b,c)$构成了一个$120^\circ$的三角形(即$c^2=a^2+b^2+ab$), 当且仅当存在两个互质的正整数$m$和$n$ $(3\nmid m-n, m > n)$使得:$a=k(m^2-n^2), b=k(2mn+n^2),c=k(m^2+n^2+mn)$

## 144. Investigating multiple reflections of a laser beam
推出反射的公式, 然后暴力迭代直到出去为止.

## 145. How many reversible numbers are there below one-billion?
可以直接暴力枚举每个数, 判断是不是`reversible number`.

## 146. Investigating a Prime Pattern
通过同余分析可以知道, $n \equiv 0 \text{ mod } 10$, $n^2 \equiv 1 \text{ mod } 3$, $n^2 \ne 0 \text{ mod } 9$, $n^2 \ne 0 \text{ mod } 13$, $n^2 \ne 0 \text{ mod } 27$, $n^2 \equiv 2 \text{ or } 3 \text{ mod } 7$. 先根据上面条件筛掉不合法的数, 之后用[Miller–Rabin primality test](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test)判断即可.

## 147. Rectangles in cross-hatched grids
对于非斜着的只需要枚举子矩形的大小为$x \times y$, 出现次数为$(n-x+1)(m-x+1)$, 考虑那些斜着的, 枚举最下面那个顶点的为止, 考虑每次斜着往左扩展$0.5$后, 斜着往右最多能扩展多少即可.

## 148. Exploring Pascal's triangle
考虑lucas定理, $\binom{n}{m}$不被$7$整除, 当且仅当$n-m$在$7$进制下不会产生进位, 也就是说令$n,m$在$7$进制下为$n=n_1n_2\cdots n_k,m=m_1m_2\cdots m_k$, 那么$n_i\ge m_i$都成立, 于是对着$n$数位dp就好了.

## 149. Searching for a maximum-sum subsequence
暴力$4$个方向, 用最大字段和的搞搞.

## 150. Searching a triangular array for a sub-triangle having minimum-sum
暴力$O(n^3)$枚举即可.
