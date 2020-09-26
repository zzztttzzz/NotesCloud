Book Name:

#  1 Introductory Example

* 从一元线性函数到多元线性函数：
  $$
  f(x) = a^Tx
  $$
  $a = [a_1,a_2,...,a_n]^T$,$x=[x_1,x_2,...,x_n]^T$, 则有：
  $$
  \frac{\partial f}{\partial x}=a
  $$

# 2 Derivation

## 2.1 Organization of Elements

* **Definition 1.** 
  $$
  \frac{\partial f}{\partial x}=\left[\begin{array}{cccc}
  \frac{\partial f}{\partial x_{11}} & \frac{\partial f}{\partial x_{12}} & \cdots & \frac{\partial f}{\partial x_{1 n}} \\
  \frac{\partial f}{\partial x_{21}} & \frac{\partial f}{\partial x_{22}} & \cdots & \frac{\partial f}{\partial x_{2 n}} \\
  \vdots & \vdots & \ddots & \vdots \\
  \frac{\partial f}{\partial x_{m 1}} & \frac{\partial f}{\partial x_{m 2}} & \cdots & \frac{\partial f}{\partial x_{m n}}
  \end{array}\right]
  $$
  定义对矩阵的偏导为逐元素求偏导，以及结果的排列顺序问题。事实上是定义为与自变量的形式相同。

## 2.2 Deal with Inner Product

* **Theorem 1.** 对于多元标量函数$f(x) = a^Tx$, 有$\frac{\partial f}{\partial x}=a$

* **Proposition 2.** 对于多元标量函数$f(x) = Tr[a^Tx]$, 有$\frac{\partial f}{\partial x}=a$
  标量上增加了迹函数，不影响结果。

## 2.3 Properties of Trace

* **Deﬁnition 2. **$Tr[A]=\sum_i A_{ii}$
  $A$行数列数相等

* **Theorem 3.** 矩阵迹的性质：

  * (1) $Tr[A+B] = Tr[A]+Tr[B]$
  * (2) $Tr[cA] = cTr[A]$
  * (3) $Tr[AB] = Tr[BA]$
  * (4) $Tr[A_1A_2...A_n] = Tr[A_nA_1...A_{n-1}] $
  * (5) $Tr[A^TB] = \sum_i\sum_jA_{ij}B_{ij}$
  * (6) $Tr[A] = Tr[A^T]$

  (1)(2)描述了线性性，(3)(4)可以理解为轮换性，(5)其实是用迹定义了矩阵的内积(Generalized Inner Product)

## 2.4 Deal with Generalized Inner Product

* **Theorem 4.** 对于多元标量函数，$f(x) = Tr[A^Tx]$, 有$\frac{\partial f}{\partial x} = A$.
  是将2.2中的偏导扩展为了矩阵形式

## 2.5 Define Matrix Differential

* **Definition 3.** 定义矩阵微分：
  $$
  \mathrm{d} A=\left[\begin{array}{cccc}
  \mathrm{d} A_{11} & \mathrm{d} A_{12} & \ldots & \mathrm{d} A_{1 n} \\
  \mathrm{d} A_{21} & \mathrm{d} A_{22} & \ldots & \mathrm{d} A_{2 n} \\
  \vdots & \vdots & \ddots & \vdots \\
  \mathrm{d} A_{m 1} & \mathrm{d} A_{m 2} & \ldots & \mathrm{d} A_{m n}
  \end{array}\right]
  $$
  其实就是逐元素微分

* **Theorem 5.** $\mathrm{d}Tr[A] = Tr[\mathrm{d}A]$
  其实可以合并到迹函数的性质中去，是由线性性而来的。

* **Theorem 6.** 对于标量函数$f$，任意的$x$，都有：
  $$
  \mathrm{d} f=\operatorname{Tr}\left[\left(\frac{\partial f}{\partial x}\right)^{\mathrm{T}} \mathrm{d} x\right]
  $$
  广义上定义了某函数的微分同偏导的关系，微分等于 偏导矩阵 同 自变量微分矩阵 的广义内积。

## 2.6 Matrix Differential Properties

* **Theorem 7.** 矩阵微分的性质：

  * $d(cA) = cd(A)$
  * $d(A+B) = dA+dB$
  * $d(AB) = dAB+AdB$

  由于是逐元素微分，所以性质比较显然

* **Example 4.** $f(x) = x^TAx$, $x$为向量，其偏导为：
  $$
  \frac{\partial f}{\partial x} = Ax + A^Tx
  $$
  当$A$为对称阵的时候，可以写为：$\frac{\partial f}{\partial x} = 2Ax$

* **Example 5.** 对于非奇异矩阵$X$
  $$
  XX^{-1} = I \\ dI = 0 = d(XX^{-1})=dXX^{-1}+XdX^{-1} \\ dX^{-1} = -X^{-1}dXX^{-1}
  $$

## 2.7 Schema of Handling Scalar Function

1. $df = dTr[f] = Tr[df]$

2. 利用矩阵微分，迹函数以及其他线性代数的性质，化为如下形式：
   $$
   df = Tr[A^Tx]
   $$

3. 则可以得到最终的偏导结果：
   $$
   \frac{\partial f}{\partial x} = A
   $$

## 2.8 Determinant

* $$
  \begin{aligned}
  \mathrm{d} \operatorname{det}(A) 
  &=\operatorname{Tr}\left[\operatorname{det}(A) A^{-1} \mathrm{d} A\right]
  \end{aligned}
  $$

* $$
  \begin{aligned}
  \mathrm{dln}\operatorname{det}(A) 
  &=\operatorname{Tr}\left[ A^{-1} \mathrm{d} A\right]
  \end{aligned}
  $$

## 2.9 Vector Function and Vector Variable

* **Definition 4.** 对于向量函数$f = [f_1,f_2,...,f_n]^T$, 以及$f_i=f_i(x)$, 其中$x = [x_1,x_2,...,x_m]^T$,有如下的定义：
  $$
  \frac{\partial f}{\partial x}=\left[\begin{array}{cccc}
  \frac{\partial f_{1}}{\partial x_{1}} & \frac{\partial f_{2}}{\partial x_{1}} & \cdots & \frac{\partial f_{n}}{\partial x_{1}} \\
  \frac{\partial f_{1}}{\partial x_{2}} & \frac{\partial f_{2}}{\partial x_{2}} & \cdots & \frac{\partial f_{n}}{\partial x_{2}} \\
  \vdots & \vdots & \ddots & \vdots \\
  \frac{\partial f_{1}}{\partial x_{m}} & \frac{\partial f_{2}}{\partial x_{m}} & \cdots & \frac{\partial f_{n}}{\partial x_{m}}
  \end{array}\right]
  $$
  ​		每一行是对同一维的$x_i$求偏导结果，每一列对应同一个函数的偏导结果。可以理解为将每一个标量函数的结果(为一列)写在一起组成矩阵的形式。

* **Example 6.**
  Hessian Matrix：
  $$
  H(f)=\left[\begin{array}{cccc}
  \frac{\partial^{2} f}{\partial x_{1}^{2}} & \frac{\partial^{2} f}{\partial x_{1} \partial x_{2}} & \cdots & \frac{\partial^{2} f}{\partial x_{1} \partial x_{n}} \\
  \frac{\partial^{2} f}{\partial x_{2} \partial x_{1}} & \frac{\partial^{2} f}{\partial x_{2}^{2}} & \cdots & \frac{\partial^{2} f}{\partial x_{2} \partial x_{n}} \\
  \vdots & \vdots & \ddots & \vdots \\
  \frac{\partial^{2} f}{\partial x_{n} \partial x_{1}} & \frac{\partial^{2} f}{\partial x_{n} \partial x_{2}} & \cdots & \frac{\partial^{2} f}{\partial x_{n}^{2}}
  \end{array}\right]
  $$
  Jacobian Matrix:
  $$
  J=\left[\begin{array}{ccc}
  \frac{\partial y_{1}}{\partial x_{1}} & \cdots & \frac{\partial y_{1}}{\partial x_{n}} \\
  \vdots & \ddots & \vdots \\
  \frac{\partial y_{m}}{\partial x_{1}} & \cdots & \frac{\partial y_{m}}{\partial x_{n}}
  \end{array}\right]
  $$
  

  文中关于二阶偏导的定义应该是写错了，$\frac{\partial^2f}{\partial x_1\partial x_2}$应该是$\frac{\partial}{\partial x_2}(\frac{\partial f}{\partial x_1})$，在这样的定义下，以及**Definition 4**中关于向量函数的偏导定义下，上述的两个Matrix可以写为矩阵矩阵QQ偏导的形式：
  Hessian Matrix: $H(f) = \frac{\partial}{\partial x}(\frac{\partial f}{\partial x^T})$，相当于先求偏导得到一个导函数的行向量，然后再求偏导得到最终的结果，由于Hessian Matrix本身求偏导顺序的问题，需要转置。

  Jacobian Matrix: $J(f) = (\frac{\partial f}{\partial x})^T$ .
  注：上述Hessian Matrix中的$f$为标量函数，而Jacobian Matrix中的$f$为向量函数。

## 2.10 Vector Function Differential

* **Theorem 9.** 在**Definition 4.**的定义之下，有$df = \left(\frac{\partial f}{\partial x}\right)^Tdx$.
  事实上，是对**Theorem 6.**的扩展。

* **Example 7.** 考虑从$\xi$到$x$的变换，$x=\sigma \Lambda^{-0.5} W^{T} \xi$.
  想要得到其Jacobian Matrix，$Jm$，首先要得到$\frac{\partial x}{\partial \xi}$，而想要得到偏导，需要首先对等式两侧同时求微分，根据**Definition 4.**的性质以及Jacobian Matrix的矩阵形式，双重转置之后得到：
  $$
  J_m =\sigma \Lambda^{-0.5} W^{T}
  $$

* **Theorem 10.** 如果$x,y$向量维数相同，有：$\left(\frac{\partial f}{\partial x}\right)^{-1}=\frac{\partial x}{\partial f}$

## 2.11 Chain Rule

* **Theorem 11.** 当有n个列向量$x^{(1)},x^{(2)},...,x^{(n)}$, 且向量的维数各不相同，分别为$l_1,l_2,...,l_n$, 已知$x^{(i)}$为$x^{(i-1)}$的函数，则有链式法则：
  $$
  \frac{\partial x^{(n)}}{\partial x^{(1)}}=\frac{\partial x^{(2)}}{\partial x^{(1)}} \frac{\partial x^{(3)}}{\partial x^{(2)}} \ldots \frac{\partial x^{(n)}}{\partial x^{(n-1)}}
  $$

* **Proposition 12.** 考虑一个链式法则的实例，$x \rightarrow y_{i} \rightarrow z$，$x,z$均为实数，$y$为向量，$z=z(y), y_{i}=y_{i}(x), i=1,2 \ldots, n$. 则有：
  $$
  \frac{\partial z}{\partial x}=\frac{\partial y}{\partial x} \frac{\partial z}{\partial y}=\sum_{i=1}^{n} \frac{\partial y_{i}}{\partial x} \frac{\partial z}{\partial y_{i}}
  $$
  可以用来很方便地表示多元函数链式法则的偏导规则。

* **Example 8.** 求对$\mu$的偏导$(x-\mu)^T\Sigma ^{-1}(x-\mu)$.
  $$
  \begin{aligned}
  & \frac{\partial\left[(x-\mu)^{\mathrm{T}} \Sigma^{-1}(x-\mu)\right]}{\partial \mu} \\
  =& \frac{\partial[x-\mu]}{\partial \mu} \frac{\partial\left[(x-\mu)^{\mathrm{T}} \Sigma^{-1}(x-\mu)\right]}{\partial[x-\mu]} \\
  (e x a m p l e(4))=& \frac{\partial[x-\mu]}{\partial \mu} 2 \Sigma^{-1}(x-\mu) \\
  (\mathrm{d}[x-\mu]=-I \mathrm{d} \mu)=&-I 2 \Sigma^{-1}(x-\mu) \\
  =&-2 \Sigma^{-1}(x-\mu)
  \end{aligned}
  $$
  

# 3 Application

**Focus on Gaussian Distribution**

## 3.2 General Multivariate Gaussian Distribution

