# LAB3 报告

## BBST

针对AVL树和伸展树，分析两者的性能。

### 1. BBST 的实现：

工程架构：

1. ```BST.h```

   包含树结点和二叉查找树的定义于实现。

   **结点结构体：**

   ```c
   struct BinNode;
   using BinNodePosi = BinNode*; //节点位置
   struct BinNode { //二叉树节点模板类
       int data; //数值
       BinNodePosi parent, lc, rc; //父节点及左、右孩子
       int height; //高度（通用）
       // 构造函数
       BinNode() :
           parent ( nullptr ), lc ( nullptr ), rc ( nullptr ), height ( 0 ) { }
       BinNode ( int e, BinNodePosi p = nullptr, BinNodePosi lc = nullptr, BinNodePosi rc = nullptr,
                   int h = 0) :
           data ( e ), parent ( p ), lc ( lc ), rc ( rc ), height ( h ) { }
       // 操作接口
       BinNodePosi succ(); //取当前节点的直接后继
   };
   ```

   每个结点维护它的父节点和两个子结点的内存地址，并能找出那个结点在数据结构的直接后继。

   **直接后继的查找：**

   ```c++
   BinNodePosi BinNode::succ() { //定位节点v的直接后继
       BinNodePosi s = this; //记录后继的临时变量
       if ( rc ) { //若有右孩子，则直接后继必在右子树中，具体地就是
           s = rc; //右子树中
           while ( HasLChild ( *s ) ) s = s->lc; //最靠左（最小）的节点
       } else { //否则，直接后继应是“将当前节点包含于其左子树中的最低祖先”，具体地就是
           while ( IsRChild ( *s ) ) s = s->parent; //逆向地沿右向分支，不断朝左上方移动
           s = s->parent; //最后再朝右上方移动一步，即抵达直接后继（如果存在）
       }
       return s;
   }
   ```

   如果结点存在右方子节点，那就从那个右结点开始，一路往左，直到找到一片树叶，为该节点的后继。

   否则，就要判断该结点和父节点的父子关系，如果是右方子节点，就继续找它的祖先，直到出现一个结点，它是某个结点的左方子结点，那个结点的父节点是该点的直接后继。

   **二分查找树基类：**

   ```c++
   class BST  { 
   protected:
      int _size; BinNodePosi _root; //规模、根节点
      virtual int updateHeight ( BinNodePosi x ); //更新节点x的高度
      void updateHeightAbove ( BinNodePosi x ); //更新节点x及其祖先的高度
      BinNodePosi _hot; //“命中”节点的父亲
      BinNodePosi connect34 ( //按照“3 + 4”结构，联接3个节点及四棵子树
         BinNodePosi, BinNodePosi, BinNodePosi,
         BinNodePosi, BinNodePosi, BinNodePosi, BinNodePosi );
      BinNodePosi rotateAt ( BinNodePosi x ); //对x及其父亲、祖父做统一旋转调整
   public: //基本接口：以virtual修饰，强制要求所有派生类（BST变种）根据各自的规则对其重写
      virtual BinNodePosi & search ( const int& e ); //查找
      virtual BinNodePosi insert ( const int& e ); //插入
      virtual bool remove ( const int& e ); //删除
   };
   ```

   维护一个根节点的地址，以及树的规模，并且提供：

   - 子树旋转的方法，及其所用的  “3 + 4” 重构的方法
   - 更新树高的方法
   - 树结点插入、查找和删除的方法

   在具体的代码内容，虽然提供了插入和删除的实现，但这个是为了考虑代码的可扩展性，并不是重点，下面从略。

   另外，在基类提供旋转和重构函数，是为了方便实现其他树的数据结构，如红黑树，虽然最终没有实现，但如果有，将会降低工作量。

   **树高的更新：**

   从当前结点开始，更新自身和祖先的高度，直到根结点。

   ```c++
   int BST::updateHeight ( BinNodePosi x ) //更新节点x高度
   { return x->height = 1 + max ( stature ( x->lc ), stature ( x->rc ) ); } //具体规则，因树而异
   
   void BST::updateHeightAbove ( BinNodePosi x ) //更新高度
   { while ( x ) { updateHeight ( x ); x = x->parent; } } //从x出发，覆盖历代祖先。可优化
   ```

   **子树旋转**

   当树发生高度被判定为不平衡的时候，按照当前结点与其他结点的拓扑关系，调用重构函数实现旋转。

   “如果是右节点，就左旋转，反之亦然”。

   具体实现：

   ```c++
   BinNodePosi BST::rotateAt ( BinNodePosi v ) { //v为非空孙辈节点
      BinNodePosi p = v->parent; 
      BinNodePosi g = p->parent; //视v、p和g相对位置分四种情况
      if ( IsLChild ( *p ) ) /* zig */
         if ( IsLChild ( *v ) ) { /* zig-zig */
            p->parent = g->parent; //向上联接
            return connect34 ( v, p, g, v->lc, v->rc, p->rc, g->rc );
         } else { /* zig-zag */
            v->parent = g->parent; //向上联接
            return connect34 ( p, v, g, p->lc, v->lc, v->rc, g->rc );
         }
      else  /* zag */
         if ( IsRChild ( *v ) ) { /* zag-zag */
            p->parent = g->parent; //向上联接
            return connect34 ( g, p, v, g->lc, p->lc, v->lc, v->rc );
         } else { /* zag-zig */
            v->parent = g->parent; //向上联接
            return connect34 ( g, v, p, g->lc, v->lc, v->rc, p->rc );
         }
   }
   ```

   **"3+4" 重构：**

   每次旋转都涉及到两层，都与三个结点，四棵子树有关，因此都可以通过一条函数，重新排列结点的相对位置，更新它们间的拓扑关系。

   ```c++
   BinNodePosi BST::connect34 (
      BinNodePosi a, BinNodePosi b, BinNodePosi c,
      BinNodePosi T0, BinNodePosi T1, BinNodePosi T2, BinNodePosi T3
   ) {
       // left subtree, T0<-a->T1
      a->lc = T0; if ( T0 ) T0->parent = a;
      a->rc = T1; if ( T1 ) T1->parent = a; 
      updateHeight ( a );
       // right subtree, T2<-c->T3
      c->lc = T2; if ( T2 ) T2->parent = c;
      c->rc = T3; if ( T3 ) T3->parent = c; 
      updateHeight ( c );
       // connect as a<-b->c
      b->lc = a; a->parent = b;
      b->rc = c; c->parent = b; 
      updateHeight ( b );
      return b; //该子树新的根节点
   }
   ```

   上述两条函数都没有循环，为常数时间复杂度。

   **删除某个结点：**

   显然没有两个子树的时候，可以和子结点继承当前结点的位置，然后释放当前结点。，如果有，则要和直接后继交换，然后删除。

   ```c++
   static BinNodePosi removeAt ( BinNodePosi & x, BinNodePosi & hot ) {
      BinNodePosi w = x; //实际被摘除的节点，初值同x
      BinNodePosi succ = nullptr; //实际被删除节点的接替者
      if ( !HasLChild ( *x ) ) //若*x的左子树为空，则可
         succ = x = x->rc; //直接将*x替换为其右子树
      else if ( !HasRChild ( *x ) ) //若右子树为空，则可
         succ = x = x->lc; //对称地处理——注意：此时succ != nullptr
      else { //若左右子树均存在，则选择x的直接后继作为实际被摘除节点，为此需要
         w = w->succ(); //（在右子树中）找到*x的直接后继*w
         swap ( x->data, w->data ); //交换*x和*w的数据元素
         BinNodePosi u = w->parent;
         ( ( u == x ) ? u->rc : u->lc ) = succ = w->rc; //隔离节点*w
      }
      hot = w->parent; //记录实际被删除节点的父亲
      if ( succ ) succ->parent = hot; //并将被删除节点的接替者与hot相联
      return succ; //释放被摘除节点，返回接替者
   }
   ```

   

   **关键码查找**

   “比查找值大就往左，否则往右”。

   ```c++
   BinNodePosi & BST::search ( const int & e ) { //在BST中查找关键码e
      if ( !_root || e == _root->data ) { _hot = nullptr; return _root; } //空树，或恰在树根命中
      for ( _hot = _root; ; ) { //否则，自顶而下
         BinNodePosi & v = ( e < _hot->data ) ? _hot->lc : _hot->rc; //确定方向，深入一层
         if ( !v || e == v->data ) return v; _hot = v; //一旦命中或抵达叶子，随即返回
      } //返回目标节点位置的引用，以便后续插入、删除操作
   } //无论命中或失败，_hot均指向v之父亲（v是根时，hot为nullptr）
   ```

   上述两条函数的时间复杂度是树高，为 $O(\log n)$。

   2. ```AVL.h```

      顾名思义，提供AVL树的实现。

      定义为上述BST类的派生类。

   ```c++
   class AVL : public BST { //由BST派生AVL树模板类
   public:
      BinNodePosi insert ( const int& e ); //插入（重写）
      bool remove ( const int& e ); //删除（重写）
      int query(const int& e);
   };
   ```

   由于在插入和删除的时候都需要检查高度，因此需要重写。 

   query 函数，能给出题目要求的比查找值不大的数值。

   **插入：**

   照常进行，后面从其父结点开始，逐层检查高度，不平衡时旋转：

   ```c++
   BinNodePosi AVL::insert ( const int& e ) { //将关键码e插入AVL树中
      BinNodePosi & x = search ( e ); 
      if ( x ) return x; //确认目标节点不存在
      BinNodePosi xx = x = new BinNode ( e, _hot ); _size++; //创建新节点x
   // 此时，x的父亲_hot若增高，则其祖父有可能失衡
      for ( BinNodePosi g = _hot; g; g = g->parent ) //从x之父出发向上，逐层检查各代祖先g
         if ( !AvlBalanced ( *g ) ) { //一旦发现g失衡，则（采用“3 + 4”算法）使之复衡，并将子树
            BinNodePosi &t = FromParentTo ( *g );
            t = rotateAt ( tallerChild ( tallerChild ( g ) ) ); //重新接入原树
            break; //局部子树复衡后，高度必然复原；其祖先亦必如此，故调整结束
         } else //否则（g仍平衡）
            updateHeight ( g ); //只需更新其高度（注意：即便g未失衡，高度亦可能增加）
      return xx; //返回新节点位置
   } //无论e是否存在于原树中，总有AVL::insert(e)->data == e
   ```

   **删除：**

   原理同上。

   ```c++
   bool AVL::remove ( const int& e ) { //从AVL树中删除关键码e
      BinNodePosi & x = search ( e ); if ( !x ) return false; //确认目标存在（留意_hot的设置）
      removeAt ( x, _hot ); _size--; //先按BST规则删除之（此后，原节点之父_hot及其祖先均可能失衡）
      for ( BinNodePosi g = _hot; g; g = g->parent ) { //从_hot出发向上，逐层检查各代祖先g
         if ( !AvlBalanced ( *g ) ) {//一旦发现g失衡，则（采用“3 + 4”算法）使之复衡，并将该子树联至
            BinNodePosi &t = FromParentTo ( *g );
            g = t = rotateAt ( tallerChild ( tallerChild ( g ) ) ); //原父亲
         }
         updateHeight ( g ); //更新高度（注意：即便g未失衡或已恢复平衡，高度均可能降低）
      } //可能需做Omega(logn)次调整——无论是否做过调整，全树高度均可能降低
      return true; //删除成功
   }
   ```

   查找不大于查找值的最大值：

   往右拐时保存记录当前结点的值，每次更新必然更接近于所求值。

   ```c++
   int AVL::query(const int& e) {
      int res = -1;
      if(_root == nullptr) return res;
      if(e == _root->data) return e;
      BinNodePosi temp_node = _root;
      while (true) {
         if(e < temp_node->data) {
            temp_node = temp_node->lc;
         } else { // 当前结点值不比查找值大，是有可能的
            res = temp_node->data;
            temp_node = temp_node->rc;
         }
         if(!temp_node) { // 搜到底就不用再搜了
            return res; // 直接返回最后被记录的那个值
         }
         if(temp_node->data == e) return e; // 命中，结束
      }
   }
   ```

   上述时间复杂度是树高，为 $O(\log n)$。	

   3. ```Splay.h```

      总体思路：插入和删除都需要查找结点。在查找完之后，把该结点带到树根，对于频繁查找相同数据时时间占优。

      同样定义为BST的派生类。

      ```c++
      class Splay : public BST { //由BST派生的Splay树模板类
      protected:
         BinNodePosi splay ( BinNodePosi v ); //将节点v伸展至根
      public:
         BinNodePosi & search ( const int& e ); //查找（重写）
         BinNodePosi insert ( const int& e ); //插入（重写）
         bool remove ( const int& e ); //删除（重写）
         int query(const int& e);
      };
      ```

      对于伸展树，旋转操作是先动父节点，再动子结点，把整体高度降低，平均复杂度是对数时间，但如果退化为单链的时候则是线性，只要每次插入的值单调就能达到。

      结点的查找：

      类似于一般BST的查找，只是找到后当把结点带到根结点。

      ```c++
      BinNodePosi & Splay::search ( const int & e ) { //在伸展树中查找e
         BinNodePosi p = BST::search ( e );
         _root = splay ( p ? p : _hot ); //将最后一个被访问的节点伸展至根
         return _root;
      } //与其它BST不同，无论查找成功与否，_root都指向最后被访问的节点
      ```

      结点的插入和删除：

      类似于 AVL 的插入和删除，只是查找函数用重写的，供splay用的查找函数，之后不旋转子树调整高度，从略。

      因此，查找、插入和删除的平均复杂度为 $O(\log n)$。

      结合AVL 的query，和自身的查找，容易设计query 函数，实现如下。

      ```c++
      int Splay::query(const int& e) {
          int res = -1;
          if(_root == nullptr) return res;
          if(e == _root->data) return e;
          BinNodePosi temp_node = _root, pred = _root;
          while (true) {
              if(e < temp_node->data) {
                  temp_node = temp_node->lc;
              } else {
                  res = temp_node->data;
                  pred = temp_node;
                  temp_node = temp_node->rc;
              }
              if(!temp_node) { // 结点为空指针，查找完毕
                              // 当把上一个成功查找的结点，带到树根
                  _root = splay(pred);
                  return res;
              }
              if(temp_node->data == e) {
                  _root = splay(temp_node);
                  return e;
              }
          }
      }
      ```

      

### 2. 时间分析

生成两种情况的数据：一是完全随机，二是顺序的数据，三是插入随机的，查找为最近插入结点的数据，查找次数是200000，数据范围是2000000。

平均时间：

AVL: $380 \pm 52$ ms, Splay: $450 \pm 71$ ms, 

由此可见，avl 占优。