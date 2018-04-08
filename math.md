$E(\lambda X) = \lambda E(X)$

证明：$E(\lambda X) = \frac{1}{N}\sum_i(\lambda x_i - \lambda \bar{x}) = \frac{1}{N}\sum_{i}\lambda (x_i - \bar{x}) = \lambda E(X)$

$E(X+Y) = E(X) + E(Y)$



$var(X) = E\{[X - E(X)]^2\} = \frac{1}{N} \sum_{i} (x_i - \bar x)^2 = \frac{1}{N} \sum_i x_i^2 - \frac{1}{N} \sum_i 2*x_i*\bar{x} + \frac{1}{N} \sum_i{\bar{x}^2} = E(X^2) - 2 * E^2(X) + E(X) = E(X^2) - E^2(X)$

无条件成立：

$var(c) = 0$

$var(X + c) = \sum_i(x_i + c - \bar {x} - c)^2 = \sum_i(x_i - \bar{x})^2 = var(X)$

$var(kX) = k^2 var(X)$

如果$X$和$Y$独立，那么$var(X + Y) = var(X) + var(Y)$



切比雪夫不等式：估计随机变量的值落在期望附近的概率

$P\{\mid X - u \mid \lt \varepsilon \} \ge 1 - \frac{\sigma^2}{\varepsilon^2}$

$P\{\mid X - u \mid \le \varepsilon\} = 1 - P\{\mid X - u\mid \ge \varepsilon\}$

$ P\{\mid X - u\mid \ge \varepsilon\} = \int_{\mid X - u\mid \ge \varepsilon} f(x)dx  \le \int_{\mid X - u\mid \ge \varepsilon} \frac{\mid X - u\mid ^2}{\varepsilon ^2}f(x)dx = \frac{1}{\varepsilon^2} \int_{\mid X - u\mid \ge \varepsilon} \mid X - u\mid ^2f(x)dx \le \frac{1}{\varepsilon^2} \int_{-\infty}^{+\infty} \mid X - u \mid^2 f(x)dx = \frac{\sigma^2}{\varepsilon^2} $

$P\{\mid X - u\mid ^2 \lt \varepsilon\} = 1 - \frac{\sigma^2}{\varepsilon^2}$



大数定律：

频率的极限是概率。



中心极限定理：



样本的统计量：

样本是独立同分布的。

假设样本的k阶矩和总体的k阶矩是相等的，可以估计出总体的参数。

样本的k阶矩可以通过样本算出，总体的k阶矩是参数$\theta$的方程，联立样本数目个方程，解方程可以得到相应的参数。



给定样本的方差为什么是除以1/(n - 1)?

当有总体的均值$\mu$ 的时候，计算方差$E[(x_i - \mu)^2] = \sigma^2$ ,$E[\frac{1}{n}\sum_i^n(x_i - u)^2] = \sigma^2$

当没有总体的均值$\mu$的时候， 我们一般会使用样本的均值$\bar{x}$来代替$\mu$ 。

$\frac{1}{n} \sum_i^n(x_i - \bar{x})^2 = \frac{1}{n} \sum_i^n(x_i - \mu  + \mu - \bar{x})^2 = \frac{1}{n} \sum_i^n (x_i - \mu)^2 - 2*(\bar{x} - \mu)*(\mu - \bar{x}) + (\mu - \bar{x})^2 \le var(X)$



矩阵：

$A_{m*n} = U_{m*m} \Sigma_{m*n}V_{n*n}$

SVD： 

矩阵行列式的求解：

$\mid A \mid = \sum_i^n a_{ij}*(-1)^{i+j}M_{ij}$ ,$M_{ij}$ 是代数余子式

伴随矩阵：

$A^* = (A_{ij})_{m*n}$ ，$A_{ij} = (-1)^{i + j} M_{ij}$

$A*A^* = \mid A \mid*I $ 所以$A^{-1} = \frac{1}{\mid A \mid} A^*$



范德蒙行列式： 当$x_i \ne x_j , 1 \le i \le j \le n$

**n个数据最多用n-1阶函数可以完全拟合**。插值



矩阵乘法：

$c_{ij} = \sum_{k = 1}^na_{ik}b_{kj} $



矩阵乘法的快速算法，分治思想

矩阵乘积顺序？DP



矩阵的秩

正交矩阵：

$A$是正交阵的充要条件：$A$的列，行向量都是单位向量，且两两正交。

$A$是正交阵， $x$为向量， 则称$Ax$为正交变换。 正交变换不改变向量长度。

$A , B$都是n阶正交阵，那么$A*B$也是正交阵？

**正交阵和对称阵，能够通过何种操作获得一定意义下的联系**？



如果$\lambda$是方阵$A$的特征值，则$\lambda^n$是$A^n$的特征值。当A可逆的时候，$\lambda ^{-1}$是$A^{-1}$的特征值。

不同特征值对应的特征向量是线性无关的。

**实对称阵的特征值是实数，对应的特征向量是实向量，且正交**

设$A$为n阶对称阵，则必有正交阵P，使得，$P^{-1}AP = P^TAP=\Lambda$



白化/漂白？？？

对于任意m*n的矩阵$A$ ,证明$A^TA$ 一定是半正定方阵。



- 一个矩阵是正定阵
- $A$ 的特征值都是正的。
- $A$的顺序主子式大于零

这三个命题是等价的。



**向量的求导：**



**QR分解**

对于m*n的列满秩矩阵A，必有：$A_{mn} = Q_{mn}.R_{nn}$

QR矩阵可以做分解。



凸优化：

凸集：凸函数的上方区域称为凸集。



**如何判断一个函数是不是凸函数**？ 

如果一个函数的二阶导存在，且$f''(x) \gt 0$ 则该函数被称为凸函数，充要条件。



仿射集：

通过集合C中两个不同的点的直线仍在集合C内，则称集合C是仿射集。

凸集：

集合C内任意两点间的线段均在集合C内，则称集合C为凸集。

$任意x_1,x_2 \in C,任意\theta \in [0,1] ,\theta x_1 + (1 - \theta)x_2 \in C$ 则C被称为凸集

凸包：

集合C的所有点的凸组合形成的集合，叫做集合C的凸包。集合C的凸包是能够包含C的最小凸集。

超平面与半空间：

超平面 $\{x \mid a^Tx = b\}$ ，半空间$\{x|a^T x \le b\}$ $\{x| a^Tx \ge b\}$

多面体是有限个半空间和超平面的交集。

保持凸性的运算：集合交运算，仿射变换，透视变换，投射变换。



分割超平面：设C和D是两个不相交的凸集，则存在超平面P，P可以将C和D进行分离。

支撑超平面：支撑超平面不一定唯一。







