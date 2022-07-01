# PA31 报告

## Build

### 1. 读题

多叉树的模拟，照样做就完事了。

### 2. 解题思路

#### 2.1 树的表示

把那棵多叉树以一棵二叉树表示。在二叉树上，多叉树上某个结点的嫡子，是那个在二叉树上对应结点的左儿子；而它的右儿子，是多叉树上该点的“弟弟”。以下面这种方式存储结点：

```c++
struct node {
    int pred;
    int size;
    int height = -1;
    int child_pos;
    int bro_pos;
    int bro_size;
    int bro_height = -1;
}Nodes[N];
```

如果那个结点是嫡子， `pred` 是其父结点，否则就是他的“兄长”。

`bro_size` 存的，是他所有“弟弟”的规模总和，`bro_height` 是他的最高的弟弟的高度，以这种方式保存高度、规模信息，方便在移动子树的时候，更新他的所有前驱的高度与规模。

#### 2.2 树的构造

首先通过邻接表，确立结点之间的从属关系，接着从“树叶” （出度为零的结点）开始更新规模与高度信息，对于某个结点，先处理它的弟弟，然后处理他的嫡子。此处借用了课上二叉树后序遍历的实现思路，遍历树上所有结点。

```c++
void build() {
    //Construct the framework
    for(int ii = 1; ii <= n; ii++) {
    	//   ......
        // Connect all the nodes here, using
        // data given by the adjacency list.
    }
    // Update the height and size of the nodes
    // ...
    // Use post-order DFS to initialize the sizes and
    // heights of the nodes. All nodes are only visited
    // once, so its complexity is O(n).
    while(!BNodes.empty()) {
        // ... post order transversal here ...
        pos = BNodes.top();
        BNodes.pop();
        // Update the heights and sizes of the current node
        update(pos);
    }
}
```

每一棵树都有 $n-1$ 条边，确立从属关系用时 $O(n)$。

更新某个结点时间为 $O(1)$，更新所有结点用时 $O(n)$ ，总耗时 $O(n)$。

#### 2.3 子树的定位

这部分是后面所有操作的基础，因为无论是移动子树，还是查找子树的信息，都要先把子树定位。

定位的方法是，从根节点开始，按照 $rank$ 去转移到树上的某个结点，期间，需要把经过的结点顺序记录。

在每一次通过 $rank$ 找到那个儿子之后，当记录当前的数组的大小，因为以后如果遇到无效结点，就要把数组还原。而还原的方法，就是把那个数组大小的值，修改为上一次成功的大小，耗时 $O(cost)$。

利用 `int get_pos(Stack* path); `实现。

#### 2.4 结点的查询

利用 2.3 定位结点，并直接输出那个点的 `size` 或 `height` 成员值，耗时 $O(cost)$。

#### 2.5 子树的移动

同样利用 2.3，分别定位源树、目标结点。

分为四部分：

1) 把子树从树上拔除 
2) 更新源子树的所有前驱的高度、规模信息。
3) 把子树连接到新的位置上
4) 更新现阶段那棵子树根节点，以及它的所有前驱的高度、规模信息。

##### 2.5.1 子树的删除

先把子树根节点前驱的后继（若是嫡子则让弟弟继承前驱的**嫡子**位置，否则继承**弟弟**位置）， 设为子树根节点的第一个弟弟，接着如果子树根节点的弟弟存在，就把子树根节点弟弟的前驱，设为子树根结点的前驱。

接着把那棵子树的所有关于弟弟的信息清零。

##### 2.5.2 更新源树前驱的信息

在定位源树的时候，2.3 生成的数组记录了源树的所有前驱，于是只要倒着把数组上的每一个结点的高度、规模信息更新，就能把整棵树的高度、规模信息更新，耗时$O(cost)$。

##### 2.5.3 连接子树

先用2.3 求目的结点位置，接着按照 $rank$ 查找源子树在新的位置的前驱，实现方法类似 `get_pos` （同样需要记录这个过程经过的结点）。定位后，利用类似链表插入的方法插入子树即可。查找位置耗时 $O(rank + cost)$，连接用时 $O(1)$ ，共用时 $O(rank + cost)$。

##### 2.5.4 更新新的树的高度、前驱信息

与 2.5.2 完全一致，略。

小结：移动子树，用时 $O(rank + cost)$。