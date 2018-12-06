## 2018-11-21
---
### 正规方程解法$NormalEquation$
线性回归直接得到使损失函数最小化的参数

$$
\theta = (X^TX)^{-1}X^TY
$$
其中:
* $\theta$是参数向量
* $X$是样本矩阵（添加过截距列）
* $Y$是结果矩阵

---
### 梯度下降法$GradientDescent$

## 2018-12-04
---
### Logistic回归
* sigmoid函数
$$
    f(x) = \frac{1}{1+e^{\theta'*X}}
$$

## 2018-12-5
---
### 高级优化
* 除梯度下降外，一些其他的优化方法
  - Conjugate gradient
  - BFGS，共轭梯度法
  - L-BFGS
- 优点，不用手动选择学习率$\alpha$
在MATLAB中使用优化后的梯度下降
先编写一个costFunction
```MATLAB
function [jVal,gradient] = costFunction(theta)
    jVal = (theta(1)-5)^2 + (theta(2)-5)^2;
    gradient = zeros(2,1);
    gradient(1) = 2*(theta(1)-5);
    gradient(2) = 2*(theta(2)-5);
    ...
end
```
jVal是$J(\theta)$的值
gradient(1) 是$\frac{\partial}{\partial\theta_1}J$的值，其余类推
已知写到gradient(n)等于多少。
然后就可以调用高级函数自动进行迭代优化

先设置好函数参数
```MATLAB
options = optimset('GradObj','on','MaxIter',100);
initialTheta = zeros(2,1)
```
然后调用函数
```MATLAB
[optTheta,functionVal,exitFlag] = fminunc(@costFunction,initialTheta,options)
```
得到的optTheta就是最优化后的参数，functionVal是损失函数最小值。

## 2018-12-6
---
### 过拟合Overfitting
* 特征多，样本少，会导致过拟合...
  * 舍弃部分特征，减少特征数量
  * 正则化

### 正则化regularization
* 可以使某些参数变小
* 可以使不可逆的样本-特征矩阵变得可逆
* 正则化后的损失函数
  $$
  J(\theta)=\frac{1}{2m}\left[\sum^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})^2+\lambda\sum^n_{j=1}\theta^2_j\right]
  $$
* 正则化后的梯度下降
  $$
  \theta_0 := \theta_0 -\alpha\frac{1}{m}\sum^m_{i=1}\big(h_\theta(x^{(i)})-y^{(i)}\big)x_0^{(i)}
  $$
  $$
  \theta_j := \theta_0 -\alpha\left[\frac{1}{m}\sum^m_{i=1}\big(h_\theta(x^{(i)})-y^{(i)}\big)x_0^{(i)} + \frac{\lambda}{m}\theta_j\right]
  $$