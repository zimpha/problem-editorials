# Codeforces Round #612

+ [x] [Garland](https://codeforces.com/contest/1286/problem/A)
+ [ ] [Numbers on Tree](https://codeforces.com/contest/1286/problem/B)
+ [ ] [Madhouse](https://codeforces.com/contest/1286/problem/C2)
+ [ ] [LCC](https://codeforces.com/contest/1286/problem/D)
+ [ ] [Fedya the Potter Strikes Back](https://codeforces.com/contest/1286/problem/E)
+ [ ] [Harry The Potter](https://codeforces.com/contest/1286/problem/F)

## A. Garland

题意：有一个长度为$n$的排列$p_1,p_2,\dots,p_n$。有些位置未知，你需要把它们填上使得这样的位置$i$最少：$p_i$和$p_{i+1}$的奇偶性不同。

$1 \le n \le 100, 0 \le p_i \le n$

题解：先特判掉全是`0`的情况。然后，对于每一段`0`，显然只有左右两边的位置有用，考虑分成以下几类：

+ `00`：如果不是全`0`的话，答案会$+2$
+ `01`：不管怎么填，我们都能使答案$+1$
+ `11`：如果不是全`1`的话，答案会$+2$
+ `*1`：如果不是全`1`的话，答案会$+1$
+ `*0`：如果不是全`0`的话，答案会$+2$

显然，我们要优先填掉`00`和`11`，然后是`*1`和`*0`。直接按照全`0`段大小从小往大填即可。

## B. Numbers on Tree

题意：有一棵$n$个点的有根树，每个点上有个整数$a_i$。令$c_i$表示子树$i$里满足$a_j < a_i$的$j$的个数。现在给出这棵树和$c$数组，构造一个$a$数组。

$1 \le n \le 2000, 0 \le c_i \le n - 1, 1 \le a_i \le 10^9$

题解：只要$c_i \le size_i$就一定是有解的。然后考虑从根开始填，维护一个变量$min_v$表示这棵子树里每个数最小应该是$min_v$，以及一个数对$(max_v, cnt_v)$表示这棵子树里有$cnt_v$个数要小于$max_v$。

## C. Madhouse

题意：交互题。有一个字符串$s$，你需要用以下询问求出这个串：每次给出$l$和$r$，会返回$s[l..r]$的所有子串。最多只能问$3$次，并且返回来的子串个数之和不超过$\left\lceil 0.777(n+1)^2\right\rceil$。

$1 \le |s| \le 100$

## D. LCC

题意：有$n$俩小车，第$i$俩在位置$x_i$，速度是$v_i$，以$p_i$概率往左开，$(1-p_i)$概率往右开。求出第一次相撞的期望时间。

$1 \le n \le 10^5, -10^9 \le x_i \le 10^9, 1 \le v \le 10^6, 0 \le p_i \le 100$

题解：显然第一次相撞发生在相邻的位置，枚举位置，然后算下概率即可。

## E. Fedya the Potter Strikes Back

## F. Harry The Potter
