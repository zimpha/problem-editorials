# Codeforces Div 2/Div 3 Selections

## [Codeforces Round #613. F. Classical?](https://codeforces.com/contest/1285/problem/F)

题意：给出$n$个数$a_1,a_2,\dots,a_n$，求出$\text{lcm}(a_i,a_j)$的最大值。

$2 \le n \le 10^5, 1 \le a_i \le 10^5$

题解：考虑枚举$\gcd(a_i,a_j)=g$，接下来只保留$g$的倍数，我们需要找到$\gcd(x,y)=1$且$xy$最大。考虑把剩下来的数从大到小排序，依次处理同时维护一个单调栈。

假设当前处理到$x$，如果栈里存在一个数$y$和$x$互质，那么我们就可以把栈顶元素出栈，并更新下答案。因为$y$肯定大于等于栈顶元素，接下来枚举的数$x^\prime$小于$x$，栈顶元素产生的答案不可能更优。这样一直弹栈直到栈里没有和$x$互质的数。然后我们把$x$加到栈顶。接下来是如何求栈里和$x$互质的数的个数。

显然和$x$互质的数的个数是$\sum_{d \mid x} \mu(d) cnt_d$，其中$cnt_d$表示$d$的倍数的个数。那么只要在入栈和弹栈的时候维护$cnt_d$即可。