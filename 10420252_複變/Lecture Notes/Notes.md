# 复变函数引论学习资料

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

### 0.3. 复数的基本概念

复数域：
$$
\mathbb{C} = \{(x + iy):x,y\in\mathbb{R}, i = \sqrt{-1}\}
$$
复数运算：
$$
z = x + iy \\
z_1 \pm z_2 = (x_1 \pm x_2) + i(y_1 \pm y_2) \\
\bar{z} = x - iy, |z| = \sqrt{x^2 +y^2} \\
z_1z_2 = (x_1x_2 - y_1y_2) + i(x_1y_2 + x_2 y_1) \\
\Rightarrow |z|^2 = z\bar{z}\\
\frac{z_1}{z_2} = \frac{z_1\bar{z_2}}{|z_2|^2} \\
$$
极式表示：
$$
z = re^{i\theta}, r = |z|, \theta = arg(z) = \atan2(y,x) \in [0,2\pi) \\
e^{i\theta} = \cos\theta + i\sin \theta \\
\Rightarrow \cos(n\theta) + i\sin(n\theta) = (cos\theta + i\sin \theta) ^ n, n \in \mathbb{Z}.
$$

***

$$
\oint_{|z| = \epsilon > 0} \frac{dz}{z} = \int_0^{2\pi} \frac{d(\epsilon e^{i\theta})}{\epsilon e^{i\theta}} = \int_0^{2\pi}\frac{i\epsilon e^{i\theta}d\theta}{\epsilon e^{i\theta}} = 2\pi i
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

#### 1.5.

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

