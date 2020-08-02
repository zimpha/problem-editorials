# Petrozavodsk Winter 2014. Day 5. Moscow SU Tapir Contest

+ [ ] [A. Defense of the Ancients]
+ [ ] [B. Bombard]
+ [x] [C. Combinations Strike Back]
+ [ ] [D. DFT for Dummies]
+ [x] [E. Lingustic Estimations]
+ [ ] [F. Passing Finals]
+ [ ] [G. Important Guests]
+ [ ] [H. Angel and Demon]
+ [ ] [I. Illegal Wage]
+ [ ] [J. For Fun and Lulz]

## C. Combinations Strike Back

题意：有一个$n$个元素的multiset，第$i$个元素为$a_i$。现在给出$q$个询问，如果$x$个数增加$1$后，大小为$k$的multiset的数目。

$1 \le n,q \le 120000, 1 \le a_i,x \le n, 1 \le k \le n + 1$

题解：注意到每个询问的话，只和$x$出现的次数有关，不同的出现次数只有$O(\sqrt{n})$种。因此可以把出现次数一样的一起处理。

令$f(x)=\sum_{i=0}^{n}ways_i \cdot x^i$，其中$ways_i$是大小为$i$的multiset数目，这个可以一开始通过分治fft算出来。

那么考虑一个询问，显然就是求$\frac{f(x)}{1+x+\dots+x^m} \cdot (1+x+\dots+x^m+x^{m+1})$第$k$项的系数，其中$m$是出现次数。

只需要求出$\frac{f(x)}{1+x+\dots+x^m}$即可，这个可以线性求出来。

复杂度$O(n\log^2 n + n \sqrt{n})$。

## E. Lingustic Estimations

题意：对于一个字符串$S$，字符串$B$ `strongly continues` $A$，当且仅当$S$里面每个$A$都跟着一个$B$。字符串$B$ `weakly continues` $A$，当且仅当$AB$是$S$的子串，每个$A$后面跟着一个$B$，或者接下来的后缀长度不够$B$。

数有多少字符串$(A, B)$满足$A$和$B$都是$S$里非空字符串，$B$ `weakly continues` $A$。

$1 \le |S| \le 200000$

题解：考虑建出$S$反串的SAM，枚举$AB$对应的节点$u$，那么可以发现$A$对应的节点一定是$u$的祖先。枚举一个祖先$v$，那么这个祖先$v$对应不在子树$u$里的那些$A$需要满足`weakly continues`的条件。

也就是说考虑，$v$对应不在子树$u$里的那些$A$在反串中出现位置的最大值$m$（在原串中对应了最早出现位置），那么有$m < |AB|$，如果下标从$1$开始的话。

那么假设$u$对应的子串长度是$[l_u, r_u]$，那么对答案的贡献就是$(r_u - m_v) \cdot (r_v-l_v+1)$。

考虑从根节点开始DFS，用单调栈维护这个最大值$m_v$，以及$m_v \cdot (r_v-l_v+1)$和$r_v-l_v+1$的前缀和，那么对于一个$u$的查询的话就是在单调栈上二分出一个区间，然后算一下上面的式子。你需要维护可以撤销的单调栈即可，或者也可以用一个带内存回收的主席树。