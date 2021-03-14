## Classification

> * 从一堆数据中提取出信息，output是这对数据是属于哪一类

### 使用领域

* 金融领域信誉得分
  * 根据一个人的收入，存款，年龄，等等，输出的是银行到底要不要借钱给这个人。
* 手写数字识别
  * 根据输入的数字，输出实际的值。
* 医疗领域
  * 判断是属于哪一种病，是患病了还是没患。

### Pokemon的种系划分

![](https://img.imgdb.cn/item/604d75ae5aedab222cb76243.jpg)

![](https://img.imgdb.cn/item/604d75df5aedab222cb7776b.jpg)

> * 对于一个Pokemon，有上述的这些数据值，但是我们不知道这个Pokemon是属于呢一个类，那么我们是否可以直接使用这些数据得到这个Pokemon的类别呢？？？？

#### 为什么不可以使用Regression的方法套用进Classification中?

> * 这是classification要找到的是一堆离散的值，也就是说$\hat y$实际上是类的名称比如$\{-1, 1\}$这样的二分类。
> * 但是如果完全照搬，导致regression得到的曲线会严重受到不同样本点的影响，而$\hat y$又无法实时给出相应的指导（值只取$\{-1, 1\}$）
> * 而且，对于那些偏离分界点较大的值，使用regression对得到非常大的预测值，而两个样本之间的距离也仅仅只有2的距离，如果距离远大于2，那么将很难判断到底属于哪一类会更好
> * 所有使用regression来用作classification是非常不明智的做法。

![](https://img.imgdb.cn/item/604d7a0a5aedab222cb94349.jpg)

#### 基本思路

> * 在预测函数$f$里面内嵌入一个函数$g$
>
>   * 如果函数$g$大于0，那么我们就让结果输出class 1
>   * 如果函数$g$小于0，那么我们就让结果输出class 2
>
> * $Loss\ Function$
>
>   * $$
>     L(f) = \sum_n\delta(f(x^n) \neq \hat y^n)
>     $$
>
>   * 当不相等的时候，我们就记录者一次错误
>   * 累计的总数为这个$Loss\ Function$的实际的值
>   * 训练模型的过程就是为了让这个值原来越小。

![](https://img.imgdb.cn/item/604d7a1d5aedab222cb94b70.jpg)

#### 从Tow Boxes 引入到 Two Classes

> * 下述公式表示抽出来一个蓝球，这个蓝球是从盒子一出来的概率
>   * 也就是蓝球来自盒子一的概率去除以来自盒子一和盒子二的和。

![](https://img.imgdb.cn/item/604d7c2c5aedab222cba2fa6.jpg)

$P(A|B)$表示在B发生的前提下A发生的概率。

> * 对于二分类的问题：
>
>   * formulation：
>
>   * $$
>     P(C_1|x) = \frac{P(x|C_1)P(C_1)}{P(x|C_1)P(C_1) + P(x|C_1)P(C_2)}
>     $$
>
>   * $P(C_1) = P(C_1|C)$： 表示在总class 里是$C_1$的概率
>
>   * $P(x|C_1)$ 表示在$C_1$里面拿到$x$的概率
>
>   * 而当拿到了上述的概率之后就可以自己创造一个类
>
>     * $P(x)=P(x|C_1)P(C_1) + P(x| C_2)P(C_2)$
>
> * 对于多元分类而言无非是增加了这个分母的项数
>
>   * $P(C_k|x)=\frac{P(x|C_k)P(C_k)}{\sum_ {i=0}^nP(x|C_i)P(C_i)}$
>   * $P(x)=\sum_{i=0}^nP(x|C_i)$

![](https://img.imgdb.cn/item/604d7e135aedab222cbb3dcb.jpg)

##### Gaussian Distribution(正态分布)

![](https://img.imgdb.cn/item/604d83745aedab222cbf3732.jpg)

> * Convariance Matrix 协方差矩阵
> * mean 均值
> * 如果说我们知道$\mu 和 \Sigma$ 那么我们就知道这个样本点$x$在这个核里面的概率

![](https://img.imgdb.cn/item/604db7be5aedab222ce6aa6e.jpg)

> * 如果给我们一个Gaussian Distribution的$\mu\  \Sigma$
> * 我们就可以使用这个function得到这些点的几率

![](https://img.imgdb.cn/item/604db9675aedab222ce80c48.jpg)

> * 那么我们想要这个functuon可以把所有的sample都找出来
>
> * 上述的Gaussian就可以帮助我们优化lossfunction
>
> * $$
>   L(\mu, \Sigma) = f_{\mu, \Sigma}(x^1)f_{\mu, \Sigma}(x^2)\dots f_{\mu, \Sigma}(x^{79}) \\
>   f_{\mu, \Sigma}(x) = \frac{1}{(2\pi)^{\frac{D}{2}}}\frac{1}{|\Sigma|^{\frac{1}{2}}}exp\{-\frac{1}{2}(x-\mu)^T\Sigma ^{-1}(x-\mu)\}
>   $$
>
> * 找到使得这个Gaussian最大的$\mu, \Sigma$
>
>   * 使用微分求解
>   * 直接$\mu$取均值
>   * $\Sigma = \frac{1}{n}\sum_{i=1}^n(x^i - \mu)(x^i - \mu)^T$

> * $P(x|C_1)$表示从$C_1$的高斯分布中取到这个点的概率。
> * $P(C_1)$表示总样本中取到$C_1$的概率

![](https://img.imgdb.cn/item/604dbbed5aedab222cea1f68.jpg)

> * 感觉上是表现不太好
> * 但是维度可以增加，也许高维空间就可以分类了。

![](https://img.imgdb.cn/item/604dbcc75aedab222ceac74b.jpg)

##### Modifying Model

> * 如果我们使用不同的协方差矩阵，首先参数过多，容易过拟合，或者说效果不佳
> * ![](https://img.imgdb.cn/item/604dc6a45aedab222cf26625.png)
> * 强迫这两个Gaussian 必须使用用一个$\Sigma$， 协方差矩阵

![](https://img.imgdb.cn/item/604dbfcf5aedab222ced26cc.jpg)

### Three Steps

* Function Set(Model)

* $$
  P(C_1|x) = \frac{P(x|C_1)P(C_1)}{P(x|C_1)P(C_1) + P(x|C_2)P(C_2)}
  $$

* Goodness of a function:

  * The mean $\mu$ 和 $\Sigma$ 使得这个$f$的概率最大，那么我们选用这个

* Find the best function:

  * 找到你最喜欢的那个概率函数

#### Sigmoid Function

$$
P(C_1|x) = \frac{P(x|C_1)P(C_1)}{P(x|C_1)P(C_1) + P(x|C_2)P(C_2)} \\
=\frac{1}{1 + \frac{P(x|C_2)P(C_2)}{P(x|C_1)P(C_1)}}= \frac{1}{1+exp(-z)}\\
z = ln\frac{P(x|C_1)p(C_1)}{P(x|C_2)p(C_2)}
$$

**Warning of math**

![](https://img.imgdb.cn/item/604dc2d75aedab222cef69cf.jpg)

![](https://img.imgdb.cn/item/604dc3685aedab222cefd32d.jpg)

![](https://img.imgdb.cn/item/604dc37c5aedab222cefe71b.jpg)

> * $\Sigma_1 = \Sigma_2 = \Sigma$

![](https://img.imgdb.cn/item/604dc44a5aedab222cf09b8c.jpg)

> * 感悟
>   * 看到这里的时候我的内心相当的激动
>   * 从概率的角度出发，我们计算了Gaussian distribution， 想使用这个来把样本分类，但是当我们把两个Gaussian function的$\Sigma$取相同的时候，其实就是一个linear model，那么为什么我们训练的时候不直接使用把这个函数设置为一个linear model 呢？？
>   * 通过gradient descent来把这个函数给找出来！！！
>   * 自然而然的，Logistic Regression 出现了！！！

