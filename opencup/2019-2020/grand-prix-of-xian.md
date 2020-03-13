# 2019 ICPC Asia-East Continent Final

+ [ ] [A. City](https://codeforces.com/gym/102471/problem/A)
+ [ ] [B. Black and White](https://codeforces.com/gym/102471/problem/B)
+ [ ] [C. Dirichlet $k$-th root](https://codeforces.com/gym/102471/problem/C)
+ [ ] [D. Fire](https://codeforces.com/gym/102471/problem/D)
+ [ ] [E. Flow](https://codeforces.com/gym/102471/problem/E)
+ [ ] [F. Game](https://codeforces.com/gym/102471/problem/F)
+ [ ] [G. Happiness](https://codeforces.com/gym/102471/problem/G)
+ [ ] [H. King](https://codeforces.com/gym/102471/problem/H)
+ [ ] [I. Moon](https://codeforces.com/gym/102471/problem/I)
+ [ ] [J. Permutation](https://codeforces.com/gym/102471/problem/J)
+ [x] [K. All Pair Maximum Flow](https://codeforces.com/gym/102471/problem/K)
+ [ ] [L. Travel](https://codeforces.com/gym/102471/problem/L)
+ [ ] [M. Value](https://codeforces.com/gym/102471/problem/M)

## K. All Pair Maximum Flow

题意：有一个$n$个点的凸边形，其中有若干条对角线有边相连，这些边构成了一个平面图。现在给出所有$m$条边，求出任意两点最大流之和，对$998245343$取模。

$3 \le n \le 200000, n \le m \le 400000, 1 \le u, v \le n, 0 \le w \le 10^9$

题解：可以观察到我们如果取最外面的面上一条权值最小的边$e$，然后考虑包含这条边的一个环，我们把$e$删掉，然后把$e$的边权加到这个环上其他边上。容易发现这样是不改变整个图任意两点的最大流的。因此可以重复这个过程直到不存在环，我们就得到了一棵树。这个时候任意两个点的最大流就是路径上的最小值。按照边权从大到小枚举，然后并查集维护连通块大小即可。