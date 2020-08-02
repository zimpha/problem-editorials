## XVII Open Cup. Stage 13. Grand Prix of Poland

+ [ ] [A. CNF-SAT](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/A/)
+ [ ] [B. Almost pattern matching](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/B/)
+ [ ] [C. Two Paths](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/C/)
+ [ ] [D. Mushrooms after rain strike back](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/D/)
+ [ ] [E. Epic Battle](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/E/)
+ [ ] [F. Reachability](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/F/)
+ [ ] [G. Reorganization](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/G/)
+ [ ] [H. Matching](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/H/)
+ [ ] [I. Word](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/I/)
+ [ ] [J. Tournament](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/J/)
+ [x] [K. Scale](https://official.contest.yandex.ru/opencupXVII/contest/4227/problems/K/)

## K. Scale

题意：有一个天平，每次显示的读数都会向下取整到最接近$c$的整数倍，并且如果重量大于等于$k \cdot c$的话会报错。现在给出$n$个物品，重量分别为$a_1,a_2,\dots,a_n$。求出有多少对$(x,y)$，能够用天平测出$a_x$的重量一定大于$a_y$的重量。

$1 \le n, k \le 1000, 1 \le c \le 5000, 1 \le a_i < k \cdot c$

题解：考虑两个重量$x$和$y$，他们能够区分$x$比$y$轻当且仅当满足下面某个条件：

1. $x < k \cdot c$并且$y \ge k \cdot c$
2. $x,y < k \cdot c, \lfloor \frac{x}{c} \rfloor < \lfloor \frac{y}{c} \rfloor$

对于一个物品$a_i$，考虑所有$2^n$种可能，我们能够根据是否包含$a_i$分成两个多重集$X_i$和$Y_i$。可以发现，物品$a_i$和$a_j$无法区分当且仅当$X_i=X_j$并且$Y_i=Y_j$。把无法区分的看成等价类，那么我们只需要找出所有的等价类即可。

把$a_i$从小到大排列，对于每个$i$，只需要考虑$a_i$和$a_{i+1}$能否属于同一个等价类即可，因为同一个等价类里的物品在排好序的序列里一定连续。那么$a_i$和$a_{i+1}$可以区分当且仅当能找到一个$x$和$y$，使得

+ $x$是集合$\{a_1,a_2,\dots,a_{i-1}\}$的一个子集和
+ $y$是集合$\{a_{i+2}, a_{i+3}, \dots, a_n\}$的一个子集和
+ $x+y+a_i$和$x+y+a_{i+1}$可以区分。

那么我们可以令$dpL(i,j)$表示前$i$个数里面，满足$x \equiv j \bmod c$的最小$x$，类似$dpE(i,j)$表示后$i$个数里面，满足$y \equiv j \bmod c$的最小$y$。这两个数组很容易求出来。

那么对于一个$i$，我们仅需要拿$dpL(i-1,\cdot)$和$dpR(i+2,\cdot)$来判断即可。第一种判定条件可以枚举$x$，然后二分判定是否存在合法的$y$。第二种判定条件，可以枚举$x$，然后考虑$(\lfloor \frac{x+a_i}{c} \rfloor, (x+a_i) \bmod c)$和$(\lfloor \frac{x+a_{i+1}}{c} \rfloor, (x+a_{i+1}) \bmod c)$的关系即可。