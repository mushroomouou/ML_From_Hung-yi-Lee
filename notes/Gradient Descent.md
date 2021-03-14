## Gradient Descent

### Principle part

> * 我们要做的是找到一组函数的参数$w, b$使得$f^*$在$L(f)$这个损失函数上的值最小即就是:
>
> * $$
>   \theta = argminL(\theta) \\
>   L： loss \ function; \ \theta : parameters
>   $$
>
> * 对于参数更新:
>
> * $$
>   \begin{bmatrix}\theta^1_1 \\ \theta_2^1\end{bmatrix} =
>   \begin{bmatrix}\theta_1^0 \\ \theta_2^0\end{bmatrix} -
>   \eta \begin{bmatrix}\frac{\partial L(\theta_1)}{\partial (\theta_1)}\\ \frac{\partial L(\theta_2)}{\partial (\theta_2)}\end{bmatrix}
>   $$
>
>   如果说:
>
>   
>   $$
>   \nabla L(\theta) =\begin{bmatrix}\frac{\partial L(\theta_1)}{\partial (\theta_1)}\\ \frac{\partial L(\theta_2)}{\partial (\theta_2)}\end{bmatrix}
>   $$
>   这就是我们说的$Gradient\ Descent$，是空间的一个向量，是与等高线相切的一个向量。
>
> * 那么简化成下面的式子
>
> * $$
>   \theta^1 = \theta^0 - \eta\nabla L(\theta^0)
>   $$
>
> * 如此连续就可以得到梯度下降的最终的收敛效果。

### Tip 1: 小心地调learning rate

![image.png](https://i.loli.net/2021/03/12/qgXwWsIa7ePyJrB.png)

> * 由于固定的$learning\  rate$会导致无法收敛，那么我们希望模型可以自动更新$Learning\ Rate$

#### $Adagrad$调整$Learning\ Rate$

*每一个不同的参数给与完全不同的$Learning\ Rate$*

* 一般的
  * $w^{t+1} \leftarrow w^t - \eta ^ t \nabla L(w^t)$
* $Adagrad$
  * $w^{t + 1} \leftarrow w^t - \frac{\eta^t}{\sigma ^ t}\nabla L(w^t)$

> * 例子
>   * $w^{1} \leftarrow w^0 - \frac{\eta^0}{\sigma ^ 0}\nabla L(w^0)$
>     * $\sigma ^0 = \sqrt{(\nabla L(w^0))^2}$
>   * $w^{2} \leftarrow w^1 - \frac{\eta^1}{\sigma ^ 1}\nabla L(w^1)$
>     * $\sigma^1 = \sqrt{\frac{(\nabla L(w^0))^2 + (\nabla L(w^1))^2}{2}}$
>   * ......
>   * $w^{t+1} \leftarrow w^t -\frac{\eta ^t}{\sigma ^t}\nabla L(w^t)$
>     * $\eta^t = \frac{\eta}{\sqrt{t + 1}}$
>     * $\sigma^t = \sqrt{\frac{(\nabla L(w^0))^2 + (\nabla L(w^1))^2 + \dots + (\nabla L(w^t))^2}{t + 1}}$
> * 那么梯度下降更新为
>   * $\frac{\eta ^ t}{\sigma ^ t} = \frac{\eta}{\sqrt{\sum_{i=1}^t\nabla L(w^t)^2}}$

![](https://img.imgdb.cn/item/604b60f45aedab222cd47adf.jpg)

*感觉好像微分越大，离最低点的距离就越大*

![](https://img.imgdb.cn/item/604b64ce5aedab222cd6ab93.jpg)

> * 可以发现，不同的$valley$ 可能会与我们想的不同，第二个图的微分很大，但是相比于第一个图，却离得更近了。

> * 而$Adagrad$的 $\sqrt{\sum_{i=1}^t(\nabla L(w^t)^2)}$蕴含了二阶微分的式子，所以相比来说更加的合理$(\frac{First\ derivative}{Second\ derivate})$.

### Tip 2：Stochastic Gradient Descent

$$
L = \sum_n(\hat y^n - (b + \sum w_ix_i^n))^2
$$

* $Gradient Descent$    $\theta ^ i = \theta^{i-1} - \eta \nabla L(\theta^{i-1})$

* $Stochastic Gradient Descent$

* $$
  L^n = (\hat y^n - (b + \sum w_ix_i^n))^2
  $$

* ![](https://img.imgdb.cn/item/604b67a05aedab222cd84514.jpg)

> * 一步一更新不见得会比summation所有的差。

### Tip3 ： Feature Scaling

![](https://img.imgdb.cn/item/604b68825aedab222cd8c529.jpg)

* $Gradient\ Descent$ 开始的位置我们并不知道，如果走的是左图，那么会相当困难去达到$Global\ Min$,相比而言，右图的不论从哪个路线走都会相对容易。

* 这就体现了放缩的重要性。

### Why Gradient Descent work ?

#### 数学

> * 目标： 让$Loss\ Function$越来越小

![](https://img.imgdb.cn/item/604b6a9a5aedab222cda20a1.jpg)

> * Taylor Series
>   * 如果一个函数在$x=x_0$处有$n$阶导数。

$$
h(x) = \sum_{k=0}^{\infin}\frac{f^{k}(x_o)}{k!}(x-x_0)^k
$$

当$x 非常靠近 x_0$的时候
$$
h(x) \approx f(x) + f'(x)(x-x_0)
$$

* 对于多个变元的Taylor Series

![](https://img.imgdb.cn/item/604b6c825aedab222cdb4e12.jpg)

* 如果靠的非常进的话：

  ![](https://img.imgdb.cn/item/604b6caf5aedab222cdb6ae6.jpg)

* 回到Gradient Descent

![](https://img.imgdb.cn/item/604b6d265aedab222cdbb5c2.jpg)

> * 这就是$Loss \ Function$的一个拟合

![](https://img.imgdb.cn/item/604b6e1e5aedab222cdc6104.jpg)

* 首先$（\theta_1, \theta_2）$是在一个圈里面的，也就是上述的$(\theta_1 - a)^2 + (\theta_2 - b)^2 \leq d^2$

* 由于上述的式子我们把$s, u, v$认为是常数。

$$
u(\theta_1 -a)+v(\theta_2 -b) = \begin{bmatrix}\theta_1 -a & \theta_2 -b\end{bmatrix}\begin{bmatrix}u \\ v\end{bmatrix}
$$

* 我们可以理解为这是两个向量的乘积，
* 如何让这个变的最小呢，显然只有当这两个向量完全反向的时候就可以成立

那么
$$
\begin{bmatrix}\theta_1 -a \\ \theta_2 -b\end{bmatrix} = -\eta\begin{bmatrix}u \\ v\end{bmatrix}
$$
那么
$$
\begin{bmatrix}\theta_1 \\ \theta_2\end{bmatrix} = \begin{bmatrix}a \\ b\end{bmatrix} + \begin{bmatrix}\theta_1 -a \\ \theta_2 -b\end{bmatrix}=\begin{bmatrix}a \\ b\end{bmatrix} -\eta\begin{bmatrix}u \\ v\end{bmatrix}=\begin{bmatrix}a \\ b\end{bmatrix} - \eta\begin{bmatrix}\frac{\partial f}{\partial x} \\\frac{\partial f}{\partial y}\end{bmatrix}=\begin{bmatrix}a \\ b\end{bmatrix} - \eta\nabla L(\theta)
$$
