# Petrozavodsk Winter 2019. 300iq Contest 1

- [ ] [A. Angle Beats](https://codeforces.com/gym/102268/problem/A)
- [ ] [B. Best Subsequence](https://codeforces.com/gym/102268/problem/B)
- [ ] [C. Cool Pairs](https://codeforces.com/gym/102268/problem/C)
- [ ] [D. Dates](https://codeforces.com/gym/102268/problem/D)
- [ ] [E. Expected Value](https://codeforces.com/gym/102268/problem/E)
- [ ] [F. Free Edges](https://codeforces.com/gym/102268/problem/F)
- [ ] [G. Graph Counting](https://codeforces.com/gym/102268/problem/G)
- [ ] [H. Hall’s Theorem](https://codeforces.com/gym/102268/problem/H)
- [x] [I. Interesting Graph](https://codeforces.com/gym/102268/problem/I)
- [ ] [J. Jealous Split](https://codeforces.com/gym/102268/problem/J)
- [ ] [K. Knowledge](https://codeforces.com/gym/102268/problem/K)

## I. Interesting Graph

题意：$n$个点$m$条边的无向图，保证对于任意$7$个点的集合$A$，存在两个点$a,b \in A$，一个点$c \not \in A$，使得$a$到$b$的所有路径都经过$c$。

现在对于$i$从$1$到$n$，求出用$i$种颜色给这个图染色的方案数。

$1 \le n, m \le 10^5, 1 \le a_i, b_i \le n$

题解：这个条件等价于图中每个连通块大小最多为$6$。原因是你如果有一个大小超过$7$的连通块，那么你可以选出一个大小为$7$的连通块来，你找不出这样的$a,b$。如果连通块大小不超过$6$，那么大小为$7$的子集肯定是不连通的，你选$a$和$b$来自不同连通块即可。

因此对于每个连通块，你可以求出$c(x)$表示用$x$中颜色染色的方案数。显然，我们只需要$x$不超过连通块大小就够了。

然后可以发现$c(\cdot)$这个东西本质不同的数目是不多的，差不多只有$70$多个。于是我们可以把$c(\cdot)$一样的一起计算。

枚举总共用$k$种颜色，那么答案就是$\sum_{c} \sum_{i=1}^{|c|} \frac{k! \cdot c(i)}{i!}$。
