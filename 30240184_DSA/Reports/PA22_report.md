# PA22 报告

## Polynomial

### 1. 读题

求多项式的字符串表达式的值。

### 2. 解题思路

先写一个多项式的类，重载加法、减法、乘法运算符，异或符重载为求幂运算符。

由于求值有先后，需要实现一个栈。

先逐个字符读入，判断类型，再判断是否能算。能算就交给重载了的运算符算。

### 3.代码实现

先写一个字符处理器(tokenizer)，再对于运算符token处理，能算就算。

#### 附上多项式类的声明：

```c++
template <typename T>
class Polynomial
{
    public:
    T coef[MAX_DEG];
    Polynomial();
    Polynomial(int c, int deg);

    Polynomial& operator+= (const Polynomial & P1);
    Polynomial& operator-= (const Polynomial & P1);
    Polynomial & operator *= (const Polynomial & P1);
    Polynomial & operator *= (const T & x);
    Polynomial & operator += (const T & x)
    {
        this->coef[0] += x;
        return *this;
    }
    Polynomial& operator^= (int pwr);
    Polynomial& operator= (const Polynomial & P1);
};
```

#### 手写栈的声明：

```c++
template <typename T>
class Stack
{
    T* data;
    size_t _capacity;
    size_t _size;
    public:
    Stack();
    ~Stack();
    bool empty();
    void pop();
    T& top();
    void push(const T& obj);
};
```

