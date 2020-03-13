# XIX Open Cup. Grand Prix of Belarus

+ [ ] [A. Alien Invasion](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/A/)
+ [ ] [B. Bus Stop](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/B/)
+ [ ] [C. Calculating Average](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/C/)
+ [ ] [D. Data Structure Problem](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/D/)
+ [ ] [E. Expected Cost](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/E/)
+ [x] [F. Fractional XOR Maximization](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/F/)
+ [ ] [G. Go West](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/G/)
+ [ ] [H. Humongous String](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/H/)
+ [ ] [I. Intellectual Prefix Maxima](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/I/)
+ [x] [J. Jimp Numbers](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/J/)
+ [ ] [K. K-Triangles](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/K/)
+ [ ] [L. Long Game](https://official.contest.yandex.ru/opencupXIX/contest/11931/problems/L/)

## F. Fractional XOR Maximization

题意：对于两个实数$x$和$y$，定义他们的异或为$x \oplus y = \lim_{n \to \infty} \frac{\lfloor 2^n x \rfloor \oplus \lfloor 2^n y \rfloor}{2^n}$。现在给出两个实数区间$[a,b]$和$[c,d]$，求出集合$\{x \oplus y: x \in [a,b], y \in [c,d]\}$。

$0 \le a_{num}, b_{num}, c_{num}, d_{num} \le 10^{17}, 1 \le a_{dem}, b_{dem}, c_{dem}, d_{dem} \le 30$。

题解：题目给出的定义就是求出$x$和$y$的二进制表示，然后逐位异或起来。我们不妨假设区间里的数都搞成了一个trie树，然后从高到低枚举每一位来确定答案。假设当前处理到了第$i$位，然后考虑当前trie对应的两个区间$[a,b]$和$[c,d]$在第$i$位的情况：

+ $a_i=0,b_i=0,c_i=0,d_i=0$，那么答案的第$i$位为$0$，区间没有变化
+ $a_i=0,b_i=0,c_i=1,d_i=1$，那么答案的第$i$位为$1$，区间没有变化
+ $a_i=1,b_i=1,c_i=0,d_i=0$，那么答案的第$i$位为$1$，区间没有变化
+ $a_i=1,b_i=1,c_i=1,d_i=1$，那么答案的第$i$位为$0$，区间没有变化
+ $a_i=0,b_i=0,c_i=0,d_i=1$，那么答案的第$i$位为$1$，$c$对应的子树被删掉了，接下来每一位$c_j$ $(j < i)$都是$0$
+ $a_i=1,b_i=1,c_i=0,d_i=1$，那么答案的第$i$位为$1$，$d$对应的子树被删掉了，接下来每一位$d_j$ $(j < i)$都是$1$
+ $a_i=0,b_i=1,c_i=0,d_i=0$，那么答案的第$i$位为$1$，$a$对应的子树被删掉了，接下来每一位$a_j$ $(j < i)$都是$0$
+ $a_i=0,b_i=1,c_i=1,d_i=1$，那么答案的第$i$位为$1$，$b$对应的子树被删掉了，接下来每一位$b_j$ $(j < i)$都是$1$
+ $a_i=0,b_i=1,c_i=0,d_i=1$，可以发现接下来答案的每一位都可以变成$0$，因此给答案加上$2^{i+1}$然后推出循环即可。

然后注意到，如果我们没能退出循环，那么上述过程可以无限做下去。假设我们做到了$2^{-5}$了，考虑$a,b,c,d$二进制表示的周期分别是$r(a),r(b),r(c),r(d)$。那么如果区间不发生任何变化，我们可以在接下来$L=\text{lcm}(r(a), r(b), r(c), r(d))$步后退出，因为我们一定可以在这里找到答案的循环节。如果区间发生了变化的话，重新计算下这个$L$，以及重新累积步数即可。

经过一些计算可以发现$r(\cdot)$的最大值是$[0, 1, 2, 1, 4, 2, 3, 1, 6, 4, 10, 2, 12, 3, 4, 1, 8, 6, 18, 4, 6, 10, 11, 2, 20, 12, 18, 3, 28, 4]$，因此$lcm(r(a), r(b), r(c), r(d)) \le 13860$。我们最坏会循环$13860 * 4$步。但是实际上在$360$左右就跑出来了。

## H. Humongous String

题意：对于字符集$\Sigma = \{s_0, \dots, s_{k−1}\}$，定义序列$\{T_i\}$：$T_0 = s_0$，$T_i = T_{i-1} s_{i \bmod k}, i \ge 1$。

令$S = T_0T_1T_2\dots$，求出长度为$n$的前缀里有多少本子不同的非空子串。

$1 \le n, k \le 10^9$

题解：把这个无限长的字符串切一切，如果$1 \le i \bmod k \le k-2$，那么$T_i$看成一个整体；然后把$T_{i}T_{i+1}$看成一个整体，如果$i \equiv k-1 \pmod k$。那么，如果一个子串$t$跨过了两个边界，那么这个串肯定只出现一次。因为假设某个整体串$u$是$t$的子串，那么$us_{0}$肯定是$t$的子串。可以发现，$u$的最后结尾肯定不是$s_0$或者$s_{k-1}$。同时$t$中接在$u$前的字符也不是$s_{k-1}$，然后分析可以发现，$t$不可能作为子串出现在其他地方。

对于每个整体串$X$，考虑计算$cnt(X,i)$表示有多少以$X_i$结尾的子串，曾经在前面出现过。那么答案就是$\frac{n(n+1)}{2}-\sum cnt(X,i)$。假设$X$里面第一个$T_i$的长度为$x$，努力分析可以知道，如果$k \ge 3$的话：

$$
cnt(X,i)=\begin{cases} i &  x \le k, i < x \\
0 &  x \le k, i = x \\
i & x=k+1, i \le x \\
i + b - k - 1 & X \text{ is big }, 2x + 1 - i \ge 2k \\
i - k  & X \text{ is big }, 2x + 1 - i < 2k \\
i + 2b-3-2k & x \bmod k = 1, i \le x - k \\
i & x \bmod k = 1, i > x - k \\
i + b-1-k & x \bmod k \ne 1, i \le x - k \\
i & x \bmod k \ne 1, i > x - k
\end{cases}
$$

如果$k=2$的话：

$$
cnt(X,i)=\begin{cases} i + 2b+1-4k &  x \ge 4, 2x + 1 - i \ge 2k \\
i - k & x \ge 4, 2x + 1 - i < 2k \\
|i - 1| & x = 2 \\
1 & x=1 \\
\end{cases}
$$

对于每个$cnt(X, i)$你可以搞成一个$ax^2+bx+c$的形式。然后之后就是对一堆这个东西求和，可以都做到$O(1)$。

## J. Jimp Numbers

题意：给出$n$，求出$1$到$n$以内有多少数$k$满足：存在恰好一对三元组$(a,b,c)$使得$a$，$b$和$c$构成等差数列，且$a^2+b^2+k=c^2$。

$1 \le n \le 10^{11}$

题解：令$a=x-y,b=x,c=x+y$，那么化简后$k=x(4y-x)$。打表后可以发现，令$f(n,e)$表示$1$到$n$以内$\pmod 4=e$的素数个数，那么答案就是$f(n,3)+f(\lfloor \frac{n}{4} \rfloor, 1)+f(\lfloor \frac{n}{4} \rfloor, 3)+f(\lfloor \frac{n}{16} \rfloor, 1)+f(\lfloor \frac{n}{16} \rfloor, 3)$，还有两个特殊的$k=4,16$也是合法的。证明如下，

我们要使得$4y=x+\frac{k}{x}$是$4$的倍数且$y < x \to x > \sqrt{\frac{k}{3}}$。

+ 如果$k \equiv 1 \pmod 4$，那么$x + \frac{k}{x} \equiv 1 \pmod 4$，不合法。
+ 如果$k \equiv 2 \pmod 4$，那么$x$和$\frac{k}{x}$一定一奇一偶，不合法。
+ 如果$k \equiv 3 \pmod 4$，那么$x + \frac{k}{x} \equiv 0 \pmod 4$，那么$k$合法当且仅当$(\sqrt{\frac{k}{3}}, k-1]$里没有其他约数，也就说$k$是质数。
+ 如果$k=2^uv$，其中$u \ge 2$，$v$是奇数。那么$x = 2^st$，其中$1 \le s \le u - 1, t \mid v$。然后$s$和$u-s$要么同时为$1$，要么同时不为$1$。显然我们要求仅有一对$(s,t)=(u-1,v)$使得$2^st > \sqrt{\frac{k}{3}}$
  + 如果$u=2$并且$v=1$，那么$k=4$，合法
  + 如果$u=2$并且$v > 1$，令$q$是$v$的最小质因子，那么有$\frac{k}{2q}=\frac{2v}{q} \le \sqrt{\frac{k}{3}} < 2v$，可以得到$3v \le q^2$。如果令$e$是$q$在$v$质因数分解出现次数，那么就有$3q^e \le 3v \le q^2$，于是$e=1$。然后再推一推可以得到$v$是质数。
  + 如果$u=3$，分析$x$和$\frac{k}{x}$的奇偶性，可以知道不存在合法解。
  + 如果$u=4$，类似的可以分析得到$v=1$或者$v$是质数
  + 如果$u \ge 5$，可以发现也不存在合法解。

至于怎么求$f(n,3)$和$f(n,1)$呢，考虑求$1$到$n$里面质数个数的容斥。令$dp(n,p_i)$表示$1$到$n$里面有多少数$x$满足$x$是质数或者$x$的最小质因子大于$p_i$。那么显然$dp(n,p_i)=dp(n,p_{i-1})-(dp(\lfloor \frac{n}{p_i} \rfloor, p_{i-1}) - dp(p_i, i-1)$。加上$\pmod 4$的状态即可算出答案。
