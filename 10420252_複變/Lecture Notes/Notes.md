# 复变函数引论学习资料

[TOC]



## 0. 基本概念

### 0.1. 格林公式

$\partial D$ 为一分段简单光滑闭合曲线，$D$ 是 $\partial D$ 围成的一个区域，且$P(x,y), Q(x,y)$ 在 $D$ 内连续可导，则
$$
\oint_{\partial D} Pdx + Qdy = \iint_D (Q_x-P_y)dxdy 
$$

### 0.2. 换元公式

设 $\mathbf{r} =\gamma(t) = x(t) \hat{i} + y(t) \hat{j}$ ，$t\in[0,1]$ 为一分段光滑曲线，则
$$
\int_{\gamma} \mathbf{F(r)} d\mathbf{r} = \int_0^1 \mathbf{F}(\gamma(t))\cdot \gamma'(t) \cdot dt
$$

### 0.3. 复数的定义

复数域：
$$
\mathbb{C} = \{(x + iy):x,y\in\mathbb{R}, i = \sqrt{-1}\}
$$
复数运算：
$$
z := x + iy \\
\Re(z):=x, \Im(z):=y,\\
z_1 \pm z_2 := (x_1 \pm x_2) + i(y_1 \pm y_2) \\
\bar{z} := x - iy, |z| := \sqrt{x^2 +y^2} \\
z_1z_2 := (x_1x_2 - y_1y_2) + i(x_1y_2 + x_2 y_1) \\
\Rightarrow |z|^2 = z\bar{z}\\
\frac{z_1}{z_2} := \frac{z_1\bar{z_2}}{|z_2|^2} \\
$$
复平面：

Argrand diagram $\leftrightarrow$ Cartesian Coordinates.

$x$ 轴 $\leftrightarrow $ 实轴 ， $y$ 轴  $\leftrightarrow$ 虚轴

极式表示、模、复角：
$$
z = re^{i\theta}, r := |z|, \theta = arg(z) := \atan2(y,x) \in [0,2\pi) \\
e^{i\theta} = \cos\theta + i\sin \theta \\
\Rightarrow \cos(n\theta) + i\sin(n\theta) = (\cos\theta + i\sin \theta) ^ n, n \in \mathbb{Z}.
$$


## 1. 复数、复变函数

### 1.1. 直线

复平面上的直线，都可以写成
$$
\bar{\alpha} z+\alpha\bar{z} + \beta = 0
$$
的形式。

在平面坐标系，直线方程都可以表示为以下形式：
$$
Ax+By+C = 0
$$
期中 $A,B,C\in \mathbb{R}$ 且不全为零。 

设 
$$
x = \frac{z + \bar{z}}{2}, y = \frac{z - \bar{z}}{2i}
$$
那么就有
$$
\frac{A-iB}{2}z + \frac{A+iB}{2} \bar{z} + C = 0
$$
令
$$
\alpha = \frac{A+iB}{2} , \beta = C
$$
即可。

### 1.2. 圆

复平面上的圆，都可以写成
$$
z\bar{z} +\bar{\alpha} z+\alpha\bar{z} + \beta = 0
$$
的形式。
$$
x^2+y^2 = |z|^2 = z\bar{z}
$$
其余同 1.1.

### 1.3. 

$$
|z_1+z_2|^2 + |z_1-z_2|^2  = (z_1+z_2)\overline{(z_1+z_2)} + (z_1-z_2)\overline{(z_1-z_2)} \\
=(z_1+z_2)(\bar{z_1}+\bar{z_2}) + (z_1-z_2)(\bar{z_1}-\bar{z_2})  \\
=2(z_1\bar{z_1}+z_2\bar{z_2}) = 2(|z_1|^2 + |z_2|^2)\\
$$

几何意义：对于一个平行四边形，其边长的平方和等于对角线长度的平方和。

### 1.4. ***求极值

对于给定的 $r\in \mathbb{R}^+, \alpha\in \mathbb{C}$, 分别求


$$
\max_{|z|\leq r} |z^n+\alpha|, \min_{|z|\leq r} |z^n + \alpha|.
$$
解：

#### 1.4.1. 最大值：

设 
$$
I = \max_{|z|\leq r} |z^n+\alpha| = |z'|
$$

##### 1.4.1.1. $\alpha = 0$ 时，显然有

$$
|z^n+\alpha| = |z^n| \leq r^n
$$

于是
$$
I = r^n, z = re^{i\theta}, \theta\in[0,2\pi), z' = r^n e^{in\theta} 
$$

##### 1.4.1.2. $\alpha \neq 0$ 时，

$$
|z^n+\alpha| \leq |z^n| + |\alpha| \leq r^n +|\alpha|
$$

这时 $z'$ 一定满足两个不等式都取等号。

对于左侧的小于等于号，等号成立当且仅当 $\exists \lambda \in \mathbb{R}^+$， s.t. $z^n = \lambda \alpha$ 。

对于右侧的小于等于号，等号成立当且仅当 $|z| = r$ 。

这代表，$\lambda = |z^n|/|\alpha| = r^n/|\alpha|$。

于是又有 $z^n = r^n/|\alpha| \cdot \alpha = r^n e^{i \arg \alpha}$ 。
$$
\Rightarrow z = z_k = r e^{\frac{i(arg \alpha + 2k\pi)}{n}}, k = 0,1,\cdots,n-1 \\
z' = (r^n+|\alpha|) e^{i \arg \alpha}, I = r^n + |\alpha|
$$
综上，
$$
\max_{|z| \leq r} |z^n+\alpha| = \left\{
\begin{array}{ll}
r^n, & \alpha = 0 (z = re^{i\theta}, \theta \in [0,2\pi)) \\
r^n+|\alpha|, &\alpha \neq 0 (z = z_k = r e^{\frac{i(arg \alpha + 2k\pi)}{n}}, k = 0,1,\cdots,n-1)
\end{array}
\right.
$$

#### 1.4.2. 最小值

设 
$$
J = \min_{|z|\leq r} |z^n+\alpha| = |z'|
$$

##### 1.4.2.1. $\alpha = 0$ 时，显然有

$$
|z^n+\alpha| = |z^n| \geq 0
$$

于是
$$
J = 0, z' = 0
$$


##### 1.4.2.2. $0<|\alpha| \leq r^n$ 时，

令 $z^n = -\alpha， z = (-\alpha)^{1/n}$， 
$$
z = z_k = |\alpha|^{1/n} e ^{\frac{i(\arg\alpha + (2k+1)\pi)}{n}}, k = 0, 1, \cdots , n-1
$$
显然有 $z' = J = 0$.

##### 1.4.2.3. $|\alpha| > r^n$ 时，

$$
|z^n+\alpha| \geq |\alpha| - |z^n| \geq |\alpha| - r^n
$$

两个等号在 $z^n = -r^n e^{i\arg\alpha}$ 时成立。
$$
\Rightarrow z = z_k = r e^{\frac{i(arg \alpha + (2k+1)\pi)}{n}}, k = 0,1,\cdots,n-1 \\
z' = (|\alpha|- r^n)e^{i\arg\alpha},J = |\alpha| - r^n
$$
综上，
$$
\min_{|z| \leq r} |z^n+\alpha| = \left\{
\begin{array}{ll}
0, & \alpha = 0 (z = 0) \\
0, & 0<|\alpha|<r^n(z = z_k = |\alpha|^{1/n} e ^{\frac{i(\arg\alpha + (2k+1)\pi)}{n}}, k = 0, 1, \cdots , n-1) \\
|\alpha| - r^n, &|\alpha|>r^n (z = z_k = r e^{\frac{i(arg \alpha + (2k+1)\pi)}{n}}, k = 0,1,\cdots,n-1)
\end{array}
\right.
$$

### 1.5. 证明为一正三角形：

给定 $z_1, z_2, z_3 \in \C$ , 且 $|z_1|= |z_2|=|z_3|= r$，$ z_1+z_2+z_3 = 0$， 证明 $\Delta z_1z_2z_3$ 是正三角形。

证明如下：

#### 1.5.1. 证明一：

由于  $z_1 = -(z_2+z_3)$， 且 $r = |z_1|=|z_2|=|z_3|$，

因此
$$
r =|z_1| = |-(z_2+z_3)| = |z_2|+|z_3|, \\
|z_2-z_3|^2 = 2(|z_2|^2+|z_3|^2) - |z_2+z_3|^2 = 4r^2 - r^2 = 3r^2 \Rightarrow |z_2-z_3| = \sqrt{3}r,
$$
同理，  $|z_1-z_2|= |z_3-z_1| = \sqrt{3}r$。     $\blacksquare$ 

#### 1.5.2. 证明二：

设 $g(z) = \prod_{k=1} ^ 3 (z-z_k) = z^3 +az^2 + bz + c$ ，

因为 $|z_k| = r, k = 1,2,3 $，$b = z_1z_2z_3(1/z_1 + 1/z_2 + 1/z_3) = (-c)(\frac{\bar{z_1} + \bar{z_2} + \bar{z_3}}{r^2}) = \frac{\bar{a}c}{r^2}$，

且  $z_1 + z_2 + z_3 = 0$，所以

$g(z) = z^3 + c$。求其零点，则
$$
z^3 = -c = c e^{i\pi} = |c| e^{i(\pi + \theta_0)} = |c|e^{i((2k-1)\pi+\theta_0)}, \theta_0 = \arg c, \\
z = z_k = |c|^{1/3} e^{i((2k-1)\pi+ \theta_0)/3}, k = 1,2,3 \\
\Rightarrow |z_k| = |c|^{1/3}, z_{k+1}/z_k = e^{2\pi i/3}, \arg(z_2) - \arg(z_1) = 2\pi/3
$$
扩展：

对于证明为正四边形，除了  $z_1+z_2+z_3+z_4 = 0$, 还要求 $ z_1z_2 + z_1z_3 + z_1z_4 +z_2z_3 +z_2z_4 + z_3 z_4 = 0$。

如果只有第一个条件，就只能证明其为矩形（$g(z) = z^4 + bz^2 + d $）。

设 $g(z) = \prod_{k = 1} ^ 4 (z-z_k) = z^4+ az^3 + bz_2+ cz + d$,

由韦达定理， $b = d\bar{b} /r^4, c= d\bar{a}/r^2$.

质心与外接圆圆心重合，当且仅当 $a= 0$。

这时对于 $g$，  $z_3 = -z_1, z_4 = -z_2$。

第二个条件 $\Leftrightarrow b = 0$。这时 $g(z) = z^4 + d$， 因此 $z_1^2 + z_2 ^ 2 = (z_1+iz_2)(z_1-iz_2)=0$， $\arg z_2 - \arg z_1 = \pm \pi /2 $ 。

对于$2n$ 边形，需要 $n$ 个条件使得其为正 $2n$ 边形；对于$2n-1$ 边形，需要 $n-1$ 个条件使得其为正 $2n-1$ 边形。

**分圆多项式**：
$$
f(z) = (z-z_0)^n + d
$$


$\blacksquare$ 

### 1.6.

若 $f:\mathbb{C}\to\mathbb{C}$ 在  $z_0$ 连续，且 $f(z_0) \neq 0$，就一定存在 $\delta > 0$, 使得 $\forall z: |z-z_0| < \delta$， 都有 $f(z)\neq 0$ 。

证明如下：

由于  $f(z_0)\neq 0$，可以取 $\epsilon = |f(z_0)|/2 >0$。

而且
$$
\lim_{z\to z_0} f(z) = f(z_0) \\
\Rightarrow \forall \epsilon > 0, \exists \delta > 0, s.t. \\
\forall z: |z-z_0|<\delta \rightarrow |f(z) -f(z_0)| < \epsilon
$$

$$
\Rightarrow |f(z_0)|/2 > |f(z) - f(z_0)| > ||f(z)| - |f(z_0)|| \Rightarrow 0<|f(z_0)|/2 < |f(z)| < 3|f(z_0)|/2 
$$

$\blacksquare$ 

## 2. 复变函数的导数

### 2.1. 证明柯西-黎曼方程。

对于复变函数 $f:D\to \C, z_0\in D$, $f$ 在 $z_0=x_0+iy_0$ 可导，

当且仅当 其实部 $u(x,y)$, 虚部 $v(x,y)$ 在 $(x_0,y_0)$ 可微，且 $u_x = v_y, u_y =-v_x$。

证明如下：

设 $f = u + iv , u,v\in C^1 $，$f' = A+iB$。

由全微分的的定义，
$$
df = f'(z) dz \\
df = u_x dx +iv_xdx + u_ydy+iv_y dy = (u_xdx+u_ydy) + i(v_xdx+v_ydy)\\
f'(z)dz = (A+iB)(dx+idy) = (Adx-Bdy) + i(Ady + Bdx) \\
\Rightarrow  \left\{ 
\begin{array}{l}
A = u_x = v_y \\ B = v_x = -u_y
\end{array}
\right.
$$
$\blacksquare$

推论： 若 $u,v \in C^n$， 则
$$
f^{(n)}(z) = \frac{\partial^n u}{\partial x^n} + i \frac{\partial^n v}{\partial x^n}
$$
因此，对于某个解析的复变函数，实部为常数 $\Leftrightarrow$ 虚部为常数。

另外， $f(z) = \ln|f(z)|+i\arg f(z)$, 因此对于模为常数的解析函数，其复角也是常数。



### 2.2. 多项式的和形式和积形式

设 $z_k = re^{i(\theta+2(k-1)\pi/n}, f(z) = \prod_{k=1}^n (z-z_k), g(z) = z^n + (-1)^n \prod_{k=1}^n z_k$

这里 $g$ 是首一多项式，且 $f(z_k)=g(z_k) = 0, k = 1,2,\cdots, n$ 。

设 $h(z) = f(z) - g(z) $, 那么 $\mathrm{deg } (h) \leq n-1$ ，且 $h(z_k) = 0, k = 1,2,\cdots, n$

（n次多项式有超过 n 个零点，那个多项式是恒等式）

$\Rightarrow h(z)\equiv 0 \Leftrightarrow f(z) \equiv g(z),\forall z:z\in \C$ 。

### 2.3. 共轭调和函数

先定义拉普拉斯算子 (Laplacian):
$$
\Delta = \nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}
$$
调和函数$f$： $\Delta f=0$。

由柯西-黎曼方程，
$$
\frac{\partial^2u}{\partial x^2} = \frac{\partial^2 v}{\partial x \partial y},
\frac{\partial^2u}{\partial y^2} = -\frac{\partial^2 v}{\partial y \partial x}, \\
\Rightarrow \Delta u = \frac{\partial^2u}{\partial x^2} + \frac{\partial^2u}{\partial y^2} = 0
$$
解析函数的实部，一定满足拉普拉斯方程，是调和函数。

同理 $\Delta v = 0$， 于是解析函数的实部和虚部组成一对调和函数，为共轭调和函数。

### 2.4. 

如果 $f(z)$ 在 $D$ 内解析，且不是常数，则$f(D)$ 是一个二维区域。

证明：
$$
J = \frac{\partial(u,v)}{\partial(x,y)} = \left|
\begin{array}{cc}
u_x & u_y \\v_x & v_y
\end{array}
\right|
= u_xv_y-v_xu_y = u_x^2 +v_x^2 =|f'(z)|^2> 0 \\
\iint_{D'}  dudv = \iint_D Jdxdy =\iint_D |f'(z)|^2dxdy > 0 \\
$$
$\blacksquare$

### ***2.5.

对于任意的$A,B\in \R$，
$$
\cos(z) = \cos(x+iy) = A+iB
$$
有无穷多解。

证明：
$$
\cos(x+iy) = \cos(x)\cos(iy) -\sin(x)\sin(iy) = \cos(x)\frac{e^y+e^{-y}}{2} -i\sin(x)\frac{e^y-e^{-y}}{2} \\
A = \Re(cos(z)) = \cos(x)\frac{e^y+e^{-y}}{2}, B = \Im (\cos(z))=-\sin(x)\frac{e^y-e^{-y}}{2}
$$
这等价于证明 上述方程组有解。

#### 2.5.1. $B=0$ 时，

$$
\sin(x)\frac{e^y-e^{-y}}{2} = 0 \Leftrightarrow \sin(x) = 0 \lor \frac{e^y-e^{-y}}{2} = 0
$$

##### 2.5.1.1. $|A|\leq 1$:

取 $y=0 \Rightarrow \cos x = A, x= x_k = \pm\arccos A +2k\pi, k\in \Z. $

##### 2.5.1.2. $|A|>1$:

取 $\sin x = 0, \cos x = \mathrm{sgn}(A)$.
$$
\Rightarrow |A| = \frac{e^y+e^{-y}}{2} > 1
$$
令
$$
\cosh(y) := \frac{e^y+e^{-y}}{2}, y>0 \\
\cosh'(y) = \frac{e^y-e^{-y}}{2} >0,\cosh(0) = 1, \lim_{y\to+\infty} \cosh(y) \to +\infty \\
\Rightarrow \exists! y_A >0, \cosh(y_A) = |A| > 1
$$
且$\cosh$ 是偶函数，因此有 $x= \pm \arccos \mathrm{sgn}(A) + 2k\pi, y = \pm y_A, k\in\Z, y_A > 0$.

#### 2.5.2. $B \neq 0$ 时，

$$
\frac{4A^2}{(e^y+e^{-y})^2} + \frac{4B^2}{(e^y-e^{-y})^2}=1
$$

记左式 为 $g(y)$， 由于 $g$ 时偶函数，只讨论 $y>0$。 显然有
$$
\lim_{y\to 0^+} g(y) \to +\infty, \lim_{y\to +\infty}g(y) = 0
$$
而且 $g$ 在 $(0,+\infty)$ 连续，有连续函数的介值定理， $\exists y' > 0$, s.t. $g(\pm y') = 1$.

而且 $\cos(x) = 2A/(e^{y'}+e^{-y'}), \sin(x) = 2B/(e^{y'}-e^{-y'})$， $\cos^2(x)+\sin^2(x)=1$ ，

因此$(\cos(x),\sin(x)) = (2A/(e^{y'}+e^{-y'}), 2B/(e^{y'}-e^{-y'}))$ 一定对应单位圆上的某一个点，即一定存在 $x'$ 满足上述要求。

如果 $A > 0$,  $x' = \arctan \frac{B(e^{y'}+e^{-y'})}{A(e^{y'}-e^{-y'})}$，

如果  $A < 0$, $x' = \pi+ \arctan \frac{B(e^{y'}+e^{-y'})}{A(e^{y'}-e^{-y'})}$，

如果 $A = 0 $ , $\sin(x) = 2B/(e^{y'}-e^{-y'}) =\pm 1, \cos(x) = 0$, (正负取决于 y 的取值) ，$x' = \frac{(4k\pm 1)\pi}{2}$ (正负号与前方相同)。

而 $x = x' + 2k\pi$ 都是解，对于 $y=-y'$ 也可以求出相应的$x'$ ，也对应无穷多个 $x$ 。

$\blacksquare $

## 3. 复积分

### 3.1. 柯西-古萨基本定理。

对于一个在单连通区域 $D$ 内解析的函数$f:D\to \C$， 对$D$ 的分段光滑的闭曲线边界 $\partial D$ ,都有
$$
\oint_{\partial D} f(z)dz = 0
$$

#### 3.1.1. 分段光滑

$C:z(t) = x(t)+ iy(t)$  是一条光滑曲线，当且仅当

$ x,y\in C^1(a,b)$ 且  $z'(t)\neq 0,\forall t: t\in(a,b).$

$C$ 是一条分段光滑曲线，当且仅当其是由有限段光滑曲线拼接而成的。

#### 3.1.2. 证明：

设 $f = u + iv$，

则由 0.1.，
$$
\oint _{\partial D} f(z)dz =\oint _{\partial D} (u+iv)(dx+idy)= \oint_{\partial D} (udx-vdy) + i \oint_{\partial D}(udy+vdx) \\
= \iint_D (-v_x-u_y)dxdy + i\iint_D (u_x-v_y)dxdy
$$
由2.1.，$v_x=-u_y, u_x=v_y$, 于是  $\oint _{\partial D} f(z)dz = 0$.   $\blacksquare$

### 3.2. 

$$
I_n =\oint_{|z-z_0|=r>0} \frac{dz}{(z-z_0)^n}, n\in \Z
$$

设 $ z = z_0 + re^{i\theta}, \theta\in[0,2\pi], dz = ire^{i\theta} d\theta$,
$$
I_n =\oint_{|z-z_0|=r>0} \frac{dz}{(z-z_0)^n} = \int_0^{2\pi} \frac{rie^{i\theta}d\theta}{r^ne^{in\theta}} = \frac{i}{r^{n-1}}\int_0^{2\pi} e^{i(1-n)\theta}d\theta 
= \left\{
\begin{array}{ll}
2\pi i, & n = 1 \\
0, & n \neq 1
\end{array}
\right.
$$

### 3.3. 

$$
I_n = \oint_{|z|=1} \frac{1-\cos 4z^5}{z^n}dz = \oint_{|z|=1}  \sum_{k = 1} ^ {+\infty} \frac{(-1)^k (4z^5)^{2k}}{z^n (2k)!}dz = \sum_{k = 1} ^ {+\infty} \frac{(-1)^k 4^{2k} }{(2k)!}\oint_{|z|=1} z^{10k-n}dz
$$

当 $10k -n = -1 \Leftrightarrow n = 10k + 1 $ ，
$$
k = (n-1)/10, I_n = 2\pi i\cdot \frac{(-1)^{(n-1)/10} 4^{(n-1)/5}}{((n-1)/5)!}
$$
否则 $I_n = 0$。 综上，
$$
I_n = \left\{
\begin{array}{ll}
\frac{2\pi i(-1)^{(n-1)/10} 4^{(n-1)/5}}{((n-1)/5)!}, & n>1 \land n \equiv 1 (\mod 10 ) \\
0, & \text{otherwise}
\end{array}
\right.
$$

### 3.4. 

$$
I_{n,m} = \oint_{|z|=1} \frac{\sin z^m}{z^n}dz = \sum_{k = 0} ^ {+\infty} \frac{(-1)^k}{(2k+1)!}\oint_{|z|=1} z^{(2k+1)m-n}dz = \left\{
\begin{array}{ll}
\frac{2\pi i(-1)^{(n-m-1)/(2m)} }{((n-1)/m)!}, & n \equiv m + 1 (\mod 2m ) \\
0, & \text{otherwise}
\end{array}
\right.
$$

### 3.5. 复合闭路定理

设 $C, C_1,C_2, \cdots, C_n$ 是简单闭曲线。 $C_1, C_2, \cdots, C_n$ 完全包含在 $C$ 内，$C_1,\cdots C_n$ 互不相交，互不包含。

若 $f$ 在 $C$ 内， $C_1, C_2, \cdots, C_n$ 外的区域内解析，在 $C_1, C_2, \cdots, C_n$ 上连续，则
$$
\oint_C f(z)dz = \sum_{k = 1} ^ n \oint_{C_k} f(z)dz
$$

#### 3.5.1. 证明：

$n=1$时，将 $C$ 与 $C_1$ 以一段直线 $l$ 连接。那么，$\Gamma_C = C \cup l^+\cup C_1^- \cup l^-$ 为一分段光滑闭曲线，且 $f$ 在 $\Gamma_C$ 围成的区域内解析，因此
$$
0 = \oint_{\Gamma_C}f(z)dz = (\oint_C + \int_{l^+}+\int_{l^-}+\oint_{C_1^-})f(z)dz \Rightarrow \oint_{C} f(z)dz = \oint_{C_1} f(z)dz
$$
 而原命题为 $n=1$ 的推广。   $\blacksquare$

#### 3.5.2. 推论：闭路变形原理

简单闭曲线$C'$ 经简单闭曲线$C$连续变化而成。只要$C'$内不解析的点，与$C$ 内不解析的点完全一致，
$$
\oint_{C'} f(z)dz = \oint_C f(z)dz
$$

#### 3.5.3. 例

$g$ 在 $|z|\leq 4$ 处处可导，$f(z) = \frac{2}{z-1} +  \frac{1}{z-2} +  \frac{4}{z-3} + g(z)$， 则
$$
\oint_{|z|=4}f(z)dz= \oint_{|z|=4}\frac{2}{z-1}dz + \oint_{|z|=4} \frac{1}{z-2} dz + \oint_{|z|=4} \frac{4}{z-3} dz + \oint_{|z|=4}g(z)dz = 2(2\pi i) + 2\pi i + 4(2\pi i) + 0 = 14\pi i
$$

### 3.6. *柯西高阶导数公式

设 $z_0$ 在简单光滑闭曲线 $C$ 内， $f$ 在 $D$ 内解析， 
$$
f^{(n)}(z_0) = \frac{n!}{2\pi i} \oint_C \frac{f(z)dz}{(z-z_0)^{n+1}}
$$

#### 3.6.1. 证明：

（*杨大伯用泰勒级数证明，但复变解析函数的泰勒级数本身是用上述公式推导的，因此有循环论证之嫌，以下给出笔者的证明）



$n=0$ 时，

设 $g(z) = \frac{f(z)-f(z_0)}{z-z_0} (z\neq z_0) $ 和 $g(z_0) = f'(z_0)$, 那么由闭路变形原理和 $g$ 在 $D-\{z_0\}$ 内解析，在 $D$ 内连续，就有
$$
\oint_C g(z) dz = \oint_{|z-z_0| = r < \delta(\epsilon)} \frac{f(z)-f(z_0)}{z-z_0}dz \leq \oint_{|z-z_0| = r < \delta(\epsilon)} \frac{|f(z)-f(z_0)|}{|z-z_0|}|dz| < \frac{\epsilon}{r}\oint_{|z-z_0| = r < \delta(\epsilon)} |dz| = 2\pi \epsilon
$$
$\forall \epsilon\in \R^+$ 成立，令 $\epsilon\to 0$ ,则 $\oint_C g(z) dz \to 0$ 
$$
\Rightarrow \oint_C \frac{f(z)}{z-z_0} dz = \oint_C \frac{f(z_0)}{z-z_0} dz = 2\pi i f(z_0)
$$
$\square$

$n = k$ 时假设结论成立，则对于 $ n = k + 1 $， 
$$
f^{(k+1)}(z_0) = \lim_{\Delta z \to 0} \frac{f^{(k)}(z_0+\Delta z) - f^{(k)}(z_0)}{\Delta z} = \lim_{\Delta z \to 0}  \frac{k!}{2\pi i \Delta z} \oint_C \left(\frac{1}{(z-z_0-\Delta z)^{k+1}}-\frac{1}{(z-z_0)^{k+1}}\right)f(z)dz \\
= \lim_{\Delta z \to 0} \frac{k!}{2\pi i \Delta z} \oint_C \frac{(z-z_0)^{k+1} - (z-z_0- \Delta z)^{k+1}}{[(z-z_0-\Delta z)(z-z_0)]^{k+1} }f(z)dz \\
=  \lim_{\Delta z \to 0} \frac{k!}{2\pi i} \oint_C \frac{(z-z_0)^{k} + (z-z_0)^{k-1}(z-z_0- \Delta z) + \cdots + (z-z_0- \Delta z)^{k}}{[(z-z_0-\Delta z)(z-z_0)]^{k+1} }f(z)dz \\
= \frac{k!}{2\pi i} \oint_C \frac{(k+1)(z-z_0)^{k}}{(z-z_0)^{2k+2} }f(z)dz = \frac{(k+1)!}{2\pi i} \oint_C \frac{f(z)dz}{(z-z_0)^{k+2} }dz
$$
$\blacksquare$

#### 3.6.2. 均值公式

$$
f(z_0) = \frac{1}{2\pi i} \oint_{|z-z_0| = r > 0} \frac{f(z)dz}{z-z_0} = \frac{1}{2\pi i} \int_0^{2\pi} \frac{f(z_0+re^{i\theta})ire^{i\theta}d\theta}{re^{i\theta}} = \frac{1}{2\pi} \int_0^{2\pi} f(z_0+re^{i\theta})d\theta
$$

### 3.7. 极值原理

#### 3.7.1. 最大模原理

设$D$ 是一个有界区域， $\partial D$ 是它的边界，若 $f$ 在  $D$ 内可导， $\partial D$ 上连续，则有
$$
\max_{z\in\bar{D}}|f(z)| = \max_{z\in\partial D} |f(z)|
$$
证明：

设 $z_0\in D$ , s.t. 
$$
f(z_0) = \max_{z\in\bar{D}}|f(z)|
$$
取 $r >0$ ,s.t. $\delta(z_0,r)\subset D$,

由均值公式， $ f(z_0) = \frac{1}{2\pi} \int_0^{2\pi} f(z_0+re^{i\theta})d\theta$ 。 两边取模，
$$
|f(z_0)| = \frac{1}{2\pi} \left|\int_0^{2\pi} f(z_0+re^{i\theta})d\theta\right| \leq \frac{1}{2\pi} \int_0^{2\pi} |f(z_0+re^{i\theta})|d\theta \leq \frac{1}{2\pi} \int_0^{2\pi} |f(z_0)|d\theta = |f(z_0)|
$$
因此上式的每一个小于等于都应该相等，这就代表 $|f(z)|$ 在 $z_0$ 的邻域内恒为 $|f(z_0)|$，于是 $f$ 在 $z_0$ 的邻域内为常数。

如果 $f$ 不是常函数，就必然有矛盾。加上$f$ 在 $\partial D$ 内连续，$f$ 的最大值必然在边界上。  $\blacksquare$

#### 3.7.2. 最小模原理

设 $g(z) = 1/f(z)$ ，且 $f$ 的像不包含原点，那么 $g'(z) = -f'(z)/[f(z)]^2 $ ，$g$在 $D$ 内解析，在$\partial D$ 上连续。

由最大模原理， 
$$
\max_{z\in\bar{D}}|g(z)| = \max_{z\in\partial D} |g(z)| 
\Leftrightarrow \frac{1}{\min_{z\in\bar{D}}|f(z)|} = \frac{1}{\min_{z\in\partial{D}}|f(z)|}  \\
\Leftrightarrow \min_{z\in\bar{D}}|f(z)| = {\min_{z\in\partial{D}}|f(z)|}
$$

#### 3.7.3. 最大值原理

若 $u$ 是 $D$ 内的调和函数，$D$ 是有界区域，则有
$$
\max_{(x,y)\in\bar{D}}u(x,y) = \max_{(x,y)\in\partial D} u(x,y)
$$
证明：

令 $g(z) = \exp(f(z))= \exp(u+iv)$, $g'(z) = f'(z)\cdot \exp(f(z))$, $e^u = |e^{u+iv}| = |g(z)|$
$$
\exp (\max_{(x,y)\in\bar D} u)
=\max_{(x,y)\in\bar D} e^{u}=
\max_{z\in\bar{D}}|g(z)| = \max_{z\in\partial D} |g(z)|  = \max_{z\in\partial D} e^u=\exp (\max_{(x,y)\in\partial D} u)
$$
 $\blacksquare$

#### 3.7.4. 最小值原理

$h(z) = \exp(-f(z))$,  $|h(z)|=e^{-u}$
$$
\exp (-\min_{(x,y)\in\bar D} u)
=\max_{(x,y)\in\bar D} e^{-u}=
\max_{z\in\bar{D}}|h(z)| = \max_{z\in\partial D} |h(z)|  = \max_{z\in\partial D} e^{-u}=\exp (-\min_{(x,y)\in\partial D} u)
$$
 $\blacksquare$

### 3.8. ***柯西积分不等式

设$f$ 在 $|z-z_0|<r$ 内解析，$|z-z_0|=r$ 连续， $M(r) = \max_{|z-z_0|\leq r} |f(z)|$, 则
$$
|f^{(n)}(z_0)| \leq \frac{n!M(r)}{r^n}
$$

##### 3.8.1. 证明：

对柯西高阶导数公式两侧取模，
$$
|f^{(n)}(z_0)| = \left|\frac{n!}{2\pi i} \oint_{|z-z_0|=r} \frac{f(z)dz}{(z-z_0)^{n+1}}\right| \leq \frac{n!}{2\pi} \oint_{|z-z_0|=r} \frac{|f(z)||dz|}{|z-z_0|^{n+1}} \\
\leq \frac{n!}{2\pi} \oint_{|z-z_0|=r} \frac{M(r)|dz|}{r^{n+1}}
= \frac{n!M(r)}{r^n}
$$
$\blacksquare$

##### 3.8.2.

$f$ 处处可导，且  $\exists M > 0, n\in \Z^+$， s.t. $\forall z : z\in \C$ ，都有
$$
|f(z)| \leq M \sum_{k=0}^n |z|^k
$$
证明 $f$ 是一个次数不大于 $n$ 的多项式。

证明如下：

令 $M(r) = M \sum_{k=0}^n r^k$，立即有
$$
|f(z)|\leq M(r) = M \sum_{k=0}^n r^k
$$
那么，由 3.8.1., 
$$
|f^{(n+j)}(0)| \leq \frac{(n+j)!M(r)}{r^{n+j}} = M(n+j)!\sum_{k=0}^n r^{k-n-j}, j = 1,2,3,\cdots
$$
令 $r\to +\infty$， 则 $|f^{(n+j)}(0)|\to 0 \Rightarrow f^{(n+j)}(0) = 0$

因此，对 $f$ 在 $z=0$ 处泰勒展开，
$$
f(z) = \sum_{k = 0} ^ {+\infty} \frac{f^{(k)}(0)}{k!}z^k \equiv \sum_{k = 0} ^ {n} \frac{f^{(k)}(0)}{k!}z^k,
$$
是一个次数不大于 $n$ 的多项式。 $\blacksquare$

### 3.9. Liouville 定理

有界整函数是常数。

证明：

设$f$ 是一个有界整函数， $M$ 满足 $\forall z: z\in \C$ , $|f(z)|\leq M$， 则对 3.8.1. 的 $r\to +\infty$,
$$
|f^{(n)}(0)| \leq \frac{n!M}{r^n} \to 0(n \in \Z^+)\Rightarrow f(z) = \sum_{k=0} ^{+\infty} \frac{f^{(k)}(0)}{k!}z^k \equiv f(0)
$$
$\blacksquare$

#### 3.9.1. Little Picard's theorem

$f:\C\to \C - \{w_1,w_2\}$ 是整函数，则$f$ 是常数。 $(g(z)= f(z) -w_1)(f(z)-w_2))$ 

#### 3.9.2. 代数学基本定理

设 
$$
P_n(z) = \sum_{k=0} ^ n c_k z^k, n\geq 1, c_k\in \C, c_n\neq 0
$$
则 
$$
P_n(z) = c_n\prod_{k=1} ^n (z-z_k)
$$
 或 $P_n(z)$ 在 $\C$ 上至少有一个零点。

证明：
$$
\lim_{z\to\infty}|P_n(z)| = \lim_{z\to\infty}|z^n| \lim_{z\to\infty} |c_n+ c_{n-1}/z + \cdots+ c_0/z^n| =\lim_{z\to \infty} |z^n||c_n| \to +\infty
$$
​	引理：

​	如果 $f$ 处处连续，且 $\lim_{z\to \infty} f(z) = 0$ ，则 $f$ 有界。

​	证明：

​	由定义知，$\forall \epsilon > 0, \exists M > 0$  s.t. $\forall z: |z|>M, |f(z)|< \epsilon$ 。

​	另一方面， $f$ 处处连续， 因此由最大模原理，知 $f$ 在 $|z|\leq M$ 内一定存在最大模 $M_1$, 使得 $|f(z)| \leq M_1$, 所以 $|f(z)|\leq \max \{\epsilon, M_1\}$.



设 $f(z) = 1/P_n(z)$, $f'(z) = -P_n(z)/[P_n(z)]^2$ ，如果 $P_n$ 没有零点，则由 1.6.及引理知$f$ 是有界的整函数，由 3.9. 知 $f$ 一定为常数$\Rightarrow P_n$ 为常数，与$P_n(z)$ 是多项式矛盾，因此一定存在 $z_1\in \C$ 使得 $P_n(z_1) =0$ ，所以 $P_n(z) = (z-z_1)P_{n-1}(z)$ 。

$\blacksquare$

## 4. 级数

$$
\zeta(2k) = (-1)^{k-1} 2^{k-1} \frac{B_k}{(2k)!}\pi^{2k} \\
\zeta(3) = \sum_{n = 0} ^ {+\infty} \frac{1}{n^3} \in \R - \Q \\
\zeta\left(\frac{1}{2}+iy\right) = 0,
$$

$y$ has infinite solutions --> Riemann conjecture.

($\zeta(4)$ is relevant to Wien's displacement law)

### 4.1. 幂级数

$$
f(z) = \sum_{k=0} ^ {+\infty} f_k(z) 
$$

称为复级数。

$f_k(z) = a_k$ ，常数项级数。

$f_k(z) = c_k(z-z_0)^k$，幂级数(power series)。

$f_k(z) = c_k r^k e^{ik\theta}$ ，傅里叶级数。

$f_k(z) = \frac{1}{n^z}$ ，
$$
\zeta(s) = \sum_{n = 1} ^ {+\infty} \frac{1}{n^s} = \prod_{p \text{ is prime}} \frac{1}{1-p^{-s}}
$$

### 4.2. ***收敛半径，Abel 定理。

#### 4.2.1. Abel 定理。

对于一个幂级数 $f(z) = \sum_{n=0} ^ {+\infty} c_nz^n$， 

当$f(z_1)$ 收敛，则 $\forall z: |z| < |z_1|$ ，都有 $f(z)$ 绝对收敛，即 $\sum_{n=0} ^ {+\infty} |c_nz^n| < +\infty$ 。

当 $f(z_2)$ 发散($f(z_2)$ 不存在或 $|f(z_2)| = +\infty$) ， 则 $\forall z: |z| > |z_2|$ ， $f(z)$ 发散。

#### 4.2.2. 收敛半径：

如果 $\exists R\in \R^+$ , 使得 $f(z) = \sum_{n=0} ^ {+\infty} c_nz^n$ 在 $|z| < R$ 时绝对收敛，$|z|>R$ 时发散，则$R$ 是 $f(z)$ 的收敛半径。

#### 4.2.3. 例子

##### 4.3.2.1. 收敛圆上处处发散：

$$
f(z) = \sum_{n = 0} ^ {+\infty} z^n = \frac{1}{1-z} ,|z|<1, R=1
$$

证明： 幂级数收敛的必要条件，是它的每一项在 $n\to+\infty$ 时，都应该趋向于零。但是，当 $|z|=1$， $|z^n| =1 \not\to 0$，而且

当 $|z|<1$ 时
$$
f(z) = \lim_{n\to +\infty} \sum_{k = 0} ^ {n} z^k = \lim_{n\to +\infty} \frac{1-z^n}{1-z} = \frac{1}{1-z}
$$
  因此 $R=1$。

##### 4.3.2.2. 收敛圆上处处(绝对)收敛：

$$
f(z) = \sum_{n = 1} ^ {+\infty} \frac{z^n}{n^2},|z|<1, R=1
$$

这是因为
$$
|f(z)| \leq \sum_{n = 0} ^ {+\infty} \left|\frac{z^n}{n^2}\right| =\sum_{n = 0} ^ {+\infty} \frac{1}{n^2} = \frac{\pi^2}{6} < +\infty
$$

##### 4.3.2.3. 收敛圆上条件收敛：

$$
f(z) = \sum_{n = 1} ^ {+\infty} \frac{z^n}{n},|z|<1, R=1
$$

除了 $z=1$ 外，其他地方都收敛：
$$
f(re^{i\theta}) = \sum_{n = 1} ^ {+\infty} \frac{r^n e^{in\theta}}{n} = \sum_{n = 1} ^ {+\infty} \frac{r^n \cos{n\theta}}{n} + i\sum_{n = 1} ^ {+\infty} \frac{r^n \sin{n\theta}}{n}
$$
另外， 
$$
f(z) = \sum_{n = 1} ^ {+\infty} \frac{z^n}{n} = \int_0^z\sum_{n = 0} ^ {+\infty} {(z')^n}dz' = \int_0^z \frac{dz'}{1-z'} = -\ln(1-z)
$$
因此，
$$
f(re^{i\theta}) = -\ln(1-re^{i\theta})
$$
$r\to 1^-,\theta\in[0,2\pi)$  时，$1-re^{i\theta} \to 1-e^{i\theta}$, 
$$
1-e^{i\theta} = 1-\cos\theta -i\sin\theta = 2\sin^2(\theta/2) -2i\sin(\theta/2)\cos(\theta/2) = 2\sin(\theta/2)(\sin(\theta/2)+i\cos(\theta/2))
$$
因此 $\Re(1- re^{i\theta})\geq 0$， 
$$
f(z) = -\ln(1-z) = -\ln|2\sin(\theta/2)| +i(\pi-\theta)/2
$$
  所以 
$$
\sum_{n = 1} ^ {+\infty} \frac{r^n \cos{n\theta}}{n} = -\ln\left|2\sin\frac{\theta}{2}\right|,\sum_{n = 1} ^ {+\infty} \frac{r^n \sin{n\theta}}{n} =\frac{\pi-\theta}{2} , \theta\in[0,2\pi)
$$
立即得到， $\theta=0$ 时， $\sin(\theta/2) = 0$，级数发散，$\theta\neq 0$ 时级数收敛。

### 4.3. 条件收敛

$f(z_0)$ 条件收敛，则收敛半径 $R = |z_0|$。

证明：

由 Abel 定理，$\forall z: z\in \C \land |z|< |z_0|,f(z)$ 绝对收敛，于是 $R\geq |z_0|$。

另一方面，如果 $R >|z_0|$， 那么 $z_0$ 在收敛圆内，再由 Abel 定理， $f(z_0)$ 绝对收敛，与题设矛盾，因此 $R=|z_0|$。

$\blacksquare$

### 4.4. 其他计算收敛半径的公式：

下面都假设极限存在。
$$
\lim_{n\to+\infty} \left|\frac{c_{n+1}}{c_n}\right| = \frac{1}{R}, 
\lim_{n\to+\infty} \sqrt[n]{|c_n|} = \frac{1}{R},
$$
如果存在$m$ , s.t. m 是$f$ 的奇点的最小模，则 $R=m$。

### 4.5. ***

$c_n = a_n+ib_n$，$a_n,b_n\in\R$ , $n\geq 0$。

设 $R>0$ (或$R=+\infty$) 是 $\sum_{n=0} ^ {+\infty} c_n z^n$ 的收敛半径，

设 $R_1>0$ (或$R_1=+\infty$) 是 $\sum_{n=0} ^ {+\infty} a_n z^n$ 的收敛半径，

设 $R_2>0$ (或$R_2=+\infty$) 是 $\sum_{n=0} ^ {+\infty} b_n z^n$ 的收敛半径。 则 $R =\min\{R_1,R_2\}$。

证明：

不失一般性，设 $R_1\leq R_2$（否则可以求$-if(z)$ 的收敛半径）。

引理：

​	若$\sum_{n=0} ^{+\infty} c_nz^n$ 的收敛半径为 $r$，$\sum_{n=0} ^{+\infty} c_n'z^n$ 的收敛半径为 $r'$，且 $\forall n: n\in \N$ 都有 $|c_n'|\leq |c_n|$，则$r'\geq r$。

​	证明：

​	$\forall z: z\in \C, |z|<r$ ,
$$
|c_n'| \leq |c_n| \Rightarrow |c_n'z^n| \leq |c_nz^n| \Rightarrow \sum_{n=0} ^ {+\infty} |c_n' z^n| \leq \sum_{n=0} ^ {+\infty} |c_n z^n| <+\infty
$$
​	$\Rightarrow \sum_{n=0} ^ {+\infty} c_n' z^n$  绝对收敛，因此 $r'\geq r$。 $\square$

回到原题，由定义显然有

$|c_n| =\sqrt{a_n^2 + b_n^2} \geq |a_n|$ ，因此 $R_1\geq R$。

另一方面，如果 $R < R_1(\leq R_2)$, 可以设 $x_0 = (R+R_1)/2$，

由于 
$$
\sum_{n=0} ^ {+\infty} c_n z^n \equiv \sum_{n=0} ^ {+\infty} a_n z^n + i \sum_{n=0} ^ {+\infty} b_n z^n
$$
令 $z=x_0$，恒等式的左端发散，但右端两个级数都收敛，矛盾，因此只能有 $R=R_1$。

$\blacksquare$

### 4.6. 分片函数

$|z|>1$时， $\frac{1}{|z|^2} < 1$ ， $\frac{1}{1+z^2}= \frac{1}{z^2(1+z^{-2})}=\frac{1}{z^2}\sum_{n=0} ^{+\infty} \frac{(-1)^n}{z^{2n}} = \sum_{n=0} ^{+\infty} \frac{(-1)^n}{z^{2(n+1)}}$

因此，
$$
f(z) = \frac{1}{1+z^2} = 
\left\{
\begin{array}{ll}
\sum_{n=0} ^ {+\infty} (-1)^nz^{2n}, & |z|<1 \\
\sum_{n=0} ^ {+\infty} \frac{(-1)^n}{z^{2(n+1)}}, & |z|>1 \\
\frac{1}{1+z^2}, & |z|=1, z\neq \pm i
\end{array}
\right.
$$
投影在实轴即有
$$
f(x) = \frac{1}{1+x^2} = 
\left\{
\begin{array}{ll}
\sum_{n=0} ^ {+\infty} (-1)^nx^{2n}, & |x|<1 \\
\sum_{n=0} ^ {+\infty} \frac{(-1)^n}{x^{2(n+1)}}, & |x|>1 \\
\frac{1}{2}, & |x|=1
\end{array}
\right.
$$

### 4.7. 洛朗级数

$$
\sum_{n=-\infty}^{+\infty} c_nz^n
$$

叫 $z$ 的L-级数。

$c_{-n} = 0, n\geq 1$ 时，$ f(z) = \sum_{n=0}^{+\infty} c_nz^n$ 是 T-级数。

对于$f$ 的某奇点 $z_k$，
$$
\oint_{|z-z_k| = \epsilon} f(z)dz = \oint \sum_{n=-\infty}^{+\infty} c_n^{(k)}z^n dz = 2\pi i c_{-1} ^{(k)}
$$
因此，如果 $m$ 是 $C$ 围成的区域内 $f$ 的奇点的个数，
$$
\oint _C f(z)dz = 2\pi i\sum_{k=1} ^ m c_{-1}^{(k)}
$$
以下给出求洛朗级数的例子。

#### 4.7.1. 

求 $f(z) = \frac{1}{z-a}$ 在 $z_0=b$ 的 L-级数， $b\neq a$。

解：
$$
f(z) = \frac{1}{z-a} = \frac{1}{(z-b)-(a-b)} = \frac{1}{(b-a)\left(1-\frac{z-b}{a-b}\right)} = \frac{1}{b-a} \sum_{n=0} ^ {+\infty}\left(\frac{z-b}{a-b}\right)^n , c_n = -\frac{1}{(a-b)^n},\\
\left|\frac{z-b}{a-b}\right|<1 \Rightarrow |z-b| < |a-b|=R
$$

 #### 4.7.2. 收敛内径、外径

$f(z) = \sum_{n=0} ^{+\infty} \frac{z^n}{a^n}+\sum_{n=0} ^{+\infty} \frac{b^n}{z^n} , |b| < |z| < |a|$ 

#### 4.7.3. 洛朗级数的系数

设 $C:|z-z_0| = \epsilon > 0。对 $$f$ 于 $z_0$ 处，展开其洛朗级数。 
$$
\oint_{C} \frac{f(z)dz}{(z-z_0)^{n+1}} = \oint_C \sum_{m = -\infty} ^ {+\infty} \frac{c_m dz}{(z-z_0)^{n+1-m}} = 2\pi i c_n \Rightarrow c_n = \frac{1}{2\pi i }\oint_{C} \frac{f(z)dz}{(z-z_0)^{n+1}}, n\in \Z
$$
与泰勒级数的区别：泰勒级数要求 $f$  $n$ 阶可导，而洛朗级数不要求。如果 $f$ $n$ 阶可导， $c_n = \frac{f^{(n)}(z_0)}{n!}$ ，就退化为泰勒级数。

#### 4.7.4.

$f(z) = \frac{1}{(z-1)(z-2)} = \frac{1}{1-z} - \frac{1}{2-z}$ 在 $0<|z|<1, 1<|z|<2$ 展开其洛朗级数。

 $0<|z|<1$:
$$
f(z) = \sum_{n = 0} ^ {+\infty} z^n -\frac{1}{2}\sum_{n = 0} ^ {+\infty} \left(\frac{z}{2}\right)^n = \sum_{n = 0} ^ {+\infty} \left(1-\frac{1}{2^{n+1}}\right)z^n  ,c_n =
\left\{
\begin{array}{ll}
1-\frac{1}{2^{n+1}}, & n \geq 0 \\
0, & n < 0
\end{array}
\right.
$$


 $1<|z|<2$:
$$
f(z) = -\frac{1}{z}\sum_{n = 0} ^ {+\infty} \frac{1}{z^n} -\frac{1}{2}\sum_{n = 0} ^ {+\infty} \left(\frac{z}{2}\right)^n = -\sum_{n = -\infty} ^ {-1} z^n-\sum_{n = 0} ^ {+\infty} \frac{1}{2^{n+1}}z^n  ,\\
c_n =
\left\{
\begin{array}{ll}
-\frac{1}{2^{n+1}}, & n \geq 0 \\
-1, & n < 0
\end{array}
\right.
$$

#### ***4.7.5.

求 
$$
J = \oint_{|z|=r>1} \frac{z^3e^{1/z}}{1+z}dz
$$
解：

令 $z = 1/t$, $dz = -dt/t^2$，$z=re^{i\theta}\Rightarrow t = r^{-1}e^{-i\theta}, \theta \in [0,2\pi]$
$$
J = -\oint_{|t|=1/r<1} -\frac{e^tdt}{t^4(1+t)}
$$
而
$$
\frac{e^t}{1+t} = \left(1 + t+\frac{1}{2}t^2 + \frac{1}{6}t^3+\cdots\right)(1-t+t^2-t^3+\cdots)
$$
$t^3$ 的系数为 $-1+1-1/2+1/6=-1/3$，
$$
J = \oint_{|t|=1/r} \frac{e^tdt}{t^4(1+t)} = \oint_{|t|=1/r} -\frac{dt}{3t} = -\frac{2\pi i}{3}
$$

#### 4.7.6. 

$$
J_n = \oint_{|z|= r>1} \frac{dz}{1+z^n}, n\in \Z^+
$$

*建议留待学习第五章时计算。

## 5. 留数

$$
f(z) = \sum_{n=-\infty} ^{+\infty} c_nz^n, \oint_{C:|z|=r} f(z)dz = \sum_{n=-\infty} ^{+\infty} c_n\oint_C z^ndz = 2\pi i c_{-1} \\
$$

### 5.1. 定义

#### 5.1.1. 孤立奇点、非孤立奇点

**奇点**：不解析的点

**孤立奇点**：去心邻域内解析的奇点

非孤立奇点：“不是孤立的”奇点，分为聚点（奇点的极限序列），自然边界（非孤立点集）。

下面只讨论孤立奇点，因为非孤立奇点不是解析函数的讨论对象。

对于一个孤立奇点，按洛朗展开的性质又分为三种：

**极点**：洛朗级数存在有限个负幂项。

按照上述对洛朗级数的定义，如果 $\exists N\in \N, \forall n: n\in \N,n > N$ 都有 $c_{-n} = 0$，那么称那个孤立奇点为 **$N$ 级极点**。

**可去奇点**：洛朗级数不存在负幂项，**“零级极点”**。

**本性奇点**：洛朗级数的负幂项有无穷多个，**“$\infty$ 级极点”**。

对于无穷远点 ($z=\infty$)，将极点的 $c_{-n}$ 换成 $c_n$ 即可。

#### 5.1.2. 例子：

例1：

$f(z) = |z|^2 =z \bar{z}$ , $\Rightarrow f'(0) = 0$，但其他点都不可导，因此复平面上所有的点都是 $f$   的奇点，是自然边界。

例2：

$f(z) = \frac{1}{\sin(z^{-1})}$ ，$z_k = \frac{1}{k\pi}$ 。 如果 $z_0=0$，则 $z_k\to z_0, k\to +\infty$，所以 $z_0=0$ 是 $f$ 的非孤立奇点，是一个聚点。

例3：

$f(z) = \frac{\sin z}{z} = \sum_{n=1}^{+\infty}\frac{(-1)^nz^{2(n-1)}}{(2n-1)!}\to 1, z\to 0$，因此 $z_0=0$ 是 $f$ 的可去奇点。

可去奇点的判别法：1. 按定义 2. $\lim_{z\to z_0} f(z)$ 存在且有限。

例4：

$f(z) = \frac{\sin z}{z^2}$ ， $z_0=0$ 是 $f$ 的一阶极点。

例5：

$f(z) = \exp(1/z)$，$z_0=0$ 是 $f$ 的本性奇点。

### 5.2. 解析函数零点的孤立性定理

对于解析函数 $f$ ，如果 $f(z)\not\equiv 0$，且存在$z_0\in \C$， $f(z_0)=0$，则存在$n\in \Z^+$, 使 $f(z) = (z-z_0)^n \varphi(z)$， 这里 $\varphi(z)$ 在 $z_0$ 解析，且 $\varphi(z_0)\neq 0$。

#### 5.2.1. 证明：

$f(z_0)=0\Rightarrow$
$$
f(z) = \sum_{k=n} ^{+\infty} \frac{f^{(k)}(z_0)}{k!}(z-z_0)^k = (z-z_0)^n  \sum_{k=0} ^{+\infty} \frac{f^{(n+k)}(z_0)}{(n+k)!}(z-z_0)^k := (z-z_0)^n \varphi(z) \\
\varphi(z) = \frac{f(z)}{(z-z_0)^n}, \varphi'(z) = \frac{f'(z)(z-z_0)^n - nf(z)(z-z_0)^{n-1}}{(z-z_0)^{2n}}
$$
因此  $z_0$ 是 $\varphi(z)$ 的一个孤立奇点。

而且按定义，
$$
\lim_{z\to z_0} \varphi(z) = \lim_{z\to z_0}\sum_{k=0} ^{+\infty} \frac{f^{(n+k)}(z_0)}{(n+k)!}(z-z_0)^k =  \frac{f^{(n)}(z_0)}{n!}
$$
存在且有限，因此 $z_0$ 是 $\varphi(z)$ 的可去奇点，所以 $\varphi(z)$ 在 $z_0$ 解析。

#### 5.2.2. 洛必达法则

Recall: 单值实变函数的洛必达法则，用柯西中值定理证明。

证明：

设$f(z) = (z-z_0)^n\varphi(z)$ ，$g(z) = (z-z_0)^m\psi(z)$   ，$\frac{f(z)}{g(z)} = \frac{(z-z_0)^n \varphi(z)}{(z-z_0)^m \psi(z)} = (z-z_0)^{n-m}\frac{\varphi(z)}{\psi(z)}$。
$$
\frac{f'(z)}{g'(z)} = \frac{n(z-z_0)^{n-1}\varphi(z) + (z-z_0)^n\varphi'(z)}{m(z-z_0)^{m-1}\psi(z) + (z-z_0)^m\psi'(z)} = \frac{n(z-z_0)^{n-m}\varphi(z) + (z-z_0)^{n-m+1}\varphi'(z)}{m \psi(z) + (z-z_0)\psi'(z)}
$$
如果 $\lim_{z\to z_0} \frac{f'(z)}{g'(z)}$ 存在，$(n=m) $，则
$$
\lim_{z\to z_0} \frac{f'(z)}{g'(z)} =\lim_{z\to z_0} \frac{n(z-z_0)^{n-m}\varphi(z) + (z-z_0)^{n-m+1}\varphi'(z)}{m \psi(z) + (z-z_0)\psi'(z)} = \lim_{z\to z_0} \frac{n\varphi(z) + (z-z_0)\varphi'(z)}{m \psi(z) + (z-z_0)\psi'(z)} =\frac{\varphi(z_0)}{\psi(z_0)} , \\
\lim_{z\to z_0} \frac{f(z)}{g(z)} = \lim_{z\to z_0}(z-z_0)^{n-m}\frac{\varphi(z)}{\psi(z)} = \frac{\varphi(z_0)}{\psi(z_0)}
$$
$n>m$ 时显然为零，$n<m$ 时，极限为无穷。

$\blacksquare$

### 5.3. 解析函数的唯一性定理

$f,g$ 在 $D$ 内处处可导，而且存在 $z_0\in D, z_k\in D$, $\lim_{k\to +\infty} z_k = z_0$ 且 $f(z_k) =g(z_k)， \forall k:k\in \N^+$， 则 $\forall z: z\in D$, $f(z) \equiv g(z)$。

证明：

令 $h(z)=f(z)-g(z) \Rightarrow h(z_k) = (f-g)(z_k) = 0\Rightarrow\lim_{k\to+\infty} h(z_k) = h(z_0) = 0 \Rightarrow z_0$ 是 $h(z)$ 的一个孤立奇点。 

 由 5.2.1. 和 1.6. 知道 $h(z)$ 在 $z_0$ 的去心邻域内都不等于零，但由于 $\lim_{k\to +\infty} z_k = z_0$ ，这就代表 $h(z)$ 在 $z_0$ 的去心邻域内有零点，因此 $h(z)\equiv 0\Rightarrow f(z) \equiv g(z)$.

$\blacksquare$

#### 5.3.1. 三角恒等式。

已知 $e^{ix} = \cos x + i\sin x$, 证明 $e^{iz} = \cos z + i\sin z$。

证明：设 $f(z) = e^{iz}, g(z) = \cos z + i\sin z$。 显然 $f,g$ 在复平面上都可导，而且在实轴上都相等，由解析函数的唯一性定理即证。

推论：所有的三角恒等式，都可以推广至复平面，所有不等式作废。

#### 5.3.2. 解析函数没有零因子。

零因子：

$f (z) \not\equiv 0, g(z) \not \equiv 0$， 但 $f(z)g(z) \equiv 0$，则称 $f,g$ 互为零因子。

证明解析函数没有零因子：即若 $f,g$ 在 $D$ 内处处可导， 且 $f(z)g(z) \equiv 0$，$\forall z\in D$， 则 $f(z) \equiv 0$ 或 $g(z) \equiv 0$。

证明如下：

设$f,g$ 在 $D$ 内解析， $f (z) \not\equiv 0, g(z) \not \equiv 0$ 。

这就一定存在 $z_0 \in D$ , s.t. $f(z_0) \neq 0$。

$f$ 在 $z_0$ 解析，由 1.6. 知 $f$ 在 $z_0$ 的邻域内非零，但 $f(z)g(z)$ 在 $z_0$ 的邻域内恒为零 $\Rightarrow g(z)$ 在$z_0$ 的邻域内恒为零。由解析函数的唯一性，$g(z)\equiv 0, z\in D$，这与假设矛盾，证毕！

$\blacksquare$

### 5.4. 留数定理

设 $C$ 包围在复平面上除了有限个点外解析的函数 $f$ 的所有不解析的点。那么，
$$
\oint_C f(z)dz = 2\pi i \sum_{k=1} ^ n c_{-1} ^ {(k)} =  2\pi i \sum_{k=1} ^ n \Res[f(z),z_k]
$$

#### 5.4.1. *留数的计算

$f(z) = \frac{P(z)}{Q(z)}$ ， $P,Q$ 在 $z_0$ 解析且 $P(z_0)\neq 0, Q(z_0) = 0, Q'(z_0) \neq 0$ ，则$c_{-1} = \Res[f(z), z_0] = \frac{P(z_0)}{Q'(z_0)}$。

证明：（杨大伯：略）

笔者的证明如下：

显然 $z_0$ 不是 $P$ 的零点，是 $Q$ 的一阶零点。

设 $Q(z) = (z-z_0)\psi(z)$，$\psi(z)$ 在$z_0$解析且 $\psi(z_0)\neq 0$ 。 因此
$$
C:|z-z_0|=\delta>0, \\
\oint_C f(z)dz = \oint_C \frac{P(z)dz}{(z-z_0)\psi(z)} = \sum_{n=0} ^ {+\infty} \frac{(P(z)/\psi(z))^{(n)}|_{z_0}}{n!}\oint_C (z-z_0)^{n-1}dz=2\pi i\frac{P(z_0)}{\psi(z_0)}
$$
另外， $Q'(z) = \psi(z) + (z-z_0)\psi'(z), Q'(z_0) = \psi(z_0)$，因此 $\Res[f(z), z_0] = \frac{P(z_0)}{Q'(z_0)}$ 。

（5.4.2.，5.4.3. 是笔者认为比较重要，自己加上的内容）

#### 5.4.2. m阶极点的留数



$f(z) = \frac{\psi(z)}{(z-z_0)^m} $ ，$z_0$ 是$f$ 的$m$ 阶极点，那么 $\Res[f(z),z_0] = \frac{\psi^{(m-1)}(z_0)}{(m-1)!}$。

证明：
$$
(z-z_0)^m f(z) = \psi(z) = \sum_{n=0} ^ {+\infty} \frac{\psi^{(n)}(z_0)}{n!}(z-z_0)^n, \\
C: |z-z_0| = \delta > 0 \\
2\pi i \Res[f(z),z_0] = \oint_C f(z)dz = \sum_{n=0} ^ {+\infty} \frac{\psi^{(n)}(z_0)}{n!}\oint_C(z-z_0)^{n-m} dz
$$
$n-m=-1\Rightarrow n=m-1$ 是唯一一个非零项，因此
$$
2\pi i \Res[f(z),z_0] = 2\pi i\frac{\psi^{(m-1)}(z_0)}{(m-1)!} \Rightarrow \Res[f(z),z_0] =\frac{\psi^{(m-1)}(z_0)}{(m-1)!}
$$
推论：

$z_0$ 是 $f$ 的一阶极点，那么 $\Res[f(z),z_0] = \psi(z_0) = \lim_{z\to z_0} (z-z_0)f(z)$

#### 5.4.3. 无穷远点的留数

设 $C$ 包含了 $f$ 在复平面上所有奇点。

回想黎曼球面，把 $C$ 投影在黎曼球面上，那么 $C$ 是一个绕 无穷远点，且 $C$ 内没有其他奇点的反向闭曲线，因此可以定义
$$
\Res[f(z),\infty] = -\frac{1}{2\pi i} \oint _C f(z)dz
$$
立即就有 
$$
\Res[f(z),\infty] + \sum_{k=1} ^ n \Res[f(z),z_k] = 0
$$
设 $C:|z| = R$ 。显然 $|z_k|<R$ 。

设 $z=1/t$，那么 $|t| = 1/R$, $|t_k| = 1/|z_k| > 1/R$， 于是  $|t| = 1/R$  内都没有 $f(1/t)$ 的极点，$t=0$ 除外。
$$
\Res[f(z),\infty] = -\frac{1}{2\pi i} \oint _C f(z)dz = \frac{1}{2\pi i}\oint_{|t| = 1/R} f\left(\frac{1}{t}\right)\cdot \frac{-dt}{t^2} = -\Res\left[\frac{1}{t^2}f\left(\frac{1}{t}\right),0\right]
$$

### ***5.5. (4.7.6.)

$$
J_n = \oint_{|z|= r>1} \frac{dz}{1+z^n}, n\in \Z^+
$$

解一：
$$
J_n = -2\pi i\Res[\frac{1}{1+z^n},\infty] = 2\pi i \Res[\frac{t^{n-2}}{1+t^n},0]
$$
$n=1$ 时，
$$
J_1 = 2\pi i \Res[\frac{1}{t(1+t)}, 0] =  2\pi i \Res[\frac{1}{t}-\frac{1}{1+t}, 0] = 2\pi i
$$
$n\geq 2 $ 时零不是 $J_n$ 的奇点，因此有
$$
J_n = \left\{
\begin{array}{ll}
2\pi i , & n = 1 \\
0, & n \geq 2
\end{array}
\right.
$$
 解二：

$1+z^n = 0\Rightarrow z_k^n =-1$
$$
J_n = 2\pi i\sum_{k=1}^n\Res[\frac{1}{1+z^n},z_k] = \frac{2\pi i }{n}\sum_{k=1}^n\frac{1}{z_k^{n-1}} = -\frac{2\pi i }{n}\sum_{k=1}^n z_k = \left\{
\begin{array}{ll}
2\pi i , & n = 1 \\
0, & n \geq 2
\end{array}
\right.
$$


### ***5.6. 

$$
I_{a,b} = \int_0^{2\pi} \frac{d\theta}{a+b\cos\theta},a>|b|\geq 0.
$$

解：

设 $z = e^{i\theta}$， $\cos\theta = \frac{z+z^{-1}}{2}$，$dz= ie^{i\theta}d\theta = iz d\theta\Rightarrow d\theta = \frac{dz}{iz}$。

When $b=0$，
$$
I_{a,0} = \int_0^{2\pi} \frac{d\theta}{a} = \frac{2\pi}{a}\left(=\frac{2\pi}{\sqrt{a^2-b^2}}\right)
$$
When $b\neq 0$，
$$
C:|z|=1, \\
I_{a,b} = \oint_C \frac{dz}{iz(a+b(z+z^{-1})/2)} = \frac{2}{i} \oint_C \frac{dz}{bz^2+2az+b}
$$

$$
bz^2+2az+b=0\Rightarrow z = \frac{-2a\pm\sqrt{4a^2-4b^2}}{2b} = -\frac{a}{b}\pm\sqrt{\frac{a^2}{b^2}-1} \in \R, \\
I_{a,b} = 4\pi \Res[\frac{1}{bz^2+2az+b},\frac{-a+\sqrt{a^2-b^2}}{b}] = \left.\frac{4\pi}{2bz+2a}\right|_{z=\frac{-a+\sqrt{a^2-b^2}}{b}} = \frac{2\pi}{-a+\sqrt{a^2-b^2}+a} = \frac{2\pi}{\sqrt{a^2-b^2}}
$$

综上，
$$
I_{a,b} = \frac{2\pi}{\sqrt{a^2-b^2}}
$$

### ***5.7.

$$
I_{A,B} = \int_0^{2\pi} \frac{d\theta}{A^2\cos^2\theta+B^2\sin^2\theta}=\int_0^{2\pi}\frac{2d\theta}{A^2(1+\cos 2\theta) + B^2(1-\cos 2\theta)} = \int_0^{2\pi}\frac{d(2\theta)}{(A^2+B^2)+(A^2-B^2)\cos 2\theta} \\
=\int_0^{4\pi}\frac{d\phi}{(A^2+B^2)+(A^2-B^2)\cos 2\phi} = \frac{4\pi}{\sqrt{(A^2+B^2)^2-(A^2-B^2)^2}} = \frac{4\pi}{\sqrt{4A^2B^2}}=\frac{2\pi}{AB} 
$$

### ***5.8.

$$
I_n = \oint_{|z|=1}\frac{1-\cos 5z^6}{z^n}dz = \sum_{k=1} ^ {+\infty} \frac{(-1)^{k-1}5^{2k}}{(2k)!}\oint_{|z|=1} z^{12k-n}dz
$$

非零项$k$ 一定满足 $ k=(n-1)/12$, $n\geq 13$ 且 $n \equiv 1(\mod 12)$

$$
I_n =  \left\{
\begin{array}{ll}
2\pi i\frac{(-1)^{(n-13)/12}5^{(n-1)/6}}{((n-1)/6)!}, & n\geq 13 \land n \equiv 1(\mod 12) \\
0, & \text{otherwise}
\end{array}
\right.
$$

### ***5.9.

$$
I_n = \int_0^{+\infty} \frac{dx}{1+x^{2n}}
$$

被积函数是偶函数，因此
$$
I_n = \frac{1}{2} \int_{-\infty} ^{+\infty} \frac{dx}{1+x^{2n}} = \lim_{R\to+\infty}\frac{1}{2}\int_{-R}^R \frac{dx}{1+x^{2n}}
$$
作 $C_R=\{z:z=Re^{i\theta},0\leq \theta \leq \pi\}, \Gamma_R=C_R\cup[-R,R].$
$$
\left|\int_{C_R} \frac{dz}{1+z^{2n}}\right| \leq \int_{C_R} \frac{|dz|}{|1+z^{2n}|} \leq \int_{C_R} \frac{|dz|}{|z^{2n}|-1} = \frac{\pi R}{R^{2n}-1} =\frac{\pi}{R^{2n-1}-R^{-1}}\to0, R\to+\infty
$$
因此
$$
\oint_{\Gamma_R}\frac{dz}{1+z^{2n}} = \int_{-R}^R \frac{dx}{1+x^{2n}} + \int_{C_R}\frac{dz}{1+z^{2n}}\to \int_{-\infty} ^ {+\infty} \frac{dx}{1+x^{2n}} =2I_n, R\to+\infty
$$
而第一个半圆的路径积分的被积函数的奇点，是  $1+z^{2n}=0$ 在上半平面的零点，共有 $n$ 个。所以，
$$
I_n = \lim_{R\to+\infty}\frac{1}{2}\oint_{\Gamma_R}\frac{dz}{1+z^{2n}} = \pi i \sum_{k=1}^n \Res[\frac{1}{1+z^{2n}}, z_k] = \pi i\sum_{k=1}^n\frac{1}{2nz_k^{2n-1}} =-\frac{\pi i}{2n}\sum_{k=1}^n z_k 
$$
$z_k^{2n}=-1\Rightarrow z_k=e^{(2k-1)\pi i/(2n)}=e^{-\pi i/(2n)}(e^{\pi i/n})^k$
$$
I_n = -\frac{\pi i}{2n}e^{-\pi i/(2n)}\sum_{k=1}^n (e^{\pi i/n})^k=-\frac{\pi i}{2n}e^{-\pi i/(2n)}\frac{e^{\pi i/n}(1+1)}{1-e^{\pi i/n}} = \frac{\pi}{2n}\cdot \frac{2ie^{\pi i/(2n)}}{e^{\pi i/n}-1} =\frac{\pi}{2n}\cdot \left(\frac{e^{\pi i/(2n)}-e^{-\pi i/(2n)}}{2i}\right)^{-1} = \frac{\frac{\pi}{2n}}{\sin\frac{\pi}{2n}}.
$$
推广：
$$
I_{r,n} = \int_0^{+\infty} \frac{dx}{r^{2n}+x^{2n}}=\frac{r}{r^{2n}}\int_0^{+\infty} \frac{d(x/r)}{1+(x/r)^{2n}} = \frac{1}{r^{2n-1}}\cdot \frac{\frac{\pi}{2n}}{\sin\frac{\pi}{2n}}
$$

### ***5.10. 

$$
I_{a,b,k} = \int_0 ^ {+\infty} \frac{x^3 \sin kx dx}{(x^2+a^2)(x^2+b^2)}
$$

解：

被积函数是偶函数，因此
$$
I_{a,b,k} = \frac{1}{2} \int_{-\infty} ^ {+\infty} \frac{x^3 \sin kx dx}{(x^2+a^2)(x^2+b^2)}
$$
记
$$
J_{a,b,k} = \int_{-\infty} ^ {+\infty} \frac{x^3 e^{ikx} dx}{(x^2+a^2)(x^2+b^2)} = \int_{-\infty} ^ {+\infty} \frac{x^3 \cos kx dx}{(x^2+a^2)(x^2+b^2)}+i\int_{-\infty} ^ {+\infty} \frac{x^3 \sin kx dx}{(x^2+a^2)(x^2+b^2)}
$$
而 $\frac{x^3 \cos kx}{(x^2+a^2)(x^2+b^2)}$ 是奇函数，积分值为零，因此 $J_{a,b,k} = 2i I_{a,b,k}$。

另一方面，作 $C_R=\{z:z=Re^{i\theta},0\leq \theta \leq \pi\}, \Gamma_R=C_R\cup[-R,R].$
$$
(!!): \frac{2}{\pi}x \leq\sin x,x\in[0,\pi/2]\\
\left|\int_{C_R}\frac{z^3e^{ikz}dz}{(z^2+a^2)(z^2+b^2)}\right| \leq \int_{C_R}\frac{R^3e^{-ky}|dz|}{|z^2+a^2||z^2+b^2|} < \int_{C_R} \frac{R^3e^{-kR\sin\theta}Rd\theta}{R^4} \\
=\int_{0}^{\pi}e^{-kR\sin\theta}d\theta = 2\int_0^{\pi/2} e^{-kR\sin\theta}d\theta <2\int_0^{\pi/2}e^{-2kR\theta/\pi}d\theta = \frac{2\pi(1-e^{-\frac{kR}{2}})}{kR}\to 0, R\to +\infty
$$
因此
$$
\oint_{\Gamma_R} \frac{z^3 e^{ikz}dz}{(z^2+a^2)(z^2+b^2)} = \int_{-R} ^ {R} \frac{x^3 e^{ikx} dx}{(x^2+a^2)(x^2+b^2)} +\int_{C_R}\frac{z^3e^{ikz}dz}{(z^2+a^2)(z^2+b^2)} \to\int_{-\infty} ^ {+\infty} \frac{x^3 e^{ikx} dx}{(x^2+a^2)(x^2+b^2)}=J_{a,b,k},R\to + \infty
$$
而在上半平面， $ai,bi$ 是被积函数仅有的两个奇点。与此同时，
$$
\frac{z^3 e^{ikz}}{[(z^2+a^2)(z^2+b^2)]'} = \frac{z^3 e^{ikz}}{2z(2z^2+a^2+b^2)}=\frac{z^2 e^{ikz}}{2(2z^2+a^2+b^2)}
$$
所以
$$
J_{a,b,k} = \lim_{R\to+\infty} \oint_{\Gamma_R} \frac{z^3 e^{ikz}dz}{(z^2+a^2)(z^2+b^2)} 
=2\pi i \left(\Res[\frac{z^3 e^{ikz}}{(z^2+a^2)(z^2+b^2)},ai]+\Res[\frac{z^3 e^{ikz}}{(z^2+a^2)(z^2+b^2)},bi]\right) \\
=2\pi i \left(\frac{-a^2 e^{-ak}}{2(-a^2+b^2)}+\frac{-b^2 e^{-bk}}{2(a^2-b^2)}\right)
= \frac{\pi i(a^2e^{-ak}-b^2e^{-bk})}{a^2-b^2},I_{a,b,k} = \frac{J_{a,b,k}}{2i} = \frac{\pi (a^2e^{-ak}-b^2e^{-bk})}{2(a^2-b^2)}
$$
推广：
$$
I_{a,b,k} = \int_0 ^ {+\infty} \frac{x \sin kx dx}{(x^2+a^2)(x^2+b^2)}= \frac{\pi (e^{-ak}-e^{-bk})}{2(a^2-b^2)}
$$


## 6. 共形映射

### 6.0. 定义

（笔者上课的学期由于疫情，杨大伯就跳过了定义了，6.0. 是笔者自己加上的补充内容）

设复平面上有一光滑曲线 $C: z=z(t), t\in\R$。 下面讨论 $z'(t)$ 的几何意义、

$\arg z'(t_0)$ 是 $C$ 在 $z_0 = z(t_0)$ 处的切线于正实轴的有向夹角。

-----

解析函数的导数--几何意义：

$w=f(z)$ 在 $D$ 内解析。

设 $z_0\in D$, $f'(z_0)\neq 0$ 。

如果存在光滑曲线 $C:z=z(t), t\in[\alpha,\beta],z_0\in C,$

$w=f(z)=(f\circ z)(t), w'(z_0) = (f'\circ z)(t_0)\cdot z'(t_0)$.

$\Rightarrow \arg(w'(z_0)) - \arg(z'(t_0)) = \arg((f'\circ z)(t_0)) = \arg(f'(z_0))$。

 因此$f$ 在$z_0$的转动角大小与 $C$ 的形状、方向无关。

那么，对于两条曲线 $C_1,C_2$,
$$
\arg w_2'(t_0) -\arg w_1'(t_0) = \arg z_2'(t_0) - \arg z_1'(t_0)
$$
因此对于两条光滑曲线，其交点及其邻域在$D$内，则两条曲线在原像切线的夹角，与像的切线的夹角保持一致，是为解析函数的**保角性**。

对于光滑曲线$C$ 上的一点 $z_0$，设$z\in C$， 那么 $f(z_0), f(z)\in f(C)$。

令 $z-z_0 = re^{i\phi}, f(z)-f(z_0)=\rho e^{i\psi}$，$z\to z_0$，可以得到$z_0$ 关于 $C$ 的切向量经过映射后的伸缩率：
$$
\frac{\rho}{r}=\lim_{z\to z_0} \frac{|f(z)-f(z_0)|}{|z-z_0|} = |f'(z_0)|
$$
同样与曲线无关。

因此解析函数在定义域内某个点的这样的伸缩率与转动角，不因该点依附在哪条曲线而有所不同。

可以定义**共形映射**为：

在复平面上，如果 $f$ 在 $z_0$ 的邻域内是单射函数，且在 $z_0$ 具有保角性，和伸缩率的不变性，则 $f$ 在 $z_0$ 共形。$f$ 在 $D$ 内每个点都共形，则 $f$ 是 $D$ 内的共形映射。

定理：

对于任何在$z_0$共形的函数，都存在 $c$, $(f\circ z)'(t_0) = c\cdot z'(t_0)$。

显然解析函数都是共形映射，伸缩率为 $|f'(z_0)|$， 转动角为 $\arg f'(z_0)$。

定理：

分式线性映射具有保圆性。

LFT maps lines and circles into lines and circles.

1. $w=1/z$ ($c\neq 0$)

Let $z = x+iy$, then
$$
w =\frac{1}{z} = \frac{x-iy}{x^2+y^2} = u + iv\\
x^2+y^2+Dx+Ey+F=0\Leftrightarrow 1 + \frac{Dx}{x^2+y^2} + \frac{Ey}{x^2+y^2} + \frac{F}{x^2+y^2} = 1+Du-Ev + F(u^2+v^2) = 0
$$

2. $w=(az+b)/d$ ($c=0$) (translation+rotation+scaling) must preserve lines and circles.  $\blacksquare$

初等函数映射：

幂级数：角形域$\to$ 角形域

指数函数：带型域 $\to$ 角形域

儒可夫斯基函数(Joukowsky) $w = z+1/z$。（圆盘$\to$ 飞机机翼）

### 6.1. 分式线性映射

分子、分母的次数不超过一，总的次数不超过一的复映射，是为分式线性映射。
$$
w=\frac{az+b}{cz+d}\Rightarrow \frac{dw}{dz} = \frac{a(cz+d)-c(az+b)}{(cz+d)^2} =\frac{ad-bc}{(cz+d)^2}, ad-bc\neq 0
$$

#### ***6.1.1.

单位圆盘$|z|<1$到单位圆盘$|w|<1$的分式线性映射，都具有下列形式：
$$
w=e^{i\theta}\frac{z-z_1}{1-\bar{z_1}z},\theta\in[0,2\pi), |z_1|<1.
$$
这是因为要把圆盘内某一个点 $z_1$，映到原点，它的反演点就要映到无穷远点了。

证明不变式 
$$
\frac{|dz|}{1-|z|^2}=\frac{|dw|}{1-|w|^2}
$$
证明如下：

证明原命题等价于证明
$$
\left|\frac{dw}{dz}\right| = \frac{1-|w|^2}{1-|z|^2},
$$
而
$$
\left|\frac{dw}{dz}\right| = |e^{i\theta}|\left|\frac{(1-\bar{z_1}z)+(z-z_1)\bar{z_1}}{(1-\bar{z_1}z)^2}\right| = \frac{1-|z_1|^2}{|1-\bar{z_1}z|^2}
$$
于是只需要证明
$$
\frac{1-|w|^2}{1-|z|^2}=\frac{1-|z_1|^2}{|1-\bar{z_1}z|^2}
$$
而
$$
1-|w|^2=1-w\bar{w}=1-\frac{z-z_1}{1-\bar{z_1}z}\cdot \frac{\overline{z-z_1}}{\overline{1-\bar{z_1}z}}=1-\frac{(z-z_1)(\bar{z}-\bar{z_1})}{|1-\bar{z_1}z|^2}=1-\frac{z\bar{z}-z\bar{z_1}-z_1\bar{z}+z_1\bar{z_1}}{|1-\bar{z_1}z|^2} \\
=\frac{1-z_1\bar{z}-\bar{z_1}z+|z_1z|^2-|z|^2+z\bar{z_1}+z_1\bar{z}-|z_1|^2}{|1-\bar{z_1}z|^2} = \frac{(1-|z|^2)(1-|z_1|^2)}{|1-\bar{z_1}z|^2}
$$
$\blacksquare$

给出圆盘 $|z-z_0|\leq r$ 到 $|w-w_0|\leq R$ 的线性映射，其中 $z_1\to w_0$。

对单位圆盘作置换 $z'=(z-z_0)/r, w'=(w-w_0)/R$.
$$
\frac{w-w_0}{R} = e^{i\theta} \frac{\frac{z-z_0}{r}-\frac{z_1-z_0}{r}}{1-\frac{\bar{z_1}-\bar{z_0}}{r}\cdot\frac{z-z_0}{r}} = re^{i\theta}\frac{z-z_1}{r^2-(\bar{z_1}-\bar{z_0})(z-z_0)}\Rightarrow w=w_0+rRe^{i\theta}\frac{z-z_1}{r^2-(\bar{z_1}-\bar{z_0})(z-z_0)},\\
\theta\in[0,2\pi),|z_1-z_0|<r
$$
准不变式：
$$
\frac{|d(\frac{z-z_0}{r})|}{1-|\frac{z-z_0}{r}|^2}=\frac{|d(\frac{w-w_0}{R})|}{1-|\frac{w-w_0}{R}|^2}
\Leftrightarrow \frac{r|dz|}{r^2-|z-z_0|^2}=\frac{R|dw|}{R^2-|w-w_0|^2}
$$

#### 6.1.2. 上半平面到单位圆盘的分式线性映射：

$$
w=e^{i\theta}\frac{z-z_1}{z-\bar{z_1}}, \Im(z_1)>0, \theta\in[0,2\pi)
$$

最简形式： $w=\frac{z-i}{z+i}$.

#### *6.1.3. 上半平面到上半平面的分式线性映射

$$
a,b,c,d\in\R, w=\frac{az+b}{cz+d}
$$

是上半平面到上半平面的分式线性映射，当且仅当 $ad-bc>0$。

证明：

令 $z=x+iy, w=u+iv$，
$$
w= \frac{a(x+iy)+b}{c(x+iy)+d} = \frac{(ax+b)+iay}{(cx+d)+icy} = \frac{[(ax+b)+i(ay)][(cx+d)-icy]}{(cx+d)^2+(cy)^2} \\
= \frac{((ax+b)(cx+d)+acy^2)+i(ay(cx+d)-cy(ax+b))}{(cx+d)^2+(cy)^2},\\
v= \frac{y(ad-bc)}{(cx+d)^2+(cy)^2}, \\
vy = \frac{y^2(ad-bc)}{(cx+d)^2+(cy)^2} \geq 0 \Leftrightarrow ad-bc>0
$$
$\blacksquare$

#### ***6.1.4. 

求单值解析映射 $f:D_1\to D_2$。

$D_1=\{z:|z-A|>A,|z-B|<B\},D_2:|w|<1$。

解：

1) 把原像映到一竖长条(原点映到无穷远点)，$z=2A$ 映到原点：

$$
z_1=\frac{z-2A}{z}
$$

2) 把竖长条旋转 $\pi/2$ ，变成一横长条：

$$
z_2=iz_1
$$

3) 把横长条拉伸，把宽度由 $\frac{B-A}{B}$ 调整为 $\pi$。
$$
z_3=\frac{\pi B}{B-A}z_2
$$

4) 把横长条映到整个上半平面：
$$
z_4 = e ^ {z_3}
$$
5) 把上半平面映到单位圆：

$$
w = \frac{z_4-i}{z_4+i}
$$

综上，
$$
w = \frac{z_4-i}{z_4+i} = \frac{e^{z_3}-i}{e^{z_3}+i}
= \frac{e^{\frac{\pi B}{B-A}z_2}-i}{e^{\frac{\pi B}{B-A}z_2}+i} 
= \frac{e^{\frac{i\pi B}{B-A}z_1}-i}{e^{\frac{i\pi B}{B-A}z_1}+i} 
= \frac{e^{\frac{i\pi B(z-2A)}{(B-A)z}}-i}{e^{\frac{i\pi B(z-2A)}{(B-A)z}}+i}
$$

### 6.2. 黎曼定理

任意的在复平面内部，且不等于复平面的单连通域与单位圆盘同胚。

证明：略（笔者水平暂未能独自写证明）。
