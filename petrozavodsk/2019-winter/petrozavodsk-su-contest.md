# Petrozavodsk SU Contest

- [ ] [A. DIY Radar]
- [ ] [B. Word Squared]
- [ ] [C. Quoridor]
- [ ] [D. Game X]
- [ ] [E. 5-Path]
- [ ] [F. Nightmare]
- [ ] [G. String Transformation]
- [ ] [H. Employees]
- [ ] [I. Modulo-magic squares]
- [x] [J. Count the Sequences]

## J. Count the Sequences

题意：给出$n$，$m$和$c$，求出满足下面条件的$(x_1,x_2,\dots,x_m)$个数，对$998244353$取模：

+ $0 \le x_i \le b^i - c$

+ $\sum_{i=1}^{m} x_i < n$

$1 \le m \le 50, 2 \le b \le 10^9, -b+2 \le c \le b - 1, 1 \le n \le b^{m+1}$

题解：考虑令$x_{m+1}=n-\sum_{i=1}^{m}x_i$，那么就可以把小于号变成等号，等价于求$x_1+x_2+\dots+x_m+x_{m+1}=n$的方案数。带上下界的方案数，可以考虑容斥，答案是

$$
\sum_{S \subseteq [1,n]}(-1)^{|S|} \binom{n+m-1-(\sum_{i \in S} b^i-c+1)}{m}
$$

注意到$m$比较小，我们可以把组合数$\binom{D-x}{m}$表示成$\frac{(D-x)(D-1-x)\cdots (D-m+1-x)}{m!}$，这个是一个$m$阶的多项式$p(x)=\sum_{i=0}^{m} a_i x^i$。我们把$\sum_{i \in S}b^i$带入上面的多项式就可以求出这个组合数。接下来考虑把多项式的每一项单独考虑，最后加起来就是答案。

令$f(i,j,k)$表示$S \subseteq [1,i]$并且$|S|=j$时，$(\sum_{i \in S}b^i)^k$的和。转移方程很简单：

$$
f(i,j,k)=f(i-1,j,k)+\sum_{t=0}^{k}\binom{k}{t}b^{it}f(i-1,j-1,k-t)
$$

观察下组合数什么时候非零，就是$n+m-1-(\sum_{i \in S} b^i-c+1) \ge m$，得到$\sum_{i \in S} b^i < n+|S|(c-1)$。

那么我们可以枚举$|S|$，然后把$n+|S|(c-1)$表示成一个$b$进制数$d_{k}d_{k-1}\dots d_0$，然后进行数位dp即可。
