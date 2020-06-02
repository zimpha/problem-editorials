# XVIII Open Cup. Grand Prix of Saratov

+ [x] [A. Three Arrays](https://codeforces.com/gym/101741/problem/A)
+ [ ] [B. Expected Shopping](https://codeforces.com/gym/101741/problem/B)
+ [ ] [C. Cover the Paths](https://codeforces.com/gym/101741/problem/C)
+ [ ] [D. Elevator](https://codeforces.com/gym/101741/problem/D)
+ [ ] [E. Code-Cola Plants](https://codeforces.com/gym/101741/problem/E)
+ [ ] [F. GCD](https://codeforces.com/gym/101741/problem/F)
+ [ ] [G. Berland Post](https://codeforces.com/gym/101741/problem/G)
+ [ ] [H. Compressed Spanning Subtrees](https://codeforces.com/gym/101741/problem/H)
+ [x] [I. Prefix-Free Queries](https://codeforces.com/gym/101741/problem/I)
+ [ ] [J. Subsequence Sum Queries](https://codeforces.com/gym/101741/problem/J)
+ [ ] [K. Consistent Occurrences](https://codeforces.com/gym/101741/problem/K)
+ [ ] [L. Increasing Costs](https://codeforces.com/gym/101741/problem/L)

## A. Three Arrays

题意：给出三个数组$a$，$b$和$c$，求出有多少对$(i,j,k)$使得$|a_i-b_j| \le d, |a_i - c_k| \le d, |b_j - c_k| \le d$。

$1 \le |a|, |b|, |c| \le 5 \cdot 10^5, 1 \le d \le 10^9, -10^9 \le a_i, b_i, c_i \le 10^9$

题解：枚举$i$，可以求出合法$b$的范围$[lb_i,rb_i]$和合法$c$的范围$[lc_i,rc_i]$。之后枚举每个$j$，遇到$lb_i$则把区间$[lc_i,rc_i]$里都加$1$，遇到$rb_i+1$则把区间$[lc_i,rc_i]$里都减$1$。然后可以求出合法的$c$的范围$[l,r]$，查询$[l,r]$的区间和即可。

## I. Prefix-Free Queries

题意：给出一个长度为$n$的字符串$s$。有$q$个询问，每次给出$k$个子串$s[l_1, r_1], s[l_2, r_2], \dots, s[l_k, r_k]$和一个整数$m$。求出$2^k$种选法里面有多少个满足任意两个互相不是对方前缀，对$m$取模。

$1 \le n, q, \sum k \le 4 \cdot 10^5, 2 \le m \le 10^9, 1 \le l_j \le r_j \le n$

题解：直接建出虚树，然后在上面dp。
