# January Challenge 2020

+ [ ] [BRKBKS](https://www.codechef.com/JAN20A/problems/BRKBKS)
+ [ ] [ISBIAS](https://www.codechef.com/JAN20A/problems/ISBIAS)
+ [ ] [OWCAFILE](https://www.codechef.com/JAN20A/problems/OWCAFILE)
+ [ ] [ARMYOFME](https://www.codechef.com/JAN20A/problems/ARMYOFME)
+ [ ] [CHEFARMY](https://www.codechef.com/JAN20A/problems/CHEFARMY)
+ [x] [CHEFPSA](https://www.codechef.com/JAN20A/problems/CHEFPSA)
+ [x] [CHFDORA](https://www.codechef.com/JAN20A/problems/CHFDORA)
+ [x] [DFMTRX](https://www.codechef.com/JAN20A/problems/DFMTRX)
+ [x] [DYNAMO](https://www.codechef.com/JAN20A/problems/DYNAMO)
+ [x] [ENGLISH](https://www.codechef.com/JAN20A/problems/ENGLISH)

## Breaking Bricks

题意：略

题解：略

## Equality

题意：给出一个长度为$N$的数组$A$，保证每个元素两两不同。给出$Q$个询问，每次给出一个区间$[L, R]$，询问区间内极大上升序列和极大下降序列个数是不是一样。

题解：略

## OWCA Files

题意：给出一个长度为$N$的数组$A$。你要选出$K$个数（可以重复选），求出它们的乘积对$P$取模的结果。对于每个$i$，输出有多少方案最后模$P$结果是$i$。

$1 \le N, P \le 259431, 0 \le A_i \le P - 1, 0 \le K \le 10^9+9$，$P$是质数。

题解：求出原根，转成加法问题。之后就是一个FFT。

## Army of Me

题意：有一个长度为$N$的排列$P$。给出$Q$个询问，每次给出一个区间$[L, R]$，询问区间里面最长的好区间。好区间定义为排序后是连续的。强制在线。

$1 \le N, Q \le 500000, 1 \le P_i \le N$

题解：首先有两个性质：两个有交的好区间的交是好区间以及两个有交的好区间的并是好区间。

我们先用线段树预处理出以$i$为左端点的最长好区间的右端点$right_i$，以及以$i$为右端点的最长好区间的左端点$left_i$。

对于一个询问$[L, R]$，我们可以先从左端点开始沿着$right$数组跳，直到超过$R$为止。这个时候，从右端点开始沿着$left$数组跳，直到小于$L$为止。这个时候，根据第一个性质，我们得到留下来的区间是好区间。用ST表加速跳的过程即可。

## Chefland Army

题意：有一个$N$个点的有根树，每个点有个权值$S_i$。然后有个$M \times N$的`01`矩阵$A$。你需要构造一个操作序列，使得能把$S_i$全部变成`0`：

+ 选出$K$个数$a_1,a_2,\dots,a_K$，要求任意一个不是其他的祖先；

+ 选一个正实数$R$，把选出来的点的$S_i$减去$R$；

+ 令$G$是这样的$i$的个数：$A(i,a_1),A(i,a_2),\dots,A(i,A_K)$中至少有一个`1`；

+ 操作代价为$G \cdot R$。

求使得操作总代价最小的操作序列。

$1 \le M \le 16, 1 \le N \le 128, 1 \le S_i \le 100$。

## Chefina and Prefix Suffix Sums

题意：有个长度为$N$的数组$a$，现在告诉你它前缀和$pre_1, pre_2, \dots, pre_N$以及后缀和$suf_1, suf_2, \dots, suf_N$重排后的结果$x_1,x_2,\dots,x_{2N}$。求出有多少个合法的数组$a$，对$10^9+7$取模。

$1 \le N \le 10^5, 0 \le |x_i| \le 10^9$

题解：首先可以对所有数求和，然后除以$N+1$就是数组的总和$S$。接下来就知道如果$x$是一个前缀，那么$S-x$一定是个后缀。也就是$x$和$S-x$的数目一定要一样。对于一组$(x, S-x)$，枚举多少个$x$作为前缀即可。需要特判下$x=S-x$的情况。

## Doraemon

题意：给出一个$N \times M$的矩阵$A$，求出有多少的有序对(某一行的子行，某一列的子列)满足：

+ 这两个序列（子行和子列）的长度相同。

+ 这个长度是奇数。

+ 这两个序列的中间元素相同（它们是矩阵中的同一个元素）。

+ 两个序列都是回文序列。

$1 \le NM \le 10^5$

题解：略

## Doofish Matrix

题意：给出$N$，构造一个$N \times N$的矩阵满足：

+ 矩阵中的每个元素都是$1$到$2N − 1$之间的整数。

+ 对每个$i, j$，($1 \le i \le N, 1 \le j \le 2N − 1$)，整数$j$都出现在第$i$行或第$i$列中。

$1 \le N \le 2000$

题解：考虑使用[Round Robin Tournament](https://en.wikipedia.org/wiki/Round-robin_tournament)

## Chef and Dynamo

题意：略

题解：略

## English

题意：有$N$个单词$W_1,W_2,\dots,W_N$。你需要把它们两两匹配，代价为$\min(l_p,l_s)^2$，其中$l_p$是最长公共前缀，$l_s$是最长公共后缀。你的目的是使代价和最大。

$1 \le N \le 10^5, 1 \le \sum |W_i| \le 10^5$

题解：对于每个单词$W_i$，把第$j$个字符替换为$(W_{i,j}, W_{i, |W_i| - j + 1})$建出trie，然后从叶子开始往上贪心，尽可能匹配即可。
