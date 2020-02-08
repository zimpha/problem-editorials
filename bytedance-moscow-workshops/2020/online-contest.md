# ByteDance-Moscow Workshops Programming Camp 2020, Online Qualification Contest

+ [ ] [A. Add on Prefix]
+ [ ] [B. Best Partition]
+ [ ] [C. Circles Covering]
+ [ ] [D. Domino for Young]
+ [ ] [E. Evil Segments]
+ [ ] [F. Forbidden Triple]
+ [ ] [G. Graph Subpaths]
+ [ ] [H. Happy Cactus]
+ [ ] [I. Invertation in Tournament]
+ [ ] [J. Just Counting]
+ [ ] [K. K Integers]
+ [ ] [L. Long Beautiful Integer]
+ [ ] [M. Modulo Equality]

## G. Graph Subpaths

题意：有一个$n$个点$m$条边的有向无环图。给出其中$k$条路径。

现在对于每个从$2$到$n$的$i$，求出有多少从$1$到$i$的路径，使得任意之前给定的路径不是它的子串。

$3 \le n, m \le 10^5, 1 \le a_i < b_i \le n, 0 \le k \le 50000, \sum l_i \le 10^5$

题解：考虑倒着做，求出$i$到$1$的路径中有哪些是合法的。假设我们把从$i$到$1$的路径全部插到一个`trie`里了，那么这个题其实就做完了。令$t_i$是从$i$出发的所有合法路径构成的`trie`，不包含节点$i$本身。

按照拓扑顺序依次构建每个$t_i$，假设当前处理到了节点$i$，那么对于所有$i$的出边$j$，我们建一条从$t_i$到$t_j$的`trie`边，边上字符为$j$。这样我们就有了一个从$i$出发的`trie`，其中一些从$i$出发的路径可能是不合法的。

接下来需要删掉不合法的路径，对于每条从$i$出发的不合法路径，我们在`trie`上走一遍，把这条路径对应的子树删掉即可。同时`trie`的每个节点维护当前子树的大小。

我们用可持久化数据结构来存储这个`trie`，这样就可以做到$O(n^2)$的复杂度。因为每个点可能有$O(n)$条出边。用可持久化线段树存储所有出边就可以把$O(n)$优化成$O(\log n)$了。

别解：考虑对这$k$条路径建立AC自动机。令$dp(i, j)$表示当前走到了DAG上的点$i$，在自动机上点$j$的合法路径数。可以观察到总得状态数是$O(n + \sum l_i)$的，因为对于一个$i$，如果走到了$j$，则表明存在一条路径某个前缀以$i$结尾。转移的话直接枚举下一个要走的点$k$，同时在自动机上走即可。
