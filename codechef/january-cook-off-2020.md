# January Cook-Off 2020

+ [x] [Chefina and Sums](https://www.codechef.com/COOK114A/problems/CFINASUM)
+ [x] [Count It](https://www.codechef.com/COOK114A/problems/CNTIT)
+ [x] [Almost Palindromic](https://www.codechef.com/COOK114A/problems/PLIND)
+ [x] [Profitable Paths](https://www.codechef.com/COOK114A/problems/PRT)
+ [x] [Range AND](https://www.codechef.com/COOK114A/problems/RGAND)

## Chefina and Sums

题意：给出$N$个数$A_1,A_2,\dots,A_N$，对于每个$k$，考虑如下过程：

+ 令$B_k=0$，对于其他$i \ne k$的$i$，$B_i=A_i$

+ 令$f(k)$是把$B$分成两个和相同连续序列的方案数

求出$f(1)+f(2)+\dots+f(k)$。

$2 \le N \le 2 \cdot 10^5, 1 \le |A_i| \le 10^9$

题解：对于每个$k$，假设当前总和为$S_k$，也就是考虑$1$到$k$的前缀和里有多少是$\frac{S_k}{2}$，以及$k$到$N$的后缀和里有多少是$\frac{S_k}{2}$即可。正着枚举一遍统计前者，倒着枚举一遍统计后者即可。

## Count It

题意：给出$N$个点的树，每条边上有一个$1$到$K$的权值。求出有多少条路径满足：令$S=(S_1,S_2,\dots,S_K)$，其中$S_i$表示路径上权值为$i$的边的条数。使得$S$能够构成一个简单多边形。

$1 \le N \le 2 \cdot 10^5, 1 \le K \le 10$

题解：一堆数能够组成一个多边形，当且仅当最长边小于其他边的和。我们先算不合法的，用总数减掉。枚举权值$i$作为最长边。考虑树分治以及跨过重心的两个点$t$和$s$，假设他们对应的权值序列为$T=(T_1,T_2,\dots,T_K)$和$S=(S_1,S_2,\dots,S_N)$。也就是说要$2(S_i+T_i) > dist(s, t)$。这个排个序后很容易计算。

## Almost Palindromic

题意：给出两个整数$L$和$R$，求出区间里有多少整数$x$，可以重排得到一个回文串。

$1 \le L \le R \le 10^{10^6}$

题解：令$cnt(d)$表示数字$d$出现的次数。那么只要最多有一个数字出现奇数次即可。

先转化成求$[1,R]$内$x$的个数，然后枚举从哪个位置开始变小，这样就可以得到一个$cnt(\cdot)$数组。接下来枚举哪一个数字出现奇数次，然后就是简单计数下即可。

## Profitable Paths

题意：有一棵$N$个点的树，和一个长度为$N$的序列$A_1,A_2,\dots,A_N$。考虑选取一个$\{1,2,\dots,N\}$的排列$p_1,p_2,\dots,p_N$，令节点$i$的权值为$A_{p_i}$。

只考虑从叶子到叶子的路径，求出一个排列使得这些路径的权值和最大。对$10^9+7$取模。

题解：首先求出$cnt(i)$表示节点$i$对答案的贡献，然后按照排序不等式，按照$cnt(i)$的大小依次赋值即可。

## Range AND

题意：给出$L$和$R$，求出$S=\sum_{i=L}^{R} (L \land (L+1) \land \dots \land i)$，对$10^9+7$取模。

$1 \le L \le R \le 10^{18}$

题解：按位处理即可。
