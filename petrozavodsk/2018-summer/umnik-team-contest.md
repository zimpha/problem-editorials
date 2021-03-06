# Petrozavodsk Summer 2018. Day 1. t.me/umnik_team Contest

+ [x] [A. Ciphertext](https://acm.timus.ru/problem.aspx?space=1&num=2118)

## A. Ciphertext

题意：有一个大小为$k$的字符集，用`A-Za-z`依次标号。这$k$个字符用`prefix code`来编码。现在有一个字符串$s$，你需要把$s$编码后的字符串划分成最多的段，使得每段都不能解码。

$1 \le k \le 52, 1 \le |s| \le 10^6$

题解：可以发现如果编码里同时有`0`和`1`，那么答案显然是`-1`；如果同时没有`0`和`1`，显然答案是编码后字符串长度。接下来不妨假设有`0`存在，那么显然其他编码都不是以`0`开头的。那么如果我们找到了一个最短的不能被解码的后缀，那么前缀里每个`1`都可以和它前面的一串`0`一起切出去。然后这个后缀可以通过AC自动机来求。