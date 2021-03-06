# PA36 报告

## Hacker

### 1. 读题

给定了盐，尝试对明文求逆。

密文是 $CRC32$ 值，粗略估计，范围是 ```unsigned int``` ，不可能开那么大的数组，存放明文；与此同时，用 ```vector<pair<unsgined int, char*> >```显然也不现实。

如果把密文这个 $CRC32$ 值，看作是散列表的 $key$, 那么字符串明文，就应该是 $value$ 。

因此，可以定义一个散列表：```HashTable<unsigned int, char*>``` ，去解决这道题。

### 2. 思路

处理散列冲突，是构造一个功能完备的散列表的一个很重要的组成部分。

常见的处理方式，有独立链条（separate chaining）法，以及开放地址（open addressing）法。

前者的实现方式，是把散列表每个位置，看作是一个链表的结点；后者则是预先开一个数组，出现散列冲突的时候，就利用试探法去找一个空位置。

虽然后者可以避免动态分配内存，节省时间，但我在最后是用了独立链条法。

### 3. 实现

在读取盐以后，就可以对长度为1到5的所有字符串求 $CRC32$ 值。

同时利用 $CRC32$ 是流式函数的特点，可以把前面字符串的初值，作为求盐的 $CRC32$ 值。

更进一步，利用递归的方式，逐位算出明文部分的 $CRC32$ 值，更大大简化了初始化的代码实现难度。

散列表存放的是链表指针，那个链表结点定义如下：

``` c++
struct node {
    ui key;
    char value[10];
    node* next;
};
```

实现散列函数、处理散列冲突。 先求出 $CRC32$ 值，并查找散列表指针，以及在该位置的链表的后继元素。无论是插入(insert)还是查询(query)，如果查找失败，自动返回空指针。

```c++
node* hash(ui key) {
    ui pos = key % N;
    node* elem = Data[pos];
    while(elem && elem->key != key) {
        elem = elem->next;
    }
    return elem;
}
```

对于插入操作，如果返回空指针，就对那笔资料分配内存，next 指向本来为开首的指针，并且把自己的地址，作为该链表的开首。

在查询的时候，如果查找失败，散列函数返回空指针，就可以直接输出 No。 

由于定义好了在插入的时候，如果存在一个 $CRC32$ 值与之相同的， 但存放的字符串不是准备插入的字符串，就可以把那一格的存放值归零。往后在搜的时候，如果发现重复了，那么 ```query``` 会搜到一个非空结点，但存放的字符串为空，就可以输出重复了。

否则，元素在散列表出现一次，查找成功。

先输出明文，然后取明文第一位，贴在一个存放先前8个记录的滚动数组，然后再对滚动数组长度为6，7，8 的明文，分别计算密文，存放再散列表内。而对于长度小于6 的明文，由于在初始化阶段就算完了，没有必要重算，对那三个串加盐，计算 $CRC32$ 值，存放在散列表内。

### 4. 时间、空间利用情况

生成初始明文的循环次数是固定的，不因输入规模而有改变，有着常数复杂度。

散列表的插入与查询，只要散列函数设计得当，一般对每次操作时间都是一样的，因此复杂度为 $O(n)$，即使考虑后面的更新操作，每次更新同样也是在基本固定的循环次数完成，所以运行的总的复杂度为 $O(n)$。

初始化的时候，产生了 
$$
\sum _{i = 1} ^ 5 18 ^ i = 2000718
$$
条密文-明文对。对于每一次查询，最多产生3条新的明文，且查询次数 $ \leq 10 ^ 6 $ ，因此累计摊分空间不大于 $5000718$ 个链表结点， 单论资料用了$(4 + 10 + 8) * 5 * 10 ^ 6 B\approx 105MB$ 空间，链表散列表本身（没有初始化的情况下）所有指针约占 $(3 * 10 ^ 6 * 8) B \approx 23MB$ ，累计使用 128MB。   







