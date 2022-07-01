# PA21 报告
## Risk
### 1. 读题

求指定天数前确诊数的最大值，然后给定确诊数阈值，判断中、低风险日数，实际上就是求区间最大值，然后排序，在有序数组找比阈值小的最大值的位置。

### 2. 解题思路

先解决区间最大值的问题。
在线算法：
可以利用RMQ 滑动窗口方法，也可以用Queap.
离线算法：
稀疏表。

碍于本人在完成作业期间学业负担比较重，综合考虑选用离线的稀疏表算法。

对于查找区间内比阈值小的元素个数，并不见得需要用到线性查找。可以先排序再二分查找。

稀疏表建表需要 $$O(n\cdot\log(n))$$ 的时间，其中 $$\log(n)$$ 是稀疏表高，$$n$$ 是天数。每次对稀疏表查询都是常数时间，于是查找确诊最大值的天数，需要 $$O(n\log(n))$$ 时间 。



在处理给定阈值的查询前，先对对应的确诊数的最大值排序。处理方法是利用内建的快排，复杂度 $$O(n \log(n))$$。



对每一次查询，在数组用二分法找比阈值小的最大元素，每次查询 $$O(log(n))$$。

因此整体的复杂度是$$O((m+n)\log(n))$$ , 其中 $$m$$ 是查询次数。

### 3. 实现

先构造稀疏表。
```c
void build(int n)
{
    int h = log2(n);
    int t = 1;
    int u = n;
    for(int i = 1; i <= h; i++)
    {
        for(int j = 0; j + t < u; j++)
        {
            ST[i][j] = _max(ST[i - 1][j], ST[i - 1][j + t]);
        }
        u -= t;
        t <<= 1;
    }
}
```

稀疏表的每一层的长度，都比上一层少 2^(层数-1)，因为在第 $$i$$ 层，每个位置的值，是第零层（原有数据）从那个项开始算起 的 $$2^i$$ 个项的最大值。

在输入回溯天数的时候，可以同时查询稀疏表找区间最大值。

```c
ll query(ll l, ll u)
{
    if(l < 0) l = 0;
    if(n < u) u = n;
    ll w = u - l;
    if(w < 1) return 0;
    int log_width = log2(w);
    return _max(ST[log_width][l], ST[log_width][u - (1 << log_width)]);
}
```

具体查找的方法，就是先求区间长度，找出相应的层，然后再比较能恰好覆盖整个区间的两个位置的数的最大值。

接着就用二分找天数：

```c
ll p = read();
ll q = read();
ll l = 0;
ll r = n;
if(peak[0] >= p)
{
    printf("0 ");
    p = 0;
    goto findmid;
}
while(1 < r - l)
{
    ll mid = (r + l) >> 1;
    if( peak[mid] < p) l = mid;
    else r = mid;
}
p = l + 1;
printf("%lld ", p);
findmid:
if(peak[0] >= q)
{
    puts("0");
    continue;
}
ll pl = l;
r = n;
while(1 < r - l)
{
    ll mid = (r + l) >> 1;
    if( peak[mid] < q) l = mid;
    else r = mid;
}
printf("%lld\n", l + 1 - p);
```

