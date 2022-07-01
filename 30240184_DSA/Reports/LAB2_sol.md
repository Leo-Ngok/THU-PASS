# LAB2 报告

## HashFun

### 1 散列函数与冲突处理

#### 1.1 散列函数

记 $s_i$为字符串的任何一位。

对 ASCII 串，利用滚动方式存储散列值：
$$
\mathrm{hash}(0) = 0 \\
\mathrm{hash}(s_{i +1}) = ((\mathrm{hash}(s_i) << 5) | (\mathrm{hash}(s_i) >> 27)) + \mathrm{ASCII}(s_{i+1})
$$
对于 UTF-8 串， 利用  MAD 法：
$$
\mathrm{hash}(0) = 5381 \\
\mathrm{hash}(s_{i +1}) = (\mathrm{hash}(s_i) << 5) +\mathrm{hash}(s_i) + \mathrm{UTF_8}(s_{i+1})
$$
其中 UTF-8 函数是取那个字符对应的二进制表示，所对应的值。

在最后输出的时候对散列表大小取模。

#### 1.2 冲突处理

##### 1.2.1 双向平方试探策略：

```c++
void quad_probe::init() {sign = -1;}// alternating between iterations

int quad_probe::operator() (hash_entry* entry, int sz, int key) {
    if(!initial_assigned) { // invoke when first triggered
        initial_value = key;
        initial_assigned = true;
    }    
    static unsigned int query_freq = 1; // freq. for probing invoked
    query_freq++;
    sign *= -1;
    unsigned int ii = query_freq >> 1;
    return (initial_value + sign * ii * ii + sz) % sz;
}
```

##### 1.2.2 公共溢出区策略：

先对散列表的构造函数，插入以下代码片段：

```c++
if(typeid(*my_collision) == typeid(overflow_probe)) {
    table_size = ((table_size >> 1) & ~3) + 3;
} // reduce the available size approx. to its half, while keeping the 4n + 3 property
```

然后定义初始化，调用重载函数：

```c++
void overflow_probe::init() {pos = -1;} // -1 means it is empty

int overflow_probe::operator()(hash_entry* entry, int sz, int key) {
    if(!initial_assigned) { // invoke when first triggered
        initial_value = sz;
        initial_assigned = true;
    } 
    pos++;
    return initial_value + pos; // probe the next empty position
}
```

### 2 测试

```generator.cpp``` 为数据生成器，第13到17行给出了命令行参数的输入方式。

在查询与插入次数都没用完的时候，随机进入这两条函数之一。

对于**插入**操作，随机在数据集找一个人名，并随机生成匹配值，同时保存那个人名的id。

对于**查找**操作，分为三个部分，每次操作随机进入其中一个：

1. 随机生成用户名字符串。
2. 在保存曾插入id的数组，随机挑一个，并输出该用户名。
3. 在数据集里随机挑选一个字符串。

以 ```srand(time(0))``` 作为生成器的种子，确保每次生成不同数据。

| 名称(set i.txt) | 出处 | 插入次数 | 查找次数 |
| --------------- | ---- | -------- | -------- |
| 1               | poj | 25000 | 25000 |
| 2|poj|400000|300000|
|3|poj|200000|500000|
|4|hdu|75000|60000|
|5|hdu|280000|350000|
|6|hdu|500000|400000|

### 3 分析

1. 两者性能并没有很大差异，两者的运行时间相若。使用UTF8-HASH 在线性试探的情况反而导致 set5.txt, set6.txt 超时，而ASCII 没有。但总体而言，区别不大。

2. 总体而言，双向平方试探占优。但对于使用 ASCII hash 的样例，其实两者区别并不是很大。较明显的是 naive , 平方法明显比起线性法为优。其中的原因，是平方法每一次迭代，都’绕‘的比较远。

3.  封闭散列效率较高。数据完全随机生成，数据量小可以认为冲突比率降低，因此开放散列适合在冲突几率低的时候使用。
4.  数据的不均匀，对导致散列值分布不均匀，结果是散列冲突的概率，相比均匀的时候增大，运行效率降低。
5. 给定一个有限大小的字母表，以字母表生成的字符串查询数字的时候，利用 Trie, 则插入、查询操作时间复杂度都与字符串长度线性相关，为 $O(|S|)$ 。

