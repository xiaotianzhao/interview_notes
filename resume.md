简历相关：

NER：

1. **基于规则的方法**

   ​	使用正则匹配找价格，"\d+.\d+元"。基于规则的实体抽取方式，优点：简单，快速，缺点：适用性差，维护成本后期比较高。

2. **基于模型的方法**

   ​	基于模型的角度看，NER实际上是一个序列标注问题。常见的序列标注模型有HMM，CRF，RNN等。

分词：

1. 基于字符串匹配。正向最大匹配，反向最大匹配。
2. 序列标注模型。HMM，CRF，RNN



AutoEncoder：

1. 原始的AutoEncoder

2. 去噪自编码器（DAE）

   $L(s, g(f(\hat{x})))$

3. 稀疏自编码器（SAE）

   $L(x, g(f(x))) + \Omega(h) = L(x, g(f(x))) + \lambda\sum_{i}\mid h_i\mid$

4. 收缩自编码器(惩罚倒数作为正则)

   $L(x,g(f(x))) + \lambda\sum_{i}\mid\mid f'(h_i(x))\mid\mid_{2}$

   CAE训练为抵抗输入扰动，鼓励将输入点领域映射到输出点更小的邻域。



CNN:

稀疏交互：局部视野，但是在高一些的层次，其实接收域是很大的

参数共享：一个模型在多个函数中使用相同的参数。

等变表示：参数共享的特殊形式使得神经网络层有平移等变性。



平移不变性：池化能够帮助输入的表示近似不变。当我们对输入进行少量的平移，经过池化后的大多数输出并不会变化。

![CNN文本分类](.\image\CNN文本分类.png)

- $n*k*channel$ n*k表示n个单词，每个单词k个维度

- CNN-rand:所有的word vector 都随机初始化，然后在训练过程中当做参数优化

  CNN-static:使用训练好的word vector作为结果，进行训练

  CNN-non-static:所有的word vector初始化为训练好的word vector的结果，在训练过程中进行fine tuned

  CNN-multichannel:使用CNN-static，CNN-non-static的混合版本，即两种类型的输入



LSTM原理：

$f_t = \sigma(W_f.[h_{t-1},x_t] + b_f)$

$f_i = \sigma(W_i[h_{t-1},x_t] + b_i)$

$\tilde{c} = tanh(W_c[h_{t-1},x_t]+b_c)$

$c_t = f_t \dot{} c_{t-1} + f_i\dot{}\tilde{c}$

$o_t = \sigma(W_o[h_{t-1},x_t] + b_o)$

$h_t = o_t\dot{}tanh(c_t)$

![LSTM原理图](.\image\LSTM原理图.png)



GRU原理：

$r_t = \sigma(W_r[h_{t-1},x_t]+b_r)$

$u_t=\sigma(W_u[h_{t-1},x_t]+b_z)$

$n_t = tanh(W_{in}x_t + b_{in}+r*(W_{hn}h_{t-1} + b_{hn}))$

$h_t = (1-u_t)*n_t + u_t * h_{t-1}$



Seq2Seq:



最长公共子串、编辑距离：



CRF是判别式模型，HMM是生成式模型

TF-IDF ：TF = 单词出现的次数/ 文档中单词出现的次数

​		IDF = log 文档总数 / 包含单词的文档数目 + 1

TEXTRANK:
