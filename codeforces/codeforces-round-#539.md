# Codeforces Round #539

## A. Sasha and a Bit of Relax

题意：
给出$n$个整数$a_1,a_2,\dots,a_n$，求有多少对$(l,r)$满足$r-l+1$是偶数，且$a_l \oplus a_{l+1} \oplus \ldots \oplus a_{mid} = a_{mid + 1} \oplus a_{mid + 2} \oplus \ldots \oplus a_r$

$2 \le n \le 3 \times 10^5, 0 \le a_i < 2^{20}$ 

题解：
显然可以知道$a_l \oplus a_{l+1} \oplus \ldots a_r=0$，等价于求偶数长度且异或和为$0$的子段。

## B. Sasha and One More Name

题意：
给出一个回文串$s$，求最小的$k$，使得能把$s$切成$k+1$份，重排后得到一个和$s$不同的回文串。

$1 \le |s| \le 5000$

题解：
如果$|s|$或$|s|-1$个字符都一样，那么无解。然后，显然答案最多为$2$，只需要判断$1$是否可行，暴力枚举即可。

## C. Sasha and a Patient Friend

题意：
有一个水箱，给出$q$个操作：1. $t$时刻，进水速度变成$s$；2. 删掉$t$时刻的一个事件；3. 拿出$l \le t \le r$之间的所有事件，假设水箱初始水位是$v$，问最早什么时候水箱水位到$0$。

$1 \le q \le 10^5, 1 \le t \le 10^9, -10^9 \le s \le 10^9, 0 \le v \le 10^9, 1 \le l \le r \le 10^9$

题解：

首先可以用Treap维护存在的事件，每次询问的时候扣出这段时间，然后再Treap上二分即可。

Treap的每个节点维护：

1. 当前速度
2. 当前时间
3. 子树对应的时间区间
4. 子树内最左和最右节点的速度
5. 当前子树的最小水位
6. 模拟完当前子树后的水位；

## D. Sasha and Interesting Fact from Graph Theory

题意：

给出$n,m,a,b$，问有多少带标号的无根树，满足：1. 每条边权值在$1$到$m$之间，$a$和$b$之间的距离恰好是$m$。

$2 \le n \le 10^6, 1 \le m \le 10^6, 1 \le a, b \le n, a \ne b$

题解：

枚举$a$和$b$之间边的条数$e$，然后$a$和$b$之间的边可以用组合数来计数，剩下的点套用[Cayley's formula](https://en.wikipedia.org/wiki/Cayley's_formula#Generalizations)。

## E. Sasha and a Very Easy Test

题意：

给出一个数组$a_1,a_2,\dots,a_n$，有$q$个操作:

1. 给$[l,r]$内的数都乘上$x$
2. $a_p$除以$x$，保证能够整除
3. 求$[l,r]$的和

所有操作都对$mod$取模

$1 \le n, q \le 10^5, 2 \le mod \le 10^9+9, 1 \le a_i, x \le 10^5$

题解：

把$x$分解为和$mod$互质的部分，和非互质部分；互质部分直接逆元做出发，非互质部分，维护素因数分解。

## F. Sasha and Algorithm of Silence's Sounds

题意：

题解：
