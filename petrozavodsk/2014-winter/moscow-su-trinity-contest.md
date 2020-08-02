# Petrozavodsk Winter 2014. Day 2. Moscow SU Trinity Contest

+ [x] [A. MEX-Query]
+ [x] [B. Beer Quadrilaterials]
+ [x] [C. Palindrome Extraction]
+ [x] [D. Short Enough Task]
+ [x] [E. Another Short Problem]
+ [x] [F. Just Another Sequence Problem]
+ [x] [G. Total LCS]
+ [ ] [H. Cyclic String]
+ [ ] [I. Circle Clique]
+ [ ] [J. Dividing Area]
+ [x] [K. Tree Problem]

## A. MEX-Query

题意：给出一个长度为$n$的数组$a_1,a_2,\dots,a_n$和$q$个询问。每次给出一个区间$[l_j,r_j]$，询问$\text{mex}(a_{l_j},a_{l_j+1},\dots,a_{r_j})$。

$1 \le n, q \le 10^6, 0 \le a_i \le 10^6, 1 \le l_i \le r_i \le n$

题解：把所有询问离线，考虑从左往右枚举每个数$a_i$，用一个线段树维护值为$a_i$最近出现的位置，以及值在$[l,r]$里的数出现位置的最小值。那么考虑所有$r_j=i$的询问，只需要在线段树上二分出一个最大的$x$，使得$[0,x]$里所有数的位置都大于等于$l_j$即可。

## B. Beer Quadrilaterials

题意：令$k=\frac{\pi}{2}$，求出有多少凸四边形$ABCD$满足：
+ $A$和$C$分别在$(-1,0)$和$(0,1)$
+ $B$在$AC$上方，$D$在$AC$下方
+ 所有边和对角线之间的夹角都是整数

题解：考虑$\triangle ABC$，令两个对角线的交点为$X$。那么根据角平分线定理有$\frac{AX}{XC}=\frac{AB \sin{\angle ABX}}{BC \sin{\angle CBX}}$。又根据$\frac{AX}{XC}=\frac{S_{\triangle AXB}}{S_{\triangle CXB}}=\frac{AX \cdot AB \cdot \sin{\angle XAB}}{XC \cdot BC \cdot \sin{\angle XCB}}$。如果我们令$\angle ABX=x,\angle CBX=y, \angle BAX=z$，那么有

$$
\frac{AX}{XC}=\frac{\sin x \cdot \sin {x+y+z}}{\sin y \cdot \sin z}
$$

把所有的$(180^\circ-x-z,\frac{\sin x \cdot \sin {x+y+z}}{\sin y \cdot \sin z})$存下来，我们就是要找多少二元组对$(a_1,b_1)$和$(a_2,b_2)$满足$a_1+b_1=180^\circ$并且$b_2=b_2$。

这个排个序直接双指针统计即可。

## C. Palindrome Extraction

题意：给出一个字符串$S$，你要找到一对字符串$B$和$D$，使得：

+ $S=A+B+C+D+E$，其中$A,B,C,D,E$都是非空字符串
+ $B+D$是回文串，并且$|B|+|D|$长度最长

$1 \le |S| \le 10^5$

题解：不妨枚举回文中心在$B$这里，那么$B=XY$，$D=X^R$，其中$Y$是回文串。可以发现$Y$肯定越长越好，因此可以枚举一个最长的$Y$。接下来就是需要求$(AX)^R$和$CDE$的所有后缀的LCP的最大值。

把$S$和$S^R$接在一起构建后缀数组，考虑$(AX)^R$在后缀数组中位置，往左和往右找到第一次出现在$CDE$里的后缀，那么LCP的最大值就是这段区间的height数组的RMQ。

如果回文中心在$D$这个的话，把串翻转一下在做一遍即可。

复杂度$O(|S| \log |S|)$。

## D. Short Enough Task

题意：给出$N$和$K$，求出长度为$N$，字符集为$K$的字符串中期望回文子串个数。

$1 \le N, K \le 10^9$

题解：显然答案是
$$
\sum_{i=1}^{N} K^{\lceil \frac{i}{2} \rceil -i} \cdot (N-i+1)
$$

当$K=1$的时候，答案为$\frac{N(N+1)}{2}$。其余情况，当$i$比较大的时候，$K^{\lceil \frac{i}{2} \rceil -i} \cdot (N-i+1)$就接近于$0$了，可以忽略不计。

## E. Another Short Problem

题意：给出$N$个三维空间上的点，第$i$个点坐标为$(x_i,y_i,z_i)$，存在概率为$p_i$。保证任意三点不共线，任意四点不共面。求出凸包上点个数的期望。

$1 \le N \le 50, 0 \le p_i \le 1, -1000 \le x_i, y_i, z_i \le 1000$

题解：当凸包上只有$1$个，$2$个，$3$个点的时候，概率很好计算。

当凸包上至少有$4$个点的时候，考虑欧拉定理$V+E-2=F$，有因为题目的限制可知$2E=3F$，于是可以得到$V=\frac{F}{2}+2$，因此我们只需要计算面的期望个数即可。

考虑枚举$i$和$j$和$k$这三个点作为凸包的一个面，假设左边点集合为$A$，右边点集合为$B$。那么概率为

$$
p_i \cdot p_j \cdot p_k \cdot ((1-p(A) \cdot p(B) + (1-p(B) \cdot p(A))))
$$

其中$p(A)=\prod_{x \in A} (1-p_x),p(B)=\prod_{x \in B}(1-p_x)$。

## F. Just Another Sequence Problem

题意：给出一个长度为$N$的数组$A_1,A_2,\dots,A_N$。你需要划分成若干部分，使得$S_1 \cdot S_2 + S_2 \cdot S_3 + \dots + S_{K-1} \cdot S_k$最大，其中$S_i$是第$i$部分的和。

$1 \le N \le 2000, -1000 \le A_i \le 1000$

题解：令$S_i=S_{i-1}+A_i$，$dp(i,j)$表示最后一部分是区间$(j,i]$的最优值，那么有如下的转移方程：

$$
\begin{aligned}
dp(i,j) &=& \max_{k < j}\{dp(j,k)+(S_i-S_j) \cdot (S_j-S_k)\} \\
&=& \max_{k < j}\{dp(j,k)+(S_j-S_i) \cdot S_k\} + (S_i-S_j) \cdot S_j
\end{aligned}
$$

$\max$里的可以看成是一些$y=mx+b$形式的直线，然后求$x=S_j-S_i$时候的最大值。

那么对于每个$dp(i,\cdot)$，就可以用这些直线构建一个凸壳，询问可以$O(\log n)$做到。

## G. Total LCS

题意：给出两个字符串$S$和$T$，对于每对$(i,j)$ ($1 \le i \le j \le |T|$)，求出$LCS(S, T[i..j])$。其中$LCS(s,t)$表示$s$和$t$的最长公共子序列的长度。

$1 \le |S|, |T| \le 2000$

题解：类似这个论文[Solving Cyclic Longest Common Subsequence in Quadratic Time](https://arxiv.org/pdf/1208.0396v3.pdf)的方法即可。

## H. Cyclic String

题意：给出一个长度为$N$的环形字符串，你需要把它切成$K$份$S_1,S_2,\dots,S_K$，使得$\max\{S_1,S_2,\dots,S_K\}$最小。

$1 \le N \le 2000, 1 \le K \le N$

题解：建立后缀数组，然后二分字典序第$x$大的字符串，那么对于每个位置$i$，我们能够知道它最长能够往后切多长，记为$L_i$。

如果每个$L_i$都非零，那么我们只需要求出最少需要几个这样的$i$就能覆盖所有字符串。

显然有些$L_i$为零，那么我们需要把这些点都删掉，同时减少相应的覆盖了$i$的那些$L_{j}$。这样最多迭代$O(N^2)$次，就能把所有没有贡献的点都删掉。这个时候如果剩下来不足$K$个点，那么这个解不合法。

那么就可以通过刚才的贪心，枚举每个起点求出最少的个数。由于需要输出方案，我们可以考虑随机$O(\frac{N}{K})$个起点，然后用$O(NK)$的dp记录方案，也可以通过这个dp判定解是否合法。

事实上可以做到$O(N \log N)$，使劲优化上述算法即可。

## I. Circle Clique

题意：有一个圆心在$(0,0)$，半径为$R$的圆。还有$N$个点，第$i$个点坐标为$(x_i,y_i)$。对于两个点$i$和$j$，如果他们和圆没有交点，那么连一条边。求这个图的最大团，并输出方案。

保证所有点互不相同，每个点都在圆外，没有两个点位于同一条切线上。

$1 \le N \le 2000, 1 \le R \le 2000, -5000 \le x_i, y_i \le 5000$

题解：可以将一个点对应到圆周上一个区间（考虑相切位置即可），那么可以发现两个点之间有边当且仅当他们的区间有交。那么问题转化成求出一个最大的区间集合，使得任意两个区间都有交。

基本就是[Petrozavodsk Winter 2020. Day 5. Jagiellonian U Contest. D. Clique](/petrozavodsk/2020-winter/jagiellonian-u-contest#d.-clique)这个题。枚举长度最小的区间，然后转化成二维平面上的点，然后用线段树优化dp即可。

最后输出方案可以找到最小区间，然后跑一个$O(N^2)$的dp记录方案。

## J. Dividing Area

题意：有$N$个点，第$i$个点坐标为$(x_i,y_i)$，保证每个点坐标不同。给出$Q$个操作
+ Type 1：连接两个点$a$和$b$，保证这条线段不和之前的线段在内部相交，线段内也没有其他点。
+ Type 0：给出边$ab$，询问$ab$左侧的闭合曲线的面积。

保证会一直加Type 1的边直到不能再加为止。

$1 \le N \le 200000, 1 \le Q \le 10^6, -2 \cdot 10^8 \le x_i, y_i \le 2 \cdot 10^8$

题解：根据题目的保证，到最后每个闭合区域一定是三角形。于是可以先$O(N \sqrt N)$找出所有的三角形。

倒着模拟所有询问，用并查集维护三角形的连通性和当前的面积即可。

## K. Tree Problem

题意：给出$N$个点的一棵树，一开始每条边都是黑色的。给出$Q$个操作：

+ 求出$a$到$b$的路径中有多少条黑边
+ 把$a$到$b$的路径上的边都搞成白色，把和$a$到$b$路径相邻的边搞成黑色

$1 \le N \le 200000, 1 \le Q \le 300000$

题解：考虑对这棵树做树链剖分，那么$a$到$b$的路径中最多会经过$O(\log N)$条轻边。

我们在重链上的每个点上维护一个标记，表示要不要把相邻的轻边都搞成黑色，同时用一个数据结构$D$维护重链上黑边的数目。

那么对于修改操作，用数据结构$D$把重链上的边都改成白色，轻边的话手动修改成白色。重链上的点也都打上标记，然后可能会让某些白色的重边变回黑色，这个手动修改一下。

对于询问操作，用数据结构$D$查询重链上的结果。对于轻边，去对应的重链上查看标记即可。