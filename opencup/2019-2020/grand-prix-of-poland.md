# XX Open Cup. Stage 8. Grand Prix of Poland / AMPPZ 2019

+ [ ] [A. Assimilation](https://www.acmicpc.net/problem/18042)
+ [ ] [B. Little Worm](https://www.acmicpc.net/problem/18043)
+ [ ] [C. Polygon](https://www.acmicpc.net/problem/18044)
+ [x] [D. Frogs](https://www.acmicpc.net/problem/18045)
+ [ ] [E. The Great Drone Show](https://www.acmicpc.net/problem/18046)
+ [ ] [F. Fantastic Compression](https://www.acmicpc.net/problem/18047)
+ [ ] [G. Bookstore](https://www.acmicpc.net/problem/18048)
+ [ ] [H. Cheese Game](https://www.acmicpc.net/problem/18049)
+ [ ] [I. Harry Potter and the Palindromic Radius](https://www.acmicpc.net/problem/18050)
+ [ ] [J. Antennas](https://www.acmicpc.net/problem/18051)
+ [x] [K. Ghost](https://www.acmicpc.net/problem/18052)
+ [ ] [L. Donuts](https://www.acmicpc.net/problem/18053)

## D. Frogs

题意：有$n$只青蛙，第$i$只在位置$i$，能力值为$s_i$，能够到达位置$[i-r_i,i+r_i]$。你需要找到一个位置，使得存在三只青蛙能够到达，并且这三个能力值之和最大。

$3 \le n \le 200000, 1 \le r_i, s_i \le 200000$

题解：按照区间$[i-r_i,i+r_i]$扫描线，用`std::priority_queue`维护能力。然后就是每次取能力值最大的三个青蛙。

## K. Ghost

题意：有$n$个矩形，第$i$个左下角为$(x_1,y_1)$，右上角为$(x_2,y_2)$，速度为$(v_x,v_y)$。有$q$个询问，每次给出一个时间区间$[l, r]$，求出在这个区间内所有矩形面积交的最大值。

$1 \le n,q \le 10^5, -10^6 \le x_1 < x_2 \le 10^6, -10^6 \le y_1 < y_2 \le 10^6, -10^6 \le v_x, v_y \le 10^6, 0 \le l \le r \le 10^6$

题解：仅考虑$x$坐标，那么每个矩形其实都可以看成两个半平面：$x \le x_2+t \cdot v_x$和$x \ge x_1 + t \cdot v_x$。

我们可以拿这些半平面求出一个半平面交，然后就可以处理出一些区间$[l, r]$，在这些区间里$x = m \cdot t + b$（只需要上凸壳减去下凸壳即可）。为了避免半平面交无限大，需要在左右各加上一个竖线框住这个半平面。

类似的，对于$y$我们也可以处理出这样一些区间。

然后把$x$和$y$的这些区间合并，就得到了在某个区间$[l, r]$里面，最大的矩形面积为$area=a \cdot t^2 + b \cdot t + c$。

预处理每个区间里面的最大面积，然后建立一个RMQ。对于一组询问，可以拆解成完全包含的和部分包含的。对于前者，只需要在RMQ上查询即可；对于后者，我们可以$O(1)$计算出答案。