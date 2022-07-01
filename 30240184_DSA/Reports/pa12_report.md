# PA12 报告
## Graphics
### 1. 读题

题目给出 $2n$ 个点，分别在正 $x,y$ 轴上。由于把那些点连上后那些线段不相交，而且连接方法唯一，因此可以先把 $x,y$ 轴上的点排序。排序后，再判断查询的点是否在某一条线段的左下侧即可。

### 2. 解题思路

先把 x,y 分别排序，然后由于那些线段有某种意义上的全序关系，可以用二分法找到最靠右上方的边，使得那条边与查询点最近的点（投影），在查询点的左下方，最后输出该点的编号。二分的判断规则，是查询点与线段的两个端点围成的有向面积的符号。由于在程序里面，编号下标是以零开始，在输出的时候要变回从一开始，就把输出加上一。

### 3. 实现

对输入而言，先按字符读入，减少读入时间：

```c++
#define ll      long long
inline ll read()
{
    ll  res = 0;
    int w;
    do
    {
        w = getchar();
    }
    while(w <  '0' || w >  '9');
    while(w >= '0' && w <= '9')
    {
        res = res * 10 + (w - '0');
        w   = getchar();
    }
    return res;
}
```

在输入后就对点分别排序。

```c
ll n = read();
for(int i = 0; i < n; i++)
{
    x_pos[i] = read();
}
qsort(x_pos, n, sizeof(ll), cmp);
for(int i = 0; i < n; i++)
{
    y_pos[i] = read();
}
qsort(y_pos, n, sizeof(ll), cmp);
```

对于每个查询，都执行一次二分搜索：

```c++
while(m--)
{
    ll  x   = read();
    ll  y   = read();
    int l   = 0;
    int r   = n;
    int mid;
    if(!judge(x, y, 0))
    {
        puts("0");
        continue;
    }
    while(1 < r - l)
    {
        mid = l + (r - l) / 2;
        if(judge(x, y, mid))
             l = mid;
        else r = mid;
    }
    printf("%d\n", l + 1);
}
```

**由于二分算法无法判断零的情况，需要在执行折半搜索前判零。**

判断函数：

```c
inline bool judge(long long, long long, int);
```

第一、二个输入是查询点，第三个输入是线段对应的下标。

判断函数的实现：

设查询点为 $P(x,y)$， 被判线段的两端分别为 $ A(0, y_i) $ 和 $ B(x_i,0)$ 。

那条边与查询点最近的点（投影），在查询点的左下方，当且仅当那三点的逆时针有向面积为正。由于在线上的情况同样看作有效，于是就变为判断面积是否非负：
$$
S_{\Delta PAB} = \frac{1}{2} \left\vert
\begin{array}{ccc}
x   & y   & 1 \\
0   & y_i & 1 \\
x_i & 0   & 1
\end{array}
\right\vert \geq 0
\newline
\Leftrightarrow x_i \cdot y + x \cdot y_i - x_i \cdot y_i \geq 0
\newline
\Leftrightarrow x \cdot y_i + x_i \cdot y \geq x_i \cdot y_i
$$
因此，真正的判断，就只有一句：

```c++
return ! (x * y_pos[i] + x_pos[i] * y < x_pos[i] * y_pos[i]);
```



 