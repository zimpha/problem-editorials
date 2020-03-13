# Volume 10

## 451. Modular inverses
这题就是求$x^2 \equiv 1 \text{ mod } n$的最大$x$. 和#407一样, 一个方法就是枚举$x$, 然后枚举$(x-1)(x+1)$的约数$n > x+1$, 用$x$更新$I(n)$.

考虑$n=\prod p_i^{e_i}$, 那么有$x^2 \equiv 1 \text{ mod } p_i^{e_i}$. 对于某个$p^k$, $x^2 \equiv 1 \text{ mod } p^{k}$有两个解$1$和$p^k-1$. 于是枚举$n$, 将其质因数分解, 然后枚举每个质数取哪个解, 用中国剩余定理合并即可.

## 452. Long Products

## 453. Lattice Quadrilaterals

## 454. Diophantine reciprocals III

## 455. Powers With Trailing Digits

## 456. Triangles containing the origin II

## 457. A polynomial modulo the square of a prime

## 458. Permutations of Project
$dp(i,S)$表示前$i$个字符, 最后$6$个字符的状态是$S$的方案数, 这个状态可以用最小表示来搞, 总共只有$203$种状态. 于是找出转移矩阵, 用快速幂即可.

## 459. Flipping game

## 460. An ant on the move

## 461. Almost Pi
用折半搜索的方法, 先枚举$a,b$得出一些数, 然后枚举$c$和$d$, 在之前的数中二分即可.

## 462. Permutation of $3$-smooth numbers

## 463. A weird recurrence relation

## 464. Möbius function and intervals

## 465. Polar polygons

## 466. Distinct terms in a multiplication table

## 467. Superinteger

## 468. Smooth divisors of binomial coefficients

## 469. Empty chairs

## 470. Super Ramvok

## 471. Triangle inscribed in ellipse

## 472. Comfortable Distance II

## 473. varphigital number base

## 474. Last digits of divisors

## 475. Music festival

## 476. Circle Packing II

## 477. Number Sequence Game

## 478. Mixtures

## 479. Roots on the Rise
根据三次方程的韦达定理, 可以知道$(a_k+b_k)(b_k+c_k)(c_k+a_k)=1-k^2$, 然后等比数列直接算就好了.

## 480. The Last Question

## 481. Chef Showdown

## 482. The incenter of a triangle

## 483. Repeated permutation

## 484. Arithmetic Derivative

## 485. Maximum number of divisors
先线性筛求出所有$d(x)$, 然后用单调队列求一个窗口内的最值.

## 486. Palindrome-containing strings

## 487. Sums of power sums

## 488. Unbalanced Nim

## 489. Common factors between two sequences

## 490. Jumping frog

## 491. Double pandigital number divisible by $11$
$dp(i,j,S)$表示前$i$位, 对$11$取模结果是$j$, 当前使用的数字状态为$S$的方案数, 随便转移一下就好了.

## 492. Exploding sequence

## 493. Under The Rainbow
可以知道总的方案数是$161884603662657876$, 没有超过long long, 于是可以把分子直接计算出来. 计算就是一个很朴素的dp, 这里不表.

## 494. Collatz prefix families

## 495. Writing $n$ as the product of $k$ distinct positive integers

## 496. Incenter and circumcenter of triangle

## 497. Drunken Tower of Hanoi

## 498. Remainder of polynomial division

## 499. St. Petersburg Lottery

## 500. Problem $500!!!$
首先预处理出一些素数来. 显然, 每个素数的幂次都是$2$的幂次. 于是考虑用优先队列来扩展, 每次取出最小的$x$, 然后把$x^2$放回去. 前$500500$个$x$的乘积就是答案.
