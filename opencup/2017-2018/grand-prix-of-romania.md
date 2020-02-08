# XVIII Open Cup. Grand Prix of Romania

- [ ] [A. Balance](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/A)
- [ ] [B. Entanglement](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/B)
- [ ] [C. Gravity](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/C)
- [ ] [D. Infinite Pattern Matching](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/D)
- [ ] [E. Inheritance](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/E)
- [ ] [F. Movies](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/F)
- [ ] [G. Origami](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/G)
- [ ] [H. Qnp](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/H)
- [ ] [I. Salaj](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/I)
- [ ] [J. Taxi](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/J)
- [ ] [K. Tris](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/K)
- [ ] [L. Xormites](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/L)

## B. Entanglement

题意：给出一个$N \times M$的矩阵，求出有多少数组对$(A,B)$满足：

+ $|A|=N,|B|=M$

+ $C_{i,j}=A_i \text{ or }B_j$

+ $A_i,B_j \in \{1,2,\dots,K\}$

$1 \le N, M \le 300, 1 \le K \le NM, 1 \le C_{i,j} \le K$

题解：首先把$C_{i,j}$都离散化，注意到最多只能有$N+M$个值，否则是无解的。接下来考虑逐行确定每个$A_i$的值。

我们维护$r$表示当前处理到了第$r$行，$row_i$表示第$i$行的选定的值，$col_j$表示第$j$列选定的值，同时$ways_i$表示第$i$行每个位置有多少种选择的可能。

对于当前第$r$行，考虑枚举$C_{r,c}$作为这一行的值，那么对于那些$C_{r,c} \ne C_{r,j}$的$j$，可以确定下来$col_j$的值，就是$C_{r,j}$。同时对于那些$i > r$且$C_{i,j} \ne c_{r,j}$的$i$，我们还可以确定一些$row_i$，就是$C_{i,j}$。

当然对于第$r$行，你可以随便选一个不在$C_{r,c}$中出现的数，有$ways_i=K-|C_r|$种可能。这样你也可以确定一些其他$col_j$和$row_i$。

接下来递归进入第$r+1$行，直到$r=N+1$或者每一列都确定了，这个时候你可以计算有多少种可能。首先每个未确定的列都可以乘上$K$，然后每个行都可以乘上$ways_i$。

如果每次递归复杂度能够做到$O(nm)$，其中$n$和$m$分别表示未确定的行数和列数。那么总得复杂度就是$O(N^2M)$的。

## F. Movies

题意：有$N+K$个电影，从$1$到$N+K$编号。你把这些电影分成了两个列表，第一个列表里有$N$个电影，第二个里有$K$个电影。有如下操作：奇数次删掉第一个列表里最大的数，偶数次删掉第一个列表里最小的数；然后从第二个列表里选出一个数插到第一个列表里任意位置。求出最早第几次操作后第一个列表里的数形成了一个递增的序列。

$1 \le N \le 10^5, 1 \le K \le 200000$

题解：
