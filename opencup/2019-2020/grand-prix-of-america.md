# XX Open Cup. Stage 13. Grand Prix of America / 2020 ICPC North America Champions

+ [ ] [A. Another Coin Weighing Puzzle](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/A/)
+ [ ] [B. Mini Battleship](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/B/)
+ [ ] [C. Bomas](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/C/)
+ [ ] [D. All Kill](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/D/)
+ [ ] [E. Grid Guardian](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/E/)
+ [ ] [F. Hopscotch](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/F/)
+ [ ] [G. ICPC Camp](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/G/)
+ [ ] [H. Letter Wheels](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/H/)
+ [ ] [I. Editing Explosion](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/I/)
+ [ ] [J. Lunchtime Name Recall](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/J/)
+ [ ] [K. Rooted Subtrees](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/K/)
+ [ ] [L. Tomb Raider](https://official.contest.yandex.ru/opencupXX/contest/17382/problems/L/)

## E. Grid Guardian

题意：

题解；显然，当$n$和$m$都是奇数的时候，答案是唯一的；当$n$是偶数，$m$是奇数的时候，答案是$(n/2+1)^{\lfloor \frac{m}{2} \rfloor}$；当$m$是偶数，$n$是奇数的时候也是类似。唯一比较困难的情况是$n$和$m$都是偶数，我们需要dp。