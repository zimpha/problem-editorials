# XIX Open Cup. Grand Prix of Gomel

- [ ] [A. One Goal](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/A)
- [ ] [B. Two Teams](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/B)
- [ ] [C. Three Indices](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/C)
- [x] [D. Four Elements](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/D)
- [ ] [E. Five Points](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/E)
- [ ] [F. Six Words](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/F)
- [ ] [G. Seven Nevers](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/G)
- [ ] [H. Eight Sins](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/H)
- [ ] [I. Nine Judges](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/I)
- [ ] [J. Ten Ranges](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/J)
- [ ] [K. Eleven Problems](https://official.contest.yandex.ru/opencupXIX/contest/11930/problems/K)

## D. Four Elements

题意：有一个集合$A$，里面元素可以用$n$个不相交的区间$[l_i, r_i]$表示。现在给出一个整数$s$，求从$A$中选出$4$个不同数使得它们和为$s$的方案数。

$1 \le n \le 400, 0 \le l_i \le r_i \le 2 \times 10^8, r_i < l_{i+1}, 0 \le s \le 8 \times 10^8$

题解：显然$A$的生成函数是$F(x)=\sum\limits_{i=1}^{n}\frac{x^{l_i}-x^{r_i+1}}{1-x}$。那么答案就是

$$
\frac{1}{24}(F^4(x)-6F(x^2)F^2(x)+3F^2(x^2)+8F(x^3)F(x)-6F(x^4))
$$

接下来考虑每一项分别怎么求。

$F(x^4)$就是看$\frac{s}{4}$是不是在集合$A$里面。

$F(x^3)F(x)$的话，考虑枚举$x \in [l_i, r_i]$，$s-3x \in [l_j, r_j]$，然后可以求出$x$的实际范围是$[\max(l_i, \lceil \frac{s-r_j}{3} \rceil), \min(r_i, \lfloor \frac{s-l_j}{3} \rfloor)]$。

$F^2(x^2)$的话，考虑枚举$x \in [l_i,r_i]$，$\frac{s}{2}-x \in [l_j,r_j]$，同样可以求出$x$的具体范围是$[\max(l_i, \frac{s}{2}-r_j), \min(r_i, \frac{s}{2}-l_j)]$。

接下来两项，我们需要求出$G(x)=F^2(x)$，可以观察发现$G(x)$一定是$O(n^2)$段区间组成，对于第$i$个区间$[l_i,r_i]$，如果$x \in [gl_i, gr_i]$，那么存在一个$a_i$和$b_i$，使得$G(x)=a_i x + b_i$。我们可以在$O(n^2 \log n)$时间处理出这些东西。

考虑$F(x^2)G(x)$，不妨枚举$x \in [gl_i, gr_i]$，然后$\frac{s-x}{2} \in [l_j, r_j]$。我们同样可以解出$x$的一个范围$[\max(gl_i, s-2r_j), \min(gr_i,s-2l_j]$，同时$x$的奇偶性还要和$s$一样。之后就是对一个区间里，满足$x$和$s$奇偶性一样的$a_ix + b_i$求和，可以$O(1)$。同时注意到使得区间非空$(i,j)$只有$O(n^2)$对，用双指针就可以维护出来，总复杂度可以做到$O(n^2)$。

考虑$G^2(x)$，枚举$x \in [gl_i,gr_i]$，以及$s-x \in [gl_j,gr_j]$，可以得到$x$的范围为$[\max(gl_i,s-gr_j),\min(gr_i,s-gl_j)]$。之后就是对这个区间里的$(a_ix+b_i)(a_j(s-x)+b_j)$求和，这个也是可以做到$O(1)$的。类似$F(x^2)G(x)$，总体可以做到$O(n^2)$。

因此可以在$O(n^2 \log n)$的复杂度下解决这题。
