# Codeforces Round #594

## A. Ivan the Fool and the Probability Theory

题意：给出$n \times m$的格子，求出多少`01`染色方案数，使得每个位置最多和相邻一个位置颜色一样。

$1 \le n, m \le 100000$

## B. The World Is Just a Programming Task (Hard Version)

题意：给出长度为$n$的括号序列，你可以选择两个位置交换，使得这个串cyclic shift$k$次后是合法括号序列的$k$个数最多，

$1 \le n \le 300000$

## C. Queue in the Train

题意：有$n$个人，第$i$个人会在时刻$t_i$去拿水，拿水需要花时间$p$。第$i$个人，会观察第$1$到第$i-1$这些人是否在拿水，如果没有的话他会去，否则他会继续等待。求出每个人最后会在什么时刻拿到水。

$1 \le n \le 10^5, 1 \le p \le 10^9, 0 \le t_i \le 10^9$

## D. Catowice City

题意：有$n$个人和$n$只猫，第$i$只猫住在第$i$个人家里。给出$m$对关系，表示第$a_i$个人认识第$b_i$只猫。现在要选出$x$个人当裁判，$n-x$只猫当选手。要求任意一个裁判都不认识选手。

$1 \le n \le m \le 10^6$

## E. Turtle

题意：给出$2 \times n$的数组$a$。你可以重排里面的元素，使得从$(1,1)$到$(2,n)$的最长路最小，每次可以向下或者向右走。

$2 \le n \le 25, 0 \le a_{1,i}, a_{2,i} \le 50000$

## F. Swiper, no swiping!

题意：给出一个$n$个点$m$条边的无向图。你需要选择一个非空点集删掉，使得每个点度数模$3$的值不变。

$1 \le n, m \le 500000$
