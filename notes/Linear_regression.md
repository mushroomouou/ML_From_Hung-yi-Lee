
## Regression

![](https://img.imgdb.cn/item/6044c5d0cef1ec5e6fd90d67.jpg)

> * 由     $f$    接受样本的数据  $input$ ，得到这组数据的   $output$。

### Pokemon

![](https://img.imgdb.cn/item/6044c69acef1ec5e6fd97178.jpg)

> * 想要通过面板的数据去预测这只宝可梦进化以后的CP值。

* ML' basis setp

  * Step 1: Model

    * ![](https://img.imgdb.cn/item/6044c83ccef1ec5e6fda405f.jpg)
    * 上述的模型是一种线性的$Model$，
      * $x_i$是各种的$attr$是属于$x$
      * $w_i$是对应$attr$的权重$weight$
      * $b$是截距$bias$

  * Step 2: Goodness of Function

    * ![](https://img.imgdb.cn/item/6044c965cef1ec5e6fdab428.jpg)
    * 模型的选入
      * 上述的每一个样本标记有每一个pokemon的进化前和进化后的cp值
    * Loss Function L:
      * 可以理解为函数的函数
      * $L(f) = L(w,b)$
      * 用来衡量一组参数的好坏
      * $\sum_{n=1}^{10}(\hat y_n - (b + w\cdot x_{cp(n)})$
      * 估测误差越大就越不好，可以理解为$Loss\ Function$判断这个拟合函数的好坏
      * ![](https://img.imgdb.cn/item/6044cb5ccef1ec5e6fdb747c.jpg)
      * 那么我们要找到的哪个拟合函数就应该是使得这个loss函数最小的那一组参数
      * $f^* = argminL(f)$
      * $w^*, b^* = argminL(w, b)$
      * 而找到这个函数$f$的方法就是使用$Gradient\ Descent$

  * Step 3: Gradient Descent

    * ![](https://img.imgdb.cn/item/6044ce00cef1ec5e6fdc6f17.jpg)

    * 步骤：

      * 一个参数

        * 随机选择一个初始的值$w_0$
        * 计算每一个权重的对应微分值
        * 更新$w_1 =: w_0 - \alpha \frac{dL}{dw}|_{w=w_0}$

      * $w, b$两个参数

        * 选择两个初始值$w_0, b_0$
        * 计算偏微分
        * 更新$w_1 =: w_0 - \alpha\frac{\partial L}{\partial w}|_{w=w_0, b=b_0} $
        * $b_1 =: b_0 - \alpha\frac{\partial L}{\partial b}|_{w=w_0, b=b_0} $

      * 关于gradient

        * ![](https://img.imgdb.cn/item/6044cef4cef1ec5e6fdcd3d2.jpg)
        * 把偏微分写成一个向量之后这就是这个L的梯度。
      * visualization
        * ![](https://img.imgdb.cn/item/6044cfeacef1ec5e6fdd3050.jpg) 	
      
    * 关于local minimum and global minimum
      * ![](https://img.imgdb.cn/item/6044d03dcef1ec5e6fdd4d8f.jpg)
        
        * 对于Linear regression 来说仅仅存在一个global minimum，而不存在local minimum。
      * Formulation
    	* ![](https://img.imgdb.cn/item/6044d120cef1ec5e6fdda6c9.jpg)
    	
    * 可以使用$Loss\ Function$ 去得到error

    * 优化

      * 使用一个额外的features
      * ![](https://img.imgdb.cn/item/6044d305cef1ec5e6fde6271.jpg)
      * 以及后面的四次方，等等等等

        * ![](https://img.imgdb.cn/item/6044d45ccef1ec5e6fdee8f9.jpg)
      * 过拟合（$overfitting$）
        * ![](https://img.imgdb.cn/item/6044d4d8cef1ec5e6fdf1a15.jpg)
        * 如果说feature越多，就意味着所蕴含的函数就越多，那么就更有可能去找到一个函数去拟合这组数据
        * ![](https://img.imgdb.cn/item/6044d54ccef1ec5e6fdf47d3.jpg)
        * 在训练集可以做的很好，但是在测试集上做的就不一定很好。

      * Let‘s do more data.
        * ![](https://img.imgdb.cn/item/6044d60ccef1ec5e6fdf8c5e.jpg)

        * 当考虑到更多的数据时，会发现还有一种蕴藏的feature，比如Pokemon的物种。
          * ![image.png](https://i.loli.net/2021/03/07/OutLa39pW6ENxUD.png)
          * 使用$\delta$去判断Pokemon的种类，这样就使用对应种类的参数。
          
        * 如果感觉还是不够优秀，那么我们就把所有的feature全部嵌入

          * ![image.png](https://i.loli.net/2021/03/07/JpZWltHiDq5hP19.png)
          * 但是
          * ![](https://img.imgdb.cn/item/6044d886cef1ec5e6fe07fe2.jpg)

        * 如何放置过拟合----使用Regularization

          1. 改变我们的$Loss Function$

             * ![](https://img.imgdb.cn/item/6044d8fecef1ec5e6fe0b1f6.jpg)
             
          2. $Regularization$

             * ![](https://img.imgdb.cn/item/6044d9a2cef1ec5e6fe10128.jpg)

             * 增加的那一项可以理解为故意增大$Loss\ Function$对函数$f$的差评，惩罚那些让拟合非常好的$f$
             * 引入$\lambda\ \ regularization$的目的是为了让拟合函数$f$的值变得更加平滑。所以这里我们不对$b$进行正则化惩罚，是由于$b$是截距，不会影响曲线的平滑度。

             

             