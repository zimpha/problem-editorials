# PA 2002 November

+ [x] [Zadanie próbne (Round 0)](https://szkopul.edu.pl/problemset/problem/-Yhja_E7nBBN6gSmjxYOjVnj/site/)
+ [x] [Szyfr (Round 1)](https://szkopul.edu.pl/problemset/problem/JeZXAV_m6RvyN6ANWz7nDDJJ/site/)
+ [x] [Patyki (Round 2)](https://szkopul.edu.pl/problemset/problem/oNbyTvJCeUiCiIjsWuttQFfV/site/)
+ [x] [Tarasy (Round 2)](https://szkopul.edu.pl/problemset/problem/db7CAaN84by8p8oO4jeomOBv/site/)
+ [x] [Autostrady (Round 3)](https://szkopul.edu.pl/problemset/problem/n2hIcEYC7gFElcM3bEmLPa6S/site/)
+ [x] [Turniej (Round 3)](https://szkopul.edu.pl/problemset/problem/csRyGSzEudhfA_ptvAurOVFH/site/)
+ [x] [Blokada (Round 4)](https://szkopul.edu.pl/problemset/problem/nqgsdR6MkTktozE1FA8s3R-z/site/)
+ [x] [Gra Fibonacziego (Round 4)](https://szkopul.edu.pl/problemset/problem/2Q9yGSHjU6O1EyeQKSt8CtPi/site/)
+ [x] [Korekcja błędów (Round 4)](https://szkopul.edu.pl/problemset/problem/TxDGz-wo3oHz_0kFsoZX-IuI/site/)
+ [x] [Widoczność (Round 4)](https://szkopul.edu.pl/problemset/problem/j7MIw_8xnVjBrBy-zbqA8BbH/site/)
+ [x] [Logo (Round 5)](https://szkopul.edu.pl/problemset/problem/u19I1ez5a1zBfvWvGwEI2usC/site/)
+ [x] [Pająki (Round 5)](https://szkopul.edu.pl/problemset/problem/NHHMwzZ6W57lyd5nDUCQKdZ7/site/)
+ [x] [Sojusz (Round 5)](https://szkopul.edu.pl/problemset/problem/RTQUjjG9QKc1yMi2kg5Y3zAk/site/)

## Round 0

### Zadanie próbne (pro)

题意：给个字符串，翻转后输出。

题解：略

## Round 1

### Szyfr (szy)

题意：$fib_1=fib_2=1, fib_n=fib_{n-1}+fib_{n-2}$，输出$fib_n$到$fib_m$的个位数。

$0 < n < m < 10^7$

题解：略

## Round 2

### Patyki (pat)

题意：给$n$个数，每次选择两个相同的数$x$，删掉加入$2x$，问最后剩下多少个数。

$1 \le n \le 10^5$

题解：从小到大模拟即可。

### Tarasy (tar)

题意：有$n$个山，高度分别为$h_1,h_2,\dots,h_n$。如果相邻位置高度比你小，那么可以随便走；如果相邻位置高度比你高，那么你得花高度差的钱。你有$k$元，求最多能访问多少位置。

$1 \le n \le 20000, 0 \le k \le 20000, 1 \le h_i \le 10000$

题解：只需要考虑从左往右，或者从右往左，处理出走一步的代价，用two pointers计算即可。

## Round 3

### Autostrady (aut)

题意：给个$n$个点$m$条边的带权无向图，求个生成树，使得最长边最小。

题解：按照边权排序后直接kruskal

### Turniej (tur)

题意：给个$n$个点$m$条边的有向无环图，求字典序最小的拓扑排序。

题解：略

## Round 4

### Blokada (blo)

题意：给出一个$n$个点，$m$条边的有向图，求$1$到$n$的最小割。

$1 \le n \le 10^4$

题意：蒯了个Min25的最高标号预流推进

### Gra Fibonacziego (gra)

题意：定义fibonacci word是：$f_1=a,f_2=b,f_i=f_{i-2}f_{i-1}$。给出一个字符串$s$，两个人玩游戏，每次可以选择一个fibonacci word后缀删掉，不能操作的输，问先手必胜还是必败。

$1 \le |s| \le 10^5$

题解：只有$O(\log |s|)$个fibonacci word，直接暴力dp即可。

### Korekcja błędów (kor)

题意：给出$n$个字符的编码$e_i$，现在给你一个编码后的字符串$s$，最多有一个字符是错的，要求还原原始消息。

$1 \le n \le 26, 1 \le |e_i| \le 150, 1 \le |s| \le 10^4$

题解：直接dp就好。

### Widoczność (wid)

题意：给出$n$个数$a_1,a_2,\dots,a_n$，一对数$(i,j)$直接可见，当且仅当$[i+1,j-1]$里的数都比$\min(a_i,a_j)$小。一对数$(i,j)$间接可见，当且仅当：1. $(i,j)$直接可见，或者2. 存在$k, i \le k \le j$，$(i,k)$和$(k,j)$都直接可见。求间接可见的数对$(i,j)$的个数。

$1 \le n \le 40000, -1000000 \le a_i \le 1000000$

题解：首选可以用单调队列处理出所有直接可见的数对$(i,j)$，令$cl_i$表示在$i$左边和$i$直接可见的数对个数，$cr_i$表示在$i$右边和$i$直接可见的数对个数。显然答案就是
$$\sum_{i=1}^{n} cl_i \cdot cr_i - \sum_{1 \le i < j < k \le n}[(i,j), (j, k), (i, k)\text{互相可见}]$$

后者就是数个三元环个数。

## Round 5

### Logo (log)

题意：给出一个$x \times y$的`01`格子，然后有$n$个$3 \times 3$的`01`格子，要求用最少的$3 \times 3$格子覆盖，你可以任意翻转+旋转+平移。

$1 \le n \le 5, 1 \le x \le 55, 1 \le y \le 5$

题解：构造出所有可能的pattern，然后逐格状态压缩dp即可。复杂度$O(nxy2^{3y})$

### Pająki (paj)

题意：给出两个$n$个点的平面图，每个面都是等边三角形，判断它们是否同构。

$3 \le n \le 20000$

题解：找出所有三元环，构造每个点的坐标，然后通过翻转+旋转+平移判定是否同构。

### Sojusz (soj)

题意：给出一个左侧$n$个点，右侧$m$个点的二分图，求最小边覆盖。

$1 \le n, m \le 2000$

题解：非孤立点个数-最大匹配
