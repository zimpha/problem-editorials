# Petrozavodsk Summer 2016. Day 7. Ural FU Dandelion Contest

+ [ ] [A. Square Function]
+ [ ] [B. Guess by Remainder]
+ [ ] [C. Subtract if Greater!]
+ [ ] [D. Eastern Subregional]
+ [ ] [E. K-transform]
+ [x] [F. Suffix Array for Thue-Morse]
+ [ ] [G. XOR Tree]
+ [ ] [H. Fence]
+ [ ] [I. Friends and Berries - 2]
+ [ ] [J. Oleg and Cola]
+ [x] [K. Process with Constant Sum]

## F. Suffix Array for Thue-Morse

题意：$k$阶`Thue-Morse string`是长度为$2^k$的串，如果$i-1$二进制表示里$1$的个数是偶数，那么第$i$个字符为`A`，否则为`B`。

给出$q$个数，$p_1,p_2,\dots,p_q$，求出$suf[p_1],suf[p_2],\dots,suf[p_q]$。

$0 \le k \le 60, 1 \le q \le 10^5$

题解：考虑构建出$k$阶`Thue-Morse string`后缀自动机，可以参考论文“On the structure of compacted subword graphs of Thue–Morse words and their applications”。

然后只需要在这个后缀自动机上走就可以求出$suf[q_i]$。

## K. Process with Constant Sum

题意：对于一个数组，考虑如下两个操作：1. $a_i \leftarrow a_i - 2$, $a_{i+1} \leftarrow a_{i+1} + 2$; 2. If $a_{i+1} = 0$: $a_i \leftarrow a_{i}-1$, $a_{i+2} \leftarrow a_{i+2}+1$。

可以发现执行若干次后，就不能再执行了。

现在有个长度为$n$的数组$b$和$q$个询问：

+ 把$b_p$修改成$x$
+ 令$a=b[l,r]$，求出如何操作，才能使得操作次数最多并且最终数组里面$0$的个数最多。

$1 \le n, q \le 2 \cdot 10^5, 1 \le p \le n, 0 \le x \le 10^5, 1 \le l \le r \le n$

题解：如果仅考虑`01`序列，可以发现如果两个`1`之间有奇数个`0`，那么他们会变成一个`2`；否则会变成连续两个`1`。这个`2`可以用第一个操作一路放到数列最末尾。

继续分析下去可以发现，最终一个序列会变成`0..0 1..1 s`，即先是连续的`0`，然后是连续的`1`，最后还有一个数$s$。

然后还可以发现，给出两个这样的东西，他们是可以合并的。于是我们可以用线段树来维护这个东西。线段树每个节点维护$(zero, one, sum)$，分别表示`0`的个数，`1`的个数以及最后一个数。

考虑如何合并两个节点$a$和$b$。我们可以先一直应用操作$1$，把$a.sum$尽可能移动到$b.sum$里去。那么$a.sum$会变成`0`或者`1`，可以分别并入到$b.zero$或者$a.one$里面去。也就是变成$(a.zero, a.one)$和$(b.zero, b.one, b.sum)$合并。

注意到如果$b.zero$是偶数的话，$a$里面的`1`可以直接平移过去，也就是最后会得到$(a.zero + b.zero, a.one + b.one, b.sum)$。否则一些`1`会合并。

+ 如果$a.one \le b.one$，若干个$b$里的`1`会消失，最终剩下$b.one-a.one$个`1`。
+ 如果$a.one > b.one$，若干个$a$里的`1`会小时，然后会全部平移到$b$那边，最终剩下$a.one-b.one-1$个`1`。这里减一是因为会有一个`1`平移到最末端去了。

知道`1`个数后，`0`个数和最末端的数字也就很好计算了。

