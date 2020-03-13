# Codeforces Round #621 (Div. 1 + Div. 2)

+ [ ] [A. Cow and Haybales](https://codeforces.com/contest/1307/problem/A)
+ [ ] [B. Cow and Friend](https://codeforces.com/contest/1307/problem/B)
+ [ ] [C. Cow and Message](https://codeforces.com/contest/1307/problem/C)
+ [ ] [D. Cow and Fields](https://codeforces.com/contest/1307/problem/D)
+ [ ] [E. Cow and Treats](https://codeforces.com/contest/1307/problem/E)
+ [ ] [F. Cow and Vacation](https://codeforces.com/contest/1307/problem/F)
+ [ ] [G. Cow and Exercise](https://codeforces.com/contest/1307/problem/G)

## A. Cow and Haybales

## B. Cow and Friend

## C. Cow and Message

## D. Cow and Fields

题意：给出$n$个点$m$条边的连通无向图，有$k$个红点。你现在可以选两个红点加一条边，使得$1$到$n$的最短路最长。

$2 \le n \le 200000, n-1 \le m \le 200000, 2 \le k \le n$

题解：求出$1$到红点距离$x_i$以及$n$到红点距离$y_i$。然后我们要找个$i$和$j$，使得$\min(x_i + y_j, x_j + y_i)$最大。

不妨令$x_i + y_j \le x_j + y_i$，也就是说$x_i - y_i \le x_j - y_j$。然后按照$x_i-y_i$排个序即可。

## E. Cow and Treats

## F. Cow and Vacation

## G. Cow and Exercise