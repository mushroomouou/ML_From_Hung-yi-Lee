# Basis Concept

## *Error 到底来自于什么地方* 

> * 一种来自于$bias（偏差）$, 一种来自于$variance（方差）$,我们要去评定哪一个是影响$error$的决定性变量

![](https://img.imgdb.cn/item/604636b15aedab222c149b9b.jpg)

> * 模型只能从数据中得出来对于这个数据的猜测函数$f^*$, 但是真正的函数是程序编写者才知道的逻辑，我们只能希望$f^*$可以和$\hat f$稍微靠进一些，而靠近的过程就是减少$bias$, 和减少$variance$的过程。

![](https://img.imgdb.cn/item/60463b265aedab222c16cb1b.jpg)

> * 模型的$feature$越多，那么这个模型所蕴含的函数空间就越大，那么就有更大的可能去找到那个真正的$\hat y$

![](https://img.imgdb.cn/item/60463bc05aedab222c171581.jpg)

> * 如果说你的$bias$过大，表示你几乎不能拟合。
>   1. 重新构建一个模型。
>   2. 重新设置$feature$。
>   3. 添加data。

![](https://img.imgdb.cn/item/60463c4b5aedab222c176077.jpg)

> * 如果说你的$variance$过大
>   1. More data
>   2. Regularization

![](https://img.imgdb.cn/item/60463d9b5aedab222c180362.jpg)

> * Model Selection

![](https://img.imgdb.cn/item/604796e65aedab222cd112e3.jpg)
> * 在测试集上表现好的，也不一定是最好的模型，还需要再真实的数据集上去观察效果。
> * 这里我们一般把机器学习的数据集划分为，训练集（train dataset），测试集（test dataset），以及验证集（validation dataset）

## Cross Validation

![](https://img.imgdb.cn/item/604797f35aedab222cd1bf71.jpg)

> * 指再训练集上完全划分为几个不同的区块，然后使用一个当作测试集，其余为训练集去训练模型，打分。
> 

## N-fold Cross Validation
![](https://img.imgdb.cn/item/604798555aedab222cd1f90d.jpg)

> * 指再训练集上完全划分为几个不同的区块，然后交叉的使用一个当作测试集，其余为训练集去训练模型，打分。遍历所有的区块，也就是说每一个区块都有一个机会去当做测试集被测试，那么得到的分数的个数为原来训练集被划分的区块的个数。
> 

