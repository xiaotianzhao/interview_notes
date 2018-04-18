Gamma函数

$\Gamma(x) = \int_0^{\infty} t^{x-1}e^{-t}dt$ 

$\Gamma(x + 1) =x\Gamma(x) $ （简单理解，因为Gamma函数是在实数范围上面的阶乘拓展）

$\Gamma(x) = (x - 1)!$



将数列的通项公式从整数集合延拓到实数集合，比如，通项公式$n^2$ 。将整数的阶乘画到图像上面的确可以画出一条平滑的曲线，那么如何去表示这条曲线呢？

无穷乘积来表示：$\frac{1*2*3*...*m}{(1+ n)*(2+n)*...*(m-1 +n)}(m+\frac{n}{2})^{n-1} \to n!$ 当$m$ 趋向于正无穷的时候

另一种无穷乘积的方式$\lim_{m \to \infty} \frac{1*2*...*m}{(1+n)*(2+n)*...*(m+n)} (m+1)^n = n!$

$\Gamma(x) = \int_{0}^{1} (-log\ t)^{x -1}dt = \int_{0}^{\infty} t^{x-1}e^{-t} dt$



Gamma分布

$\int_{0}^{\infty} \frac{x^{\alpha-1}e^{-x}}{\Gamma(\alpha)} dx = 1$ 

令$x=\beta t$ ,$Gamma(t \mid \alpha,\beta) = \frac{\beta^\alpha t^{\alpha-1}e^{-\beta t}}{\Gamma(\alpha)}$  ,$\alpha$是形状参数，决定了分布曲线的形状，$\beta$是决定曲线有多陡的。

- 指数分布和$X^2$ 分布都是特殊的Gamma分布。
- 使用Gamma分布作为先验分布很强大。在贝叶斯统计分析中被广泛用于其他分布的先验
- 指数分布，泊松分布，正态分布，对数正态分布和Gamma分布是共轭关系

Beta函数

$B(m,n) = \int_{0}^{1} x^{m-1}(1-x)^{n-1} dx = \frac{\Gamma(m)\Gamma(n)}{\Gamma(m + n)}$ 



Beta分布和Dirichlet分布

Beta分布的导出：

1. $X_1,X_2,...,X_n $从$Uniform(0,1)$ 里面独立采样得到
2. 把这n个随机变量排序后得到顺序统计量$X_{(1)},X_{(2)},...,X_{(n)}$
3. $X_{k}$ 的分布是Beta分布

   $f(x) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} $

