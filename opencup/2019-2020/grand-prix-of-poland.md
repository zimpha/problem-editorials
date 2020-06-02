# XX Open Cup. Stage 8. Grand Prix of Poland / AMPPZ 2019

+ [ ] [A. Assimilation]
+ [ ] [B. Little Worm]
+ [ ] [C. Polygon]
+ [ ] [D. Frogs]
+ [ ] [E. The Great Drone Show]
+ [ ] [F. Fantastic Compression]
+ [ ] [G. Bookstore]
+ [ ] [H. Cheese Game]
+ [ ] [I. Harry Potter and the Palindromic Radius]
+ [ ] [J. Antennas]
+ [ ] [K. Ghost]
+ [ ] [L. Donuts]

## K. Ghost

题意：有$n$个矩形，第$i$个左下角为$(x_1,y_1)$，右上角为$(x_2,y_2)$，速度为$(v_x,v_y)$。有$q$个询问，每次给出一个时间区间$[l, r]$，求出在这个区间内所有矩形面积交的最大值。

$1 \le n,q \le 10^5, -10^6 \le x_1 < x_2 \le 10^6, -10^6 \le y_1 < y_2 \le 10^6, -10^6 \le v_x, v_y \le 10^6, 0 \le l \le r \le 10^6$