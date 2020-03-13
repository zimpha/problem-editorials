# Volume 02

## 51. Prime digit replacements
枚举所有可能的情况, 找出那个解.

## 52. Permuted multiples
从小到大依次枚举可能的数.

## 53. Combinatoric selections
利用组合数递推式计算, 超过部分直接设为一个较大值.

## 54. Poker hands
按照规则模拟, 算出每一手的分数.

## 55. Lychrel numbers
暴力枚举, 然后迭代最多$50$次.

## 56. Powerful digit sum
用`python`算下就好了.

## 57. Square root convergents
很容易找到分子分母的递推式:
$$\begin{aligned}
a_{i+1} &=  a_{i}+2b_{i}, \\ b_{i+1} & = a_i+b_i.
\end{aligned}$$
## 58. Spiral primes
不断增加边界模拟即可.

## 59. XOR decryption
对给出来的文本做频率分析, 然后可以猜测一些对应的字母.

## 60. Prime pair sets
找出$10000$以内的素数, 然后爆搜.

## 61. Cyclical figurate numbers
枚举$6$种多边形数在答案集合的排列, 然后枚举第一个数.

## 62. Cubic permutations
算出底数在$10^5$以内的立方数, 然后找到三个即可.

## 63. Powerful digit counts
考虑$a^n$的十进制位数为$\lfloor n\log_{10}{a} \rfloor+1$, 也就是说$n - 1 \le n \log_{10}{a} < n$, 可以得到$10^{\frac{n-1}{n}} \le a < 10$.枚举$n$, 算下可行的$a$即可.

## 64. Odd period square roots
打下表可以在[oeis](http://oeis.org/A013943)上找到这个数列.

## 65. Convergents of e
可以根据题目给出来的公式直接递推.

## 66. Diophantine equation
解佩尔方程, 如果$D$是完全平方数则无解, 否则解可以表示为
$$
\begin{aligned}
x_{k+1} &= x_1 x_k + n y_1 y_k, \\ y_{k+1} &= x_1 y_k + y_1 x_k.
\end{aligned}
$$
初始解可以用下面程序解出:
``` python
def pell(D):
  sqrtD = int(sqrt(D))
  if sqrtD * sqrtD == D:
    return -1
  c = sqrtD
  q = D - c * c
  a = (c + sqrtD) / q
  step = 0
  X = {}
  Y = {}
  X[0], X[1] = 1, sqrtD
  Y[0], Y[1] = 0, 1
  while True:
    X[step] = a * X[step ^ 1] + X[step]
    Y[step] = a * Y[step ^ 1] + Y[step]
    c = a * q - c
    q = (D - c * c) / q
    a = (c + sqrtD) / q
    step ^= 1
    if c == sqrtD and q == 1 and step == 1:
      return X[0], Y[0]
```

## 67. Maximum path sum II
参考#18的做法.

## 68. Magic 5-gon ring
写个全排列爆搜.

## 69. Totient maximum
筛法算出$[1,10^6]$内的$\varphi(n)$, 然后枚举即可.

## 70. Totient permutation
线性筛法算出$[1,10^7]$内的$\varphi(n)$, 然后枚举即可.

## 71. Ordered fractions
枚举分母, 然后二分出最接近$\frac{3}{7}$的分数即可.

## 72. Counting fractions
答案就是$\sum\limits_{i=1}^{n}\varphi(i)$.

## 73. Counting fractions in a range
$O(d^2)$暴力枚举即可.

## 74. Digit factorial chains
枚举每个数, 计算出链的长度.

## 75. Singular integer right triangles
枚举所有的互素勾股数对即可.可以用[Tree of primitive Pythagorean triples](https://en.wikipedia.org/wiki/Tree_of_primitive_Pythagorean_triples)枚举.

## 76. Counting summations
背包计数即可.

## 77. Prime summations
用背包算出$1000$以内数的答案.

## 78. Coin partitions
利用五边形数定理可以在$O(n\sqrt{n})$时间算出$n$以内的答案.令$p(n)$表示$n$的划分数, 那么$p(n)=\sum (-1)^{k-1}p(n - \frac{k(3k-1)}{2})$.

## 79. Passcode derivation
先去重, 然后可以发现最多只有$33$个, 然后全排列枚举出现的可能.

## 80. Square root digital expansion
用`python`的`Decimal`计算.

## 81. Path sum: two ways
$f(i,j)=\max\{f(i-1,j),f(i,j-1)+a(i,j)\}$

## 82. Path sum: three ways
直接跑最短路.

## 83. Path sum: four ways
同#82, 直接跑最短路.

## 84. Monopoly odds
用`Monte Carlo method` 随机游走$10^6$次, 看下答案即可.

## 85. Counting rectangles
可以注意到矩形的长不会超过$2000000$, 于是枚举矩形的长和高暴力计算即可.

## 86. Cuboid route
暴力枚举$m$即可.

## 87. Prime power triples
筛出$[1,\sqrt{n}]$以内的素数, 然后暴力枚举所有组合.

## 88. Product-sum numbers
枚举$1$使用的个数, 然后爆搜答案.

## 89. Roman numerals
观察到只需要把"VIIII", "IIII", "LXXXX", "XXXX", "DCCCC", "CCCC"依次替换为"IX", "IV", "XC", "XL", "CM", "CD"即可.也可以先转成十进制, 然后再用规则转成罗马数字.

## 90. Cube digit pairs
枚举所有的组合即可.

## 91. Right triangles with integer coordinates
暴力枚举两个端点坐标.

## 92. Square digit chains
暴力枚举加上记忆化即可.

## 93. Arithmetic expressions
枚举$a,b,c,d$, 计算的时候可以枚举$a,b,c,d$的排列, 然后每种每种排列有$5$种加括号的方式, 以及有$4^3$种插符号的方式.

## 94. Almost equilateral triangles
令$a,b$分别为腰长和底边长, 可以分为两种情况.

1. $b=a+1$, 可以得到$(\frac{3a-1}{2})^2-2y^2=1$
2. $b=a-1$, 可以得到$(\frac{3a+1}{2})^2-2y^2=1$

都是解个佩尔方程就好了.

## 95. Amicable chains
暴力筛法, 暴力枚举.

## 96. Su Doku
用`python`的`dlxsudoku`库求解.

## 97. Large non-Mersenne prime
`print (28433 * pow(2, 7830457, m) + 1) % m`

## 98. Anagramic squares
先暴力枚举所有的`anagrams words`, 然后枚举平方数, 判断第二个是否可以是平方数.

## 99. Largest exponential
取对数比大小验证即可.

## 100. Arranged probability
令$B,T$分别表示蓝色的和总数, 那么可以得到$2(2B-1)^2-(2T-1)^2=1$. 利用佩尔方程求解即可. 或者可以使用网上的求解器[Dario Alpern's Generic Two integer variable equation solver](https://www.alpertron.com.ar/QUAD.HTM).

令$x=2B-1, y=2T-1$, 可以得到递推式
$$
\begin{aligned}
x_i &= 3x_{i-1}+2y_{i-1}, \\ y_i &= 4x_{i-1}+3y_{i-1}.
\end{aligned}$$
初始值为$x_0=y_0=1$.
