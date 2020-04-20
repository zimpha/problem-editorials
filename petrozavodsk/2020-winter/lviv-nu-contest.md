# Petrozavodsk Winter 2020. Day 6. Lviv NU Contest

+ [x] [A. Outlier](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/A6/)
+ [ ] [B. A Math Problem](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/B6/)
+ [ ] [C. A Permutation Problem](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/C6/)
+ [ ] [D. Split in Sets](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/D6/)
+ [ ] [E. The Destruction of the Crystals](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/E6/)
+ [ ] [F. Balls](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/F6/)
+ [ ] [G. Football Match](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/G6/)
+ [ ] [H. Hill](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/H6/)
+ [x] [I. Special Game](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/I6/)
+ [ ] [J. Even More Exciting Game](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/J6/)
+ [ ] [K. Potato Shuffle](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/K6/)
+ [ ] [L. Palindrome](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/L6/)

## A. Outlier

题意：给出一个$n$个点的点集$S$，定义$S$的宽度为包含$S$的两平行线之间的最小距离。现在你可以删掉某个点，求出最小可能宽度。

$5 \le n \le 10^5, -10^7 \le x_i, y_i \le 10^7$

题解：首先我们可以求出$S$的凸包，可以注意到，我们只会删掉凸包上的点。显然这个最小宽度有两种情况：

+ 枚举凸包上一条边$ab$，求出距离这条边最远的点$p$，然后删掉$p$。这时候会有一些新的点成为凸包上的点，求出这些点距离$ab$的最远距离，这个作为新的宽度。
+ 枚举凸包上一个点$p$，然后删掉$p$。这时候会有一些新的边成为凸包上的边，依次枚举这些边，然后求出距离这条边的最远点的距离，这个作为新的宽度。

显然求出边到点的最远距离可以二分，于是难点在于删掉一个点之后如何快速求出新增的点。考虑选取$y$坐标最小且$x$坐标最小的点作为原点$O$，然后把不在凸包上的点做极角排序。考虑你要删掉点$P$，然后$P$前面一个点是$A$，后面一个点是$B$。那么考虑极角序在$OA$和$OB$之间的所有点，如果这个点在三角形$APB$内，那么它可能成为凸包上的点。于是我们可以把这些点拿出来暴力重新求个凸包。因为每个点只会最多被重新计算$3$次，所以暴力的复杂度就是对的。

## B. A Math Problem

题意：给出两个序列$a_1,a_2,\dots,a_n$和$b_1,b_2,\dots,b_m$，定义矩阵$c_{i,j}=\text{lcm}(a_i,b_j)$。现在求出有多少$c_1,c_2,\dots,c_n$和$d_1,d_2,\dots,d_m$，使得$c_{i,j}=\text{lcm}(c_i,d_j)$，对$10^9 + 7$取模。

$1 \le n, m \le 10^5, 1 \le a_i, b_i \le 10^9$

## C. A Permutation Problem

题意：给出一个长度为$n$的排列。你每次需要把每对$(i,j)$都交换一遍，最后使得这个排列排好序。构造一个方案。

$2 \le n \le 1000$

## D. Split in Sets

题意：有$n$个整数$a_1,a_2,\dots,a_n$和$k$个互不相同的盒子。你需要把这个$n$个数分到这$k$个盒子里，要求每个盒子里至少有一个数。一个盒子的代价为盒子里数的`AND`。求出最大代价和，以及能够达到这个最大值的方案数，对$10^9+7$取模。

$1 \le k \le n \le 10^5, 0 \le a_i \le 10^9$

## E. The Destruction of the Crystals

题意：有一个$n \times m$的格子，有$k$个水晶，有$b$个炸弹，其他位置是空地，分别用`k`，`b`和`.`表示。每个炸弹引爆后你可以选择炸掉这一行或者这一列，然后会引爆对应的其他炸弹。你可以选择一个炸弹引爆，求出最多能够炸到多少水晶。

$1 \le n, m \le 3000, 0 \le k+b \le nm$

## F. Balls

题意：有$n$个球，从左往右第$i$个的颜色为$c_i$。每次你可以选择一个连续子序列，然后要求这个子序列里恰好有一个数出现一半以上，然后把不是这个数的位置删掉。你需要操作若干次，使得最后剩下来的球颜色都一样。问最后有哪些颜色可能留下来。

$1 \le n \le 10^5, 1 \le c_i \le 10^9$

## G. Football Match

题意：给出一个长度为$n$个字符串，仅包含`Y`和`N`。你需要给第$i$个位置分配一个$1$到$10000$的权值，要求如果$s_i$是`Y`的话，那么删掉第$i$个位置后，剩下来的位置可以分成两组，每组权值和一样；如果$s_i$是`N`的话，则不行。

$3 \le n \le 50$

## H. Hill

题解：你需要用$n$条线段依次拼接然后连接$(x_0,y_0)$和$(x_n,y_n)$，第$i$条线段的长度为$l_i$。求出这些线段的最高点。

$1 \le n \le 10^5, 1 \le l_i \le 10^6, |x_0|, |y_0|, |x_n|, |y_n| \le 10^6$

## I. Special Game

题意：Dmytryk和Petro玩游戏，有$2n$张从$1$到$2n$的牌，一开始每个人各$n$张。总共进行$n$轮游戏，第一轮Dmytryk先出牌。每一轮，第一个人出一张牌，然后第二个人看到后，出另一张牌，牌面大的人赢。下一轮由赢的人先出牌。每一轮，如果后出的人有能获胜的牌，他一定会出。求出Dmytryk最多能获胜的次数。

$1 \le n \le 1000$

题意：先把把所有数都格子排序一下，我们有$A_1 < A_2 < \dots < A_n$和$B_1 < B_2 < \dots < B_n$。显然如果$A_1 > B_n$或者$A_n < B_1$先手的策略是固定的，都是输或者都是赢。否则先手可以选择输或者赢。

先手如果选择赢的话，那么他就需要找到一个最小的$i$使得$A_i > B_n$，然后后手肯定会直接出$B_1$。显然这个不是一个好的策略，因为这个$A_i$不管在什么时候出都是必胜的，一开始就用掉显然不够好。于是我们应该考虑选择输掉，然后用一张比较小的牌来干掉后手一个比较大的牌，使得我必胜的场次越多越好。

那么假设先手选了一个$A_i$，那么后手策略肯定是选择一个最小的$j$满足$B_j > A_i$。经过分析可以发现，这一轮选出来的$A_i$和$B_j$一定满足$A_i < B_j$并且$i-j$最大。于是每次就是找出这样一对数，然后删掉即可。

## J. Even More Exciting Game

题意：有一个长度为$n$的字符串，Petro和Oleg-Andriy开始玩游戏。每次，要么删掉一个字符，要么把一个字符变成边长字母序的下一个字符，不能操作的输。Oleg-Andriy会连续操作两次。求出最优策略下，Oleg-Andriy或Petro先手的情况下，Petro能否获胜。

题解：每个字符可以看成一堆石子，从$z$到$a$，依次为$1$到$26$，那么每次可以取走一个石子或者取走一堆石子。

$n \ge 4$和$n=2$的情况是一样的。

## K. Potato Shuffle

题意：有$n$个数$a_1,a_2,\dots,a_n$。每次可以选择相邻两个和不超过$k$的位置，交换一下。求出最终有多少种不同的序列出现，对$10^9+7$取模。

$1 \le n \le 10^5, 0 \le k \le 2 \cdot 10^9, 1 \le a_i \le 10^9$

## L. Palindrome

题意：有个长度为$n$的`01`串，每次可以选择一个位置移动到字符串末尾。求出最少操作次数，使得这个字符串变成一个回文串。

$1 \le n \le 300$