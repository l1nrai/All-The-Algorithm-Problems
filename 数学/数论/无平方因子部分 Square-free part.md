
## **Definition**

任意正整数 $x$ 都可以唯一分解为一个完全平方数和一个**无平方因子数**（Square-free integer）的乘积。

即 $x = a^2 \cdot k$，其中 $k$ 不包含任何大于 1 的完全平方数因子。我们定义这个 $k$ 为 $x$ 的核心部分 $core(x)$。

_注：这在数论上等价于要求莫比乌斯函数 $\mu(k) \neq 0$，即 $\mu^2(k) = 1$。_

## **Theorem

两个正整数 $i$ 和 $j$ 的乘积 $i \cdot j$ 是完全平方数，当且仅当它们具有相同的核心部分，即：

$$core(i) = core(j)$$

**Proof:**

设 $i = a^2 \cdot k_1$，$j = b^2 \cdot k_2$，其中 $k_1, k_2$ 均无平方因子。

二者的乘积为 $i \cdot j = (a \cdot b)^2 \cdot (k_1 \cdot k_2)$。

要使 $i \cdot j$ 为完全平方数，必须满足 $k_1 \cdot k_2$ 是完全平方数。既然 $k_1, k_2$ 都没有平方因子（即每个质因子的指数只能为 1），它们相乘能凑成平方数（质因子指数变为偶数）的唯一条件就是它们的质因子组成完全相同，因此必然有 $k_1 = k_2$。

## **Corollary**

基于上述定理，求 $\sum_{i=1}^n∑_{j=1}^m​∣f(ij)∣$，其中 $∣f(x)∣$ 当 $x$ 是完全平方数时为 $1$，否则为 $0$。可以转化为：枚举所有的核心部分 $k$，分别计算在区间 $[1, n]$ 和 $[1, m]$ 中有多少个数的 $core$ 为 $k$，然后将两边的数量相乘累加。

对于一个固定的无平方因子数 $k$，在 $1 \dots n$ 中满足 $core(i) = k$ 的 $i$ 的个数，等价于求满足 $a^2 \cdot k \le n$ 的正整数 $a$ 的个数。

通过移项，满足条件的最大正整数 $a$ 为：

$$a \le \sqrt{\frac{n}{k}} \implies \text{Count} = \lfloor \sqrt{\frac{n}{k}} \rfloor$$

因此，原本 $O(nm)$ 的双重求和，被降维成了一个上限为 $\min(n,m)$ 的单层求和：

$$\text{Ans} = \sum_{k=1}^{\min(n,m)} \mu^2(k) \lfloor \sqrt{\frac{n}{k}} \rfloor \lfloor \sqrt{\frac{m}{k}} \rfloor$$

## Templates

用类似埃氏筛法，预处理出无平方因子数：

```java
boolean[] haveNoSquare = new boolean[(int) limit + 1];  
Arrays.fill(haveNoSquare, true);  
haveNoSquare[0] = false;  
long mx = (long) Math.sqrt(limit);  
for (long i = 2; i <= mx; i++) {  
    long sq = i * i;  
    for (long j = sq; j <= limit; j += sq) {  
        haveNoSquare[(int) j] = false;  
    }  
}
```

## Problems

- [洛谷 P10584 [蓝桥杯 2024 国 A] 数学题](https://www.luogu.com.cn/problem/P10584) 