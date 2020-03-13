# Petrozavodsk Winter 2020. Day 8. Almost Algorithmic Contest

## A. Um nik’s Algorithm

题意：给出左侧$n_1$个点，右侧$n_2$个点，总共$m$条边的二分图。令最大匹配大小为$K$，你需要找出一个匹配大小至少为$0.95K$。

$1 \le n_1, n_2, m \le 2000000$

## B. String Algorithm

题意：给出一个长度为$n$的字符串$s$。对于每个$k$，把$s$砍成$\frac{n}{k}$个长度为$k$的子串，忽略掉多余的小串。然后计算出有多少对子串最多有一个位置不匹配。

$1 \le n \le 200000$

## C. StalinSort Algorithm

题意：给出一个长度为$n$的排列$p_1,p_2,\dots,p_n$。从左往右依次考虑每个数，如果比前一个数大，那么不做任何操作；否则，可以选择删掉这个数，或者在能够有序的基础上删掉上一个数。求出最多能保留多少数。

$1 \le n \le 500000$

