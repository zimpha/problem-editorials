# Petrozavodsk Winter 2017. Day 3. U of Tokyo Selection 1

+ [x] [A. Spanning Trees]
+ [x] [B. Triangle]
+ [x] [C. Boxes and Balls](https://atcoder.jp/contests/utpc2011/tasks/utpc2011_8)
+ [ ] [D. Bit Operations]
+ [ ] [E. Randomized Binary Search Tree]
+ [x] [F. Election]
+ [ ] [G. Hash]
+ [x] [H. K-th String]
+ [ ] [I. Shortest Path Queries]
+ [ ] [J. Kitamasa’s Counterattack]
+ [x] [K. Wrapping]
+ [ ] [L. Ascending Tree]

## C. Boxes and Balls

题意：有$m$个箱子和$n$个球，第$i$个球的重量是$w_i$, 初始时所有的箱子都是空的. 另有一个长度为$k$的指令序列$a_i$, 你要执行$k$次操作， 第$i$次操作如下：如果存在一个箱子里包含球$a_i$, 那么这轮不用操作, 否则你需要选择一个箱子，把球$a_i$放进去, 并支付代价$w_{a_i}$. 如果选择了一个已经装有箱子的球， 那么你得先把这个箱子清空。求最小的操作代价和。

$1 \le m \le 10, 1 \le n,k \le 10^4, 1 \le w_i \le 10^4, 1 \le a_i \le n$

题解：考虑一个球$x$，在$s$时刻放入，下一次放入的时刻是$t$。如果这个球在$[s,t)$之间一直没有拿出来，那么代价是$0$。否则你可以认为这个球是在$[s+1,t)$里任意一个时刻取出来的，不妨就假设是在$s+1$时刻取出来的。

那么可以发现，对于一个球$x$，它的连续出现的两个位置$s$和$t$，我们要选择区间$[s,t)$或者$[s,s+1)$作为这次停留的区间。对于前者，花费代价是$0$；后者花费代价是$w_x$。并且对于任意时刻，不能超过有$m$个区间覆盖这个时刻。

那么不妨一开始就把所有操作都执行了，然后考虑合并一些操作使得被合并的代价最多。这其实就是等价于，选择了区间$[s+1,t)$，代价为$-w_x$。然后同样时刻下，这样的区间最多有$m-1$个。于是就可以考虑用费用流来解决。

对时间建立$k$个点，从$i$到$i+1$连一条容量为$m-1$，代价为$0$的边；对于$[s+1,t)$这样的区间，从$s+1$到$t$连一条容量为$1$，大家为$-w_x$的边。之后从$1$到$k$跑一个最小费用最大流即可。