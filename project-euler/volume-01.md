# Volume 01

## 1. Multiples of 3 and 5
容斥原理: $\frac{1000}{3}+\frac{1000}{5}-\frac{1000}{15}$.

## 2. Even Fibonacci numbers
直接暴力计算.

## 3. Largest prime factor
用`factor`暴力质因数分解.

## 4. Largest palindrome product
暴力枚举所有三位数..

## 5. Smallest multiple
求出$\mathrm{lcm}(1,2,...,20)$.

## 6. Sum square difference
暴力计算.

## 7. 10001st prime
筛法求解即可.

## 8. Largest product in a series
枚举每个可能, 取最大值.

## 9. Special Pythagorean triplet
暴力枚举出这个解.

## 10. Summation of primes
筛法的时候顺便求和即可.

## 11. Largest product in a grid
同#8, 暴力枚举所有可能.

## 12. Highly divisible triangular number
筛法求出前$10^5$的数的约数个数, 暴力找答案.

## 13. Large sum
用python算下答案即可.

## 14. Longest Collatz sequence
暴力计算加上记忆化.

## 15. Lattice paths
$f(i,j)=f(i-1,j)+f(i,j-1)$, 或者直接组合数.

## 16. Power digit sum
命令行下用`bc`算出结果, 然后求个和.

## 17. Number letter counts
暴力模拟.

## 18. Maximum path sum I
$f(i,j)=\max(f(i-1,j), f(i - 1, j - 1)) + a(i,j)$

## 19. Counting Sundays
用日期转化星期的公式计算.
``` cpp
int toWeekday(int y, int m, int d) {
  int tm = m >= 3 ? (m - 2) : (m + 10);
  int ty = m >= 3 ? y : y - 1;
  return (ty + ty / 4 - ty / 100 + ty / 400 + (int)(2.6 * tm - 0.2) + d) % 7;
}
```

## 20. Factorial digit sum
python大法好

## 21. Amicable numbers
先筛出每个约数, 然后暴力计算.

## 22. Names score
按照题目规则模拟.

## 23. Non-abundant sums
暴力枚举小于$28123$的数, 然后计算答案.

## 24. Lexicographic permutations
用`C++`的`next_permutation`计算.

## 25. $1000$-digit Fibonacci number
暴力计算出即可.

## 26. Reciprocal cycles
计算出每个分数的循环节, 取最大的.

## 27. Quadratic primes
枚举所有可能的$a$和$b$, 暴力计算能够生成的连续素数.

## 28. Number spiral diagonals
先构造出矩阵, 然后计算答案.

## 29. Distinct powers
首先计算出$[1,n]$内数的幂次表示, 然后暴力枚举$a$和$b$用`set`去重.

## 30. Digit fifth powers
枚举$[1,10^6]$内的数, 算下可行的数的和.

## 31. Coin sums
用背包计数.

## 32. Pandigital products
枚举$\{0,1,2,3,4,5,6,7,8,9\}$的全排列, 然后枚举所有划分计算合法等式.

## 33. Digit cancelling fractions
枚举所有可能, 找出这$4$个分数.

## 34. Digit factorials
解应该在$[1,10^6]$以内, 枚举一下即可.

## 35. Circular primes
线筛出所有素数, 然后暴力枚举.

## 36. Double-base palindromes
暴力枚举.

## 37. Truncatable primes
可以观察到, 满足条件的数每位一定由$\{1,3,5,7,9\}$组成, 爆搜即可.

## 38. Pandigital multiples
全排列枚举答案.

## 39. Integer right triangles
暴力枚举$a$和$b$, 计算出$c$, 判断是否合法.

## 40. Champernowne’s constant
$d_n$可以用$\log{n}$的时间计算出来.

## 41. Pandigital prime
全排列枚举答案.

## 42. Coded triangle numbers
暴力计算每个单词的和, 判断是否是三角形数.

## 43. Sub-string divisibility
枚举全排列.

## 44. Pentagon numbers
暴力枚举, 找到第一对就是答案.

## 45. Triangular, pentagonal, and hexagonal
暴力枚举, 判断是否合法.

## 46. Goldbach’s other conjecture
在$[1,10^6]$内枚举下答案.

## 47. Distinct primes factors
在$[1,10^6]$内枚举下答案.

## 48. Self powers
暴力快速幂计算下.

## 49. Prime permutations
暴力枚举每个四位数.

## 50. Consecutive prime sum
筛出所有素数, 暴力计算答案.
