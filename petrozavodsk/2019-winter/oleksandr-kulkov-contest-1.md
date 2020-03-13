# Petrozavodsk Winter 2019. Oleksandr Kulkov Contest 1

- [ ] [A. Tritwise Mex](https://codeforces.com/gym/102129/problem/A)
- [ ] [B. Associativity Degree](https://codeforces.com/gym/102129/problem/B)
- [ ] [C. Medium Hadron Collider](https://codeforces.com/gym/102129/problem/C)
- [ ] [D. Basis Change](https://codeforces.com/gym/102129/problem/D)
- [ ] [E. Scored Nim](https://codeforces.com/gym/102129/problem/E)
- [ ] [F. Milliarium Aureum](https://codeforces.com/gym/102129/problem/F)
- [ ] [G. Permutant](https://codeforces.com/gym/102129/problem/G)
- [ ] [H. Game Of Chance](https://codeforces.com/gym/102129/problem/H)
- [x] [I. Incomparable Pairs](https://codeforces.com/gym/102129/problem/I)
- [ ] [J. The Zong of the Zee](https://codeforces.com/gym/102129/problem/J)
- [ ] [K. Expected Value](https://codeforces.com/gym/102129/problem/K)

## I. Incomparable Pairs

题意：给出一个字符串$s$，求出有多少对字符串$(a,b)$使得$a$不是$b$的子串，$b$也不是$a$的子串。并且$a$和$b$都是$s$的一个非空子串。

$1 \le |s| \le 10^5$

题解：先转成求$a$是$b$的子串，或者$b$是$a$的子串。

我们如果从左往右依次加入每个字符，然后能够快速维护$cnt(x)$表示当前有多少字符串的左端点是$x$。那么每次询问其实就是对$cnt[l_i..r_i]$求和。

考虑从左往右依次加入字符构建一个后缀自动机。假设加入字符$s_i$后落在节点$u^i$上，考虑$u^i$沿着`suffix link`走到根的这条路径，显然这些节点对应的字符串都是以$i$为右端点的，然后这些串的左端点构成了一个连续区间$[l_i,r_i]$。也就是说要对这段区间$cnt(x)$要加上$1$。同时我们还需要减去一些$cnt(y)$，因为路径上这些点原先对应的字符串原先右端点是另一个数$j$，然后他们的左端点也是对应了一个区间$[l_j,r_j]$，对这些区间的$cnt(y)$都减$1$即可。

不妨在后缀自动机上记录一个$mx$表示这个点当前的右端点是谁。然后一个节点$u$对应的右端点就是$u$这棵子树里面$mx$的最大值。对于每个左端点$x$，维护$up(x)$，表示从$u^x$出发往上一直走到$up(x)$这些节点的右端点都是$x$。

那么每次加入一个字符$s_i$后，只需要利用$up(\cdot)$数组，快速找到一段右端点相同的路径，不妨假设右端点为$j$，这条路径长度为对应的区间为$[l_j, r_j]$，那么把$cnt(l_j..r_j)$减去$1$即可。

这样每次暴力修改，复杂度均摊是$O(n \log n)$的。每次修改，还需要用线段树或者树状数组维护区间和，总的复杂度是$O(n \log^2 n)$。
