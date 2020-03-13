# 2020 Humbleool Cup Prelims

+ [x] [ScoringJudges](https://community.topcoder.com/stat?c=problem_statement&pm=15980&rd=17851)
+ [x] [NonSimilarTriangles](https://community.topcoder.com/stat?c=problem_statement&pm=15947&rd=17851)
+ [x] [CardDrawPoints](https://community.topcoder.com/stat?c=problem_statement&pm=15978&rd=17851)

## ScoringJudges

题意：给出$n$个数$score_0,score_1,\dots,score_{n-1}$。求出前$\frac{1}{3}$大数的平均值+前$\frac{1}{3}$小数的平均值+剩下数的平均值。

$3 \le n \le 50, 0 \le score_i \le 100$

题解：略

## NonSimilarTriangles

题意：给出$n$个数$L_0,L_1,\dots,L_{n-1}$。求出能构成多少不相似的三角形。

$3 \le n \le 150, 1 \le L_i \le 10^6$

题解：略

## CardDrawPoints

题意：有$n$个数，$count_0,count_1,\dots,count_{n-1}$，其中$count_i$表示$i$出现了$count_i$次。你现在手上没有数，要么可以随机获得剩下的某个数，要么选择放弃。如果当前手上有两个数一样，那么得分是$0$；否则得分是所有数之和。求最优操作下的期望得分。

$1 \le n \le 16, 0 \le count_i \le 10$

题解：$dp(mask)$表示当前手上数的集合为$mask$的最优期望得分。那么下一次操作放弃的得分是这些数的和，不放弃的话也可以求出期望得分，两者取个最大值即可。