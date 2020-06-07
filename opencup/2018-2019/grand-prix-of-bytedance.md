# XIX Open Cup. Stage 13. Grand Prix of Bytedance

+ [ ] [A. Algorithm Was Applied](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/A/)
+ [x] [B. Balanced Rainbow Sequence](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/B/)
+ [ ] [C. Called Convergient](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/C/)
+ [ ] [D. Doesn’t Contain Loops or Multiple Edges](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/D/)
+ [ ] [E. Equal Adjacent Elements](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/E/)
+ [ ] [F. Formally, You Choose Three Integers](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/F/)
+ [ ] [G. Game](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/G/)
+ [ ] [H. Hat With An Integer](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/H/)
+ [ ] [I. Intersect With Other Balls](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/I/)
+ [ ] [J. $J$ The Attacker Has](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/J/)
+ [ ] [K. $K$ Integers](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/K/)
+ [ ] [L. Labeled Connected Graphs](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/L/)
+ [ ] [M. Moves You Need to Make](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/M/)
+ [ ] [N. Number Of Vertices](https://official.contest.yandex.ru/opencupXIX/contest/12091/problems/N/)

## B. Balanced Rainbow Sequence

题意：你有一个长度为$n$的括号序列$s$，第$i$个括号颜色$c_i$是$0$或者$1$或者$2$。现在你可以修改某些括号，使得

+ 删掉每个颜色为$0$个括号后，剩下的括号序列合法
+ 删掉每个颜色为$1$个括号后，剩下的括号序列合法

求出最小操作次数。

$1 \le n \le 6000$

题解：把`(`和`)`分别看成$1$和$-1$，假设最终颜色$2$对应的括号序列和为$balance$，那么显然其他颜色对应的括号序列和为$-balance$。我们不妨先把这些括号序列的和调对，显然只修改前缀的左括号或者后缀的右括号是最优的。

接下来我们做得任何修改都得保证括号序列的和不变，也就是说每改一个左括号都得同时修改一个右括号，反之亦然。显然修改最前面若干个右括号和最后面若干个左括号是最优的。那我们考虑什么时候是需要修改的。

先考虑颜色$0$和$2$构成的括号序列，从左往右考虑，如果存在一个前缀的和为负，不妨假设为$t$。那么我们需要修改，使得这个和变成非负。假设左侧不同颜色右括号个数为$close_0$和$close_2$，右侧不同颜色的左括号个数为$open_0$和$open_1$，总共颜色$0$的改了$2L$次，颜色$2$的改了$2B$次，那么有$\min(L, close_0, open_0) + \min(B, close_2, open_2) \ge \lceil -\frac{t}{2} \rceil$。

对于颜色$1$和$2$构成的括号序列也有$\min(G, close_0, open_0) + \min(B, close_2, open_2) \ge \lceil -\frac{t}{2} \rceil$。最后把式子展开其实可以得到$L$，$G$，$B$，$L+B$和$G+B$的最小值。我们可以$O(n)$求出这些值，不妨依次设为$a_L,a_G,a_B,a_{LB},a_{GB}$，那么显然取$L=a_L,G=a_G,B=\max(a_B,a_{LB}-a_L,a_{GB}-a_G)$的时候取到$L+G+B$的最小值。

事实上这些最小值可以表示成$\lceil -\frac{t}{2} \rceil-open_{\cdot}$或者$\lceil -\frac{t}{2} \rceil-close_{\cdot}$的最大值，我们把$balance$从$-n$枚举到$n$的时候，其实可以$O(\log n)$求出这些最值的。