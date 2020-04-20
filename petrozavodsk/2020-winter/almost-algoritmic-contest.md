# Petrozavodsk Winter 2020. Day 8. Almost Algorithmic Contest

+ [ ] [A. Um nik’s Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/A8/)
+ [ ] [B. String Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/B8/)
+ [ ] [C. StalinSort Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/C8/)
+ [ ] [D. FFT Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/D8/)
+ [ ] [E. Binary Search Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/E8/)
+ [ ] [F. Face Recognition Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/F8/)
+ [ ] [G. Petr’s Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/G8/)
+ [ ] [H. Greedy Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/H8/)
+ [ ] [I. Euclid’s Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/I8/)
+ [x] [J. Closest Pair Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/J8/)
+ [ ] [K. Interactive Algorithm](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/K8/)
+ [ ] [L. Not Our Problem](https://official.contest.yandex.com/ptz-winter-2020/contest/17020/problems/L8/)

## A. Um nik’s Algorithm

题意：给出左侧$n_1$个点，右侧$n_2$个点，总共$m$条边的二分图。令最大匹配大小为$K$，你需要找出一个匹配大小至少为$0.95K$。

$1 \le n_1, n_2, m \le 2000000$

## B. String Algorithm

题意：给出一个长度为$n$的字符串$s$。对于每个$k$，把$s$砍成$\frac{n}{k}$个长度为$k$的子串，忽略掉多余的小串。然后计算出有多少对子串最多有一个位置不匹配。

$1 \le n \le 200000$

## C. StalinSort Algorithm

题意：给出一个长度为$n$的排列$p_1,p_2,\dots,p_n$。从左往右依次考虑每个数，如果比前一个数大，那么不做任何操作；否则，可以选择删掉这个数，或者在能够有序的基础上删掉上一个数。求出最多能保留多少数。

$1 \le n \le 500000$

## J. Closest Pair Algorithm

题意：考虑如下求最近点对的算法，给出$n$个点$(x_0,y_0),(x_1,y_1),\dots,(x_{n-1},y_{n-1})$，求出函数`dist`调用次数的期望。保证没有三点共线。

```
rotate the plane around the origin by a random angle phi
let p be the array of points
sort p by x coordinate in increasing order
ans = INF;
for (int i = 0; i < n; i++) {
  for (int j = i - 1; j >= 0; j--) {
    if (p[i].x - p[j].x >= ans) break;
    ans = min(ans, dist(p[i], p[j]));
  }
}
```

$2 \le n \le 250, -10^6 \le x_i, y_i \le 10^6$

题解：显然$p$的顺序只有$O(n^2)$种。对于某对$(i,j)$，满足$x_i \cdot \cos \phi - y_i \cdot \sin \phi = x_j \cdot \cos \phi - y_j \cdot \sin \phi$的$\phi$是关键点，只有$O(n^2)$个。于是，可以先$O(n^2)$枚举一个顺序。

对于一个固定的顺序$q_1,q_2,\dots,q_n$。定义$D(q_i,q_j)$是上述做法枚举到$(i,j)$时$ans$的值。那么函数`dist`调用次数就是
$$
\sum_{i=0}^{n-1}\sum_{j=0}^{n} [(x_i \cdot \cos \phi - y_i \cdot \sin \phi) - (x_j \cdot \cos \phi - y_j \cdot \sin \phi) < D(i,j)]
$$

考虑$q$里两个相邻元素发生交换后$D(\cdot,\cdot)$会发生的变化。显然$D(q_i,q_j)$可以表示为某个子集的最近点对，如果我们交换了$q_k$和$q_{k+1}$的位置，那么可以发现发生变化的$D(q_i,q_j)$一定满足$q_i=q_k$或者$q_i=q_{k+1}$或者$q_j=q_k$或者$q_j=q_{k+1}$。对于这些位置我们可以$O(n)$暴力重新计算。

然后可以发现$\phi$从$0$变成$2\pi$的时候，只有$O(n^2)$种$q_k$和$q_{k+1}$会发生交换。因此计算所有可能的$D(\cdot,\cdot)$的复杂度是$O(n^3)$的。对于固定的$D(i,j)$，然后对于它所有可能的值，以及对应的$\phi$所在区间，我们可以算出满足$(x_i \cdot \cos \phi - y_i \cdot \sin \phi) - (x_j \cdot \cos \phi - y_j \cdot \sin \phi) < D(i,j)$的范围。

于是可以在$O(n^3)$的复杂度内算出期望调用次数。