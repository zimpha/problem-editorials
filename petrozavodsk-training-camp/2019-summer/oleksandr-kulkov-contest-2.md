# Oleksandr Kulkov Contest 2

- [ ] [A. Square Root Partitioning](https://codeforces.com/gym/102354/problem/A)
- [ ] [B. Yet Another Convolution](https://codeforces.com/gym/102354/problem/B)
- [ ] [C. Money Sharing](https://codeforces.com/gym/102354/problem/C)
- [ ] [D. Magic Strings](https://codeforces.com/gym/102354/problem/D)
- [ ] [E. Decimal Expansion](https://codeforces.com/gym/102354/problem/E)
- [ ] [F. Cosmic Crossroads](https://codeforces.com/gym/102354/problem/F)
- [ ] [H. Defying Gravity](https://codeforces.com/gym/102354/problem/H)
- [ ] [I. From Modular to Rational](https://codeforces.com/gym/102354/problem/I)
- [ ] [J. Tree Automorphisms](https://codeforces.com/gym/102354/problem/J)

## D. Magic Strings

题意：$F_1=ab, F_{k+1}=F_kF_k b$，求$F_n$本质不同子串个数对$10^9+7$取模。

$1 \le n \le 10^{18}$

题解：可以构造两个$3 \times 3$的矩阵$A$和$B$，在后面加上字符`a`的话乘上矩阵$A$，加上$b$的话乘上矩阵$B$。那么原问题等价于$f_1=AB,f_{k+1}=f_kf_kB$。这个玩意这这个模数下周期是$5 \times 10^8+3$。本地每隔$10^6$打个表即可。
