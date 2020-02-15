# XVIII Open Cup. Grand Prix of Romania

- [ ] [A. Balance](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/A)
- [x] [B. Entanglement](https://official.contest.yandex.ru/opencupXVIII/contest/5012/problems/B)
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

题解：考虑枚举第一个列表里面区间$[L,R]$的数必须要留下来，那么现在这个区间里面的数在第一个列表里面必须是递增的。假设在第一个列表里小于$L$的最大数为$x$，大于$R$的最小数为$y$，并且小于$L$的数有$X$个，大于$R$的数有$Y$个。我们肯定要先把这$X+Y$个数都删掉，才能达到排序的目的。

不妨先假设$Y \ge X$，我们删掉一个数的后，要从第二个列表里面拿出一个数加回到第一个列表里面。那么显然一开始尽量加入在$[x+1,y-1]$的数比较好，之后肯定要加入$[0,x]$的数，最后再加入$[y,\infty)$的数。因为这样才能使得操作最优。

不妨设第二个序列里面在$[0,x],[x+2,y-1],[y,\infty)$里的数分别为$U,V,W$。那么在$Y$不断减小的过程中会发生以下几种情况：

+ $X$先变成了$0$，然后$Y$现在非零($Y$如果也是$0$的话就结束了)，这里肯定有$V \ge 2X-1$。这个时候第一个列表中$[0,x]$里的数都被删完了，也就是说随便往$[0,y-1]$里插任何数都能够是它们最终排好序。于是只要看剩下来的$U+V$和$2Y$的大小关系就可以判定是否可行以及算出最小步数。

+ $V$先变成了$0$，那么以后我们加入的数都比$x$小，也就是说$x$肯定不会被删掉，于是随着$Y$的继续变小会发生下面的情况：
  
  + $Y$先变成了$0$，这个时候肯定有$U \ge 2Y$，也就是说第一个列表中$[y,\infty)$的数被删完了，接下来可以随便往$[x+1,\infty)$里插入任何数，总是能排好序的。于是接下里看$2X$和$W$的大小关系就可以判定可行性以及算出最小步数。
  
  + $U$先变成了$0$，于是接下来插入比$y$大的数，于是最终要么$X$变成了$0$，要么$W$先用完。不管哪种情况我们都能过算出来是否可行以及最小步数。

对于$Y < X$的情况，我们按照上面的优先顺序操作完第一步之后，就可以利用对称性转成$Y \ge X$的情况，类似分析下即可。
