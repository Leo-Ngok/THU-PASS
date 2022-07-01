# PA11 报告
## A + B problem
### 1. 读题
就是高精度运算，这题是高精度乘法。
### 2. 解题思路
这题的数值范围是一个不大于 $10^{5000}$ 的非负整数，即便用 ``` long long ```  也远超数据的可行范围。

用一个数组保存输入数据，是一个很好的方法，接着就是处理进制的问题。选 ``` long long * ``` 类型的数组，可以最大化每个单元存的数值范围。

对于计算乘法的算法，主要有 “硬算” 法，与快速傅里叶变换相关的算法。

前者的复杂度是 $O(n^2)$，其中 $n$ 是两个输入的值的位数的较大者。

后者的复杂度约为 $O(n\cdot \log n)$ ， $n$ 的定义同上。

### 3. 解题思路的实现

先实现数据的读入与整理。为了防止暂存结果的数组，在运算过程中溢出，以下约定是 $10^8$ 进制，保存计算对象。
#### 3.1. 定义计算用的数组： 
从上到下分别是读取标准输入流的字符串、A 和 B 的在 $10^8$ 进制意义下的值，以及 $A\times B$ 的值。

```c++
#define ll      long long
#define MAXN    700
#define NS      100000000
#define ENS     8
char            dgt[MAXN * 8];
ll              x[MAXN];
ll              y[MAXN];
ll              res[2 * MAXN];
```
#### 3.2. 处理输入：
先把所有数组清零。
读到第 $8k$ 位的时候，把输入的下标往后挪一格，在原有的数值上，在最高位的前面加上数码。为了方便计算，引入 np 数组，如下：

``` c
const int    np[]     = {1, 10, 100, 1000, 10000, 100000, 1000000, 10000000};
```

由于在处理的时候，可以同时得知位数，因此输入除了是一个指向 A、B 数组的指针，也有一个 ```int ``` 的引用，表示那个数在 $10^8$ 意义下的位数。以下对零做了特判，防止溢出。

```c++
inline void read(ll* arr,int& digits)
{
    memset(arr, 0LL, sizeof(ll) * MAXN);
    memset(dgt, 0,   sizeof dgt);
    scanf("%s", dgt);
    size_t n = strlen(dgt);
    if(n == 1 && dgt[0] == '0') 
    {
        digits = -1;
        return;
    }
    for(int i = 0; i < n; i++)
    {
        arr[i / ENS] += (dgt[ n - i - 1 ] - '0') * np[i % ENS];
    }

    digits = n / ENS;
    if(( n % ENS)) digits++;
}
```

### 3.3. 乘法运算：

#### 3.3.1. “硬算”法：

假设 $A = \overline{a_n a_{n-1}a_{n-2}\cdots a_1 a_0}_{(10)} $,  $B =  \overline{b_m b_{m-1}b_{m-2}\cdots b_1 b_0}_{(10)}$ ，其中 $a_0,a_1,\cdots, a_n, b_0, b_1, \cdots,b_m \in \{0,1,2,\cdots,9\}$ 。

那么 $A \times B$ 就相当于 
$$
A \times B= \sum _{i = 0} ^ n 10 ^ i \cdot a_i \cdot B = \sum _{i = 0} ^ n 10 ^ i \cdot a_i \cdot (\sum _{j = 0} ^ m 10 ^ j \cdot b_j) = \sum _{i = 0} ^ n \sum _{j = 0} ^ m 10 ^ {i + j} \cdot a_i \cdot b_j   (*)
$$

进位的处理:

$(*)$ 中的 $a_i \cdot b_j $ 是很有可能超出允许范围的，这时就需要对数组做出调整。考虑到 $ 0 \leq a_i \cdot b_j < 10^2 = 100$, 于是就可以把十位部分加到后一位去，只保留个位部分。数组是连续访问的，因此可以在数码乘法后立即处理进位。

#### 3.3.2. DFT 相关算法

DFT 及其衍生算法，本质上是多项式乘法。

##### 3.3.2.1. 单位根

在开始前，先介绍单位根。所谓单位根，就是所有满足
$$
\omega ^n - 1 =0
$$
 的 $\omega$, 其中 $\omega \in\mathbb{C}$。

由代数基本定理，$\omega$ 的可能性共有 $n$ 个。

##### 3.3.2.2. 多项式

对于任意的 $n$ 次一元多项式，除了可以用 $n + 1$ 个形如  $p_{i}$ 的“系数”表示，也可以用  $ n + 1 $ 个 形如 $ (x_i, y_i) $ 的在那个多项式有序对表示。在 DFT 算法中，$x_i$ 是上述的单位根，而在 NTT 中，$x_i$ 是一个对于某个质数的本原根的某次冪，前者用于一般用途的乘法，后者用于对某数取模的乘法。

##### 3.3.2.3. 原理

离散傅立叶变换$\mathcal{F}$ 是一个在 $\mathbb{C}^n$ 的双射：
$$
\mathcal{F}:\mathbb{C}^N\to\mathbb{C}^N
$$
由于$\mathcal{F}$ 是线性的，其可以表示成
$$
\mathcal{F}_n=\frac{1}{\sqrt{n}}\left[\begin{array}{lllll}
1 &       1  & 1        & \cdots & 1 \\
1 & \omega   & \omega^2 & \cdots & \omega^{n-1} \\
1 & \omega^2 & \omega^4 & \cdots & \omega^{2(n-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
1 & \omega^{n-1} &\omega^{2(n-1)} &\cdots & \omega^{(n-1)^2}
\end{array}\right]
$$
同时又有
$$
\mathcal{F^{-1}}=\overline{\mathcal{F}}
$$
把对应在 $\mathcal{F}$ 的像域的值逐个相乘 ($O(n)$)，再逆变换回去 ($O(n\cdot \log{n})$)，答案就出来了。

同时 $\mathcal{F}$ 可以分解为 
$$
\mathcal{F}_n=\left[\begin{array}{ll}
I_{n/2}&D_{n/2}\\
I_{n/2}&-D_{n/2}
\end{array}\right]
\left[\begin{array}{ll}
F_{n/2}&\\
&F_{n/2}
\end{array}\right]
$$


其中 $D_n=\mathrm{Diag}(\omega^0,\omega^1,\cdots,\omega^{n-1})$, 而 $\omega = \cos{\frac{2\pi}{n} + i \cdot \sin{\frac{2\pi}{n}}}$ 。

把 $p(x)$ 写成 $p(x) = p_1(x^2)+x\cdot p_2(x^2)$ , 这时分别对 $p_1, p_2$  进行傅里叶变换即可。

由于 $n$ 是二次幂，所以这个算法的 $n$ 要求是一个最小的、比$A,B$ 位数要大的二次幂。如此一来，我在运行的时候由于数据规模不算很大，优化的时间很有限，于是最后用了"硬算"法。

### 3.4. 实现

```c++
inline void mul(int n, int m)
{
    memset(res, 0, sizeof res);
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            res[i + j]     += x[i] * y[j];
            res[i + j + 1] += res[i + j] / NS;
            res[i + j]     %= NS;
        }
    }
}
```

 

### 3.4. 输出结果
除了最高位，其他位都要在输出的时候，在前面补零。
```c++
inline void print(int n, int m)
{
    int t= n + m + 2;
    while (res[t] == 0)
        t--;
    printf("%lld", res[t]);
    while(t--)
    {
        printf("%08lld", res[t]);
    }
    puts("");
}
```

