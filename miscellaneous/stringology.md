# 字符串科技

+ [x] [To Queue or not to Queue](https://www.codechef.com/problems/TMP01)
+ [x] [Chef and Substrings](https://www.codechef.com/problems/GERALD3)
+ [x] [Sasha and swag strings](https://acm.timus.ru/problem.aspx?space=1&num=1799)
+ [x] [How Many Substrings?](https://www.hackerrank.com/contests/w27/challenges/how-many-substrings/problem)
+ [x] [Incomparable Pairs](https://codeforces.com/gym/102129/problem/I)
+ [ ] [String](http://acm.hdu.edu.cn/showproblem.php?pid=5891)
+ [ ] [Sum of Squares of the Occurrence Counts](https://official.contest.yandex.ru/opencupXVIII/contest/7389/problems/I/)
+ [ ] [Substrings on a Tree](https://www.codechef.com/problems/TSUBSTR)
+ [ ] [Two Strings Game](https://www.hackerrank.com/challenges/two-strings-game/problem)
+ [ ] [Alice and Bob (and string)](https://www.hackerrank.com/contests/worldcupfinals/challenges/str-game)
+ [ ] [Alice and Bob and a string](https://acm.timus.ru/problem.aspx?space=1&num=1897)
+ [ ] [Cyclical Quest](https://codeforces.com/contest/235/problem/C)
+ [ ] [Mikhail’s Problem](https://official.contest.yandex.ru/opencupXVIII/contest/4961/problems/H/)
+ [ ] [Palindromic Magic](https://codeforces.com/problemset/problem/1081/H)
+ [ ] [【集训队作业2018】串串](http://uoj.ac/problem/433)
+ [ ] [Double Palindrome](https://codeforces.com/gym/102411/problem/D)
+ [ ] [Dynamic string complexity](https://acm.timus.ru/problem.aspx?space=1&num=2137)
+ [ ] [Deep Purple](https://codeforces.com/gym/100962/submit/D)
+ [ ] [Speckled Band](https://codeforces.com/problemset/problem/1043/G)
+ [x] [Lexicographically Smallest String](https://contest.yandex.com/contest/1299/problems/F/)
+ [ ] [Cutting the Line](https://codeforces.com/problemset/problem/594/E)
+ [ ] [Rap God](https://codeforces.com/problemset/problem/786/D)
+ [ ] [Fibonacci Words](https://szkopul.edu.pl/problemset/problem/hJrxkE_IQ4fs1YaX7Gm6UZk2/site/?key=statement)
+ [ ] [【CTSC2016】萨菲克斯·阿瑞](http://uoj.ac/problem/199)
+ [ ] [Tiles](https://szkopul.edu.pl/problemset/problem/NfLo0jGGrAUebGy5-3gJO_Re/site/?key=statement)
+ [ ] [You Are Given Some Letters...](https://codeforces.com/problemset/problem/1202/F)
+ [x] [模式串查找](https://loj.ac/problem/3194)

## 后缀结构

### To Queue or not to Queue

题意：一开始有个空字符串，有$Q$个操作，每次在末尾加一个字符或者删掉前面一个字符。操作结束后输出本质不同子串个数，对$10^9+7$取模。

$1 \le Q \le 10^6$

题解：先从这个[回答](http://stackoverflow.com/a/9513423)里学习后缀树的构建过程。

然后回到这个题。我们在构建后缀树的同时维护当前的叶子数，那么本质不同子串就很好维护了。考虑删除一个字符，我们需要把当前最长的后缀删掉。基本上是要从叶子开始，把度数为$2$的点都删掉，直到遇到了`active point`或者遇到一个度不是$2$的点。

如果当前遇到了一个`active point`。这个时候，我们考虑是不是还有后缀要插入，也就是`remain`的值是不是$0$。如果没有就做完了；否则我们还需要处理`active point`。具体有以下两种情况：

+ `active point`是叶子，并且当前的后缀已经处理掉了。我们只要把这个叶子的边对应的子串该对即可。
+ 当前这个后缀对应的下一条边不在后缀树上，我们需要创建一个新的节点。这个时候我们也解决掉了一个后缀。

因此在这两种情况下，我们都还需要更新下`active point`。

复杂度$O(Q)$。

这题还可以用后缀数组+线段树来做。基本思想就是维护当前所有后缀的排序结果。复杂度$O(Q \log Q)$。

### Chef and Substrings

题意：给出一个长度为$n$的字符串$s$和$m$个询问。每次给出一个区间$l_i,r_i$，求出所有起点在$[l_i,r_i]$内的本质不同子串个数。

$1 \le n, m \le 50000$

题解：我们如果从右往左依次加入每个后缀，然后能够快速维护$cnt(x)$表示第一次出现位置在$x$的子串个数。那么每次询问其实就是对$cnt[l_i..r_i]$求和。

考虑从右往左依次加入字符构建一个后缀自动机。假设加入字符$s_i$后落在节点$u^i$上，考虑$u^i$沿着`suffix link`走到根的这条路径，显然这些节点对应的字符串都是以$i$为左端点的，也就是说$cnt(i)$要加上$n-i$。同时我们还需要减去一些$cnt(j)$，因为路径上这些点原先对应的字符串原先左端点是另一个数$j$。

不妨在后缀自动机上记录一个$mx$表示这个点当前的左端点是谁。然后一个节点$u$对应的左端点就是$u$这棵子树里面$mx$的最小值。对于每个左端点$x$，维护$up(x)$，表示从$u^x$出发往上一直走到$up(x)$这些节点的左端点都是$x$。

那么每次加入一个字符$s_i$后，只需要利用$up(\cdot)$数组，快速找到一段左端点相同的路径，不妨假设左端点为$j$，这条路径长度为$len$，那么把$cnt(j)$减去$len$即可。

这样每次暴力修改，复杂度均摊是$O(n \log n)$的。每次修改，还需要用线段树或者树状数组维护区间和，总的复杂度是$O(n \log^2 n)$。

### Sasha and swag strings

题意：给出一个长度为$n$的字符串$s$，考虑构建它的后缀树，求出后缀树上每条边对应的字符串里的本质不同子串个数。

$1 \le n \le 10^5$

题解：先建出后缀树，然后扣出每条边对应的区间。最后套用`How Many Substrings?`的做法，复杂度$O(n \log^2 n)$。

据说用`CSAM`可以做到$O(n)$，有待学习。

### How Many Substrings?

题意：给出一个长度为$n$的字符串$s$和$q$个询问。每次给出一个子串，询问子串内本质不同子串个数。

$1 \le n, q \le 10^5$

题解：和`Chef and Substrings`类似，同样是维护当前有多少字符串的左端点是$x$。不过需要从左往右依次加入每个字符。贡献都是对一个区间加$1$或者$-1$。

也许可以做到$O(n \log n)$。

### Incomparable Pairs

题意：给出一个字符串$s$，求出有多少对字符串$(a,b)$使得$a$不是$b$的子串，$b$也不是$a$的子串。并且$a$和$b$都是$s$的一个非空子串。

$1 \le |s| \le 10^5$

题解：转成求$a$是$b$的子串，或者$b$是$a$的子串。

### String

题意：一开始有个字符串$s$，然后有$m$个强制在线的操作：

+ 在末尾加入一个字符
+ 给出区间$[l,r]$，询问$s[l..r]$里的一个最长子串，在$s[l..r]$里出现了至少两次。

$1 \le |s|, m \le 50000$

### Sum of Squares of the Occurrence Counts

题意：有个字符串$s$，对于每个前缀$x$都统计下：$\sum_p f(x,p)^2$，其中$f(x,p)$表示$p$在$x$出现次数。

$1 \le |s| \le 10^5$

### Substrings on a Tree

题意：给出一棵$N$个点的有根树，每个点上有个字符。定义这个树的子串为从上往下走的一条路径。先输出有多少个本质不同的子串。

然后给出$Q$个询问，每次给出$26$个小写字母的排列$P_i$和整数$K_i$，求把所有本质不同子串按照$P_i$给定的字符大小关系排序后，第$K_i$小的子串。

$1 \le N \le 250000, 1 \le Q \le 50000, 1 \le K_i \le 2^{63}-1$

### Two Strings Game

题意：有两个字符串$A$和$B$。一开始有两个串$a$和$b$，分别是$A$和$B$的子串。两个人开始玩游戏。每次可以选择$a$或者$b$，在后面加入一个字符。要求操作结束后，$a$是$A$的子串，$b$是$B$的子串。求出第$k$对必胜的串$(a,b)$。

$1 \le |A|, |B| \le 300000, 1 \le K \le 10^{18}$

### Alice and Bob (and string)

题意：有个字符串$S$。一开始有个串$T$，是$S$个子串。两个人玩游戏，每次可以再$T$的前面加入一个字符。要求操作结束后，$T$仍是$S$的子串。求出字典序第$K$小的必胜串。

$1 \le |S| \le 10^5, 1 \le K \le 10^9$

### Alice and Bob and a string

有个字符串$S$。一开始有个串$T$，是$S$个子串。两个人玩游戏，每次可以同时在$T$的前面和后面加入一个字符(可以不同)。要求操作结束后，$T$仍是$S$的子串。求出字典序第$K$小的必胜串。

$1 \le |S| \le 10^5, 1 \le K \le 10^{10}$

### Cyclical Quest

题意：给出一个字符串$s$，然后又$n$个询问。每次给出一个字符串$x_i$，求出$s$有多少子串和$x_i$循环同构。

$1 \le |s| \le 10^6, 1 \le n \le 10^5, \sum |x_i| \le 10^6$

## 回文

### Mikhail’s Problem

题意：给出一个长度为$n$的字符串$s$和$q$个询问。每次给出一个子串，询问子串内本质不同回文串个数。

$1 \le n, q \le 10^5$

### Palindromic Magic

题意：给出两个串$A$和$B$。选一个$A$的回文子串$a$，$B$的回文子串$b$。求出本质不同的$ab$的个数。

$1 \le |A|, |B| \le 200000$

### 【集训队作业2018】串串

题意：给出一个字符串$s$，求出它有多少本质不同的子串可以由两个回文串拼接而成。

$1 \le |s| \le 500000$

### Double Palindrome

题意：给出$n$和$k$。求出有多少个长度不超过$n$，字符集为$1$到$k$的字符串，它可以由两个回文串拼接而成。

$1 \le n \le 10^5, 1 \le k \le 26$

## Border

### Dynamic string complexity

题意：定义一个字符串的`complexity`为它的所有border的周期的个数。定义一个字符串的`dynamic complexity`为它所有前缀的`complexity`之和。

给出一个`01`串$s$，对于每个$i$ ($1 \le i \le 25$)，求出一个以$s$为前缀的长度为$|s|+i$的`01`串，使其`dynamic complexity`最大。

$1 \le |s| \le 10^5$

### Deep Purple

题意：给出一个长度为$n$的字符串$s$。然后有$q$个询问，每次给出$l_i$和$r_i$，求出$s[l..r]$的最长border。

$1 \le n, q \le 200000, 1 \le l_i \le r_i \le n$

### Speckled Band

题意：给出一个长度为$n$的字符串$s$。然后有$q$个询问，每次给出$l_i$和$r_i$。你需要把$s[l_i..r_i]$切成若干段，使得存在两段相同，且不同的段数最少。

$1 \le n, q \le 200000, 1 \le l_i \le r_i \le n$

## Lyndon Factorization

### Lexicographically Smallest String

### Cutting the Line

## 杂

### Rap God

### Fibonacci Words

### 【CTSC2016】萨菲克斯·阿瑞

### Tiles

### You Are Given Some Letters...

### 模式串查找

参考[ROI 2018/2019](https://github.com/zimpha/problem-editorials/blob/master/russian-olympiad-in-informatics/2018-2019.md)
