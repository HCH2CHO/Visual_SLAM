## 2 群的性质

1. {**Z**,+}是群。

  
   $$
   \begin{align}
   封闭性：& \forall z_1,z_2 \in Z, z_1+z_2\in Z  \\
   结合律：& \forall z_1,z_2,z_3 \in Z,(z_1+z_2)+z_3=z_1+(z_2+z_3) \\
   幺元：& \exists 0 \in Z, \forall z \in Z,0+z=z+0=z \\
   逆: & \forall z \in Z, \exists z^{-1} \in Z,z+ z^{-1}=z- z=0
   \end{align}
   $$

2. {**N**,+}不是群，不满足逆的性质。

$$
逆:\forall n \in N, n^{-1}=-n \notin N
$$

## 3 验证向量叉乘的李代数性质

$$
\begin{align}
封闭性: & \forall X,Y \in R^3,X \times Y \in R^3 \\ 
双线性: & \forall X,Y,Z, \in R^3, a,b\in R ，有\\
&(aX+bY) \times Z = a(X \times Z) +b(Y \times Z),\\
&Z \times (aX+bY)= a(Z \times X) +b(Z \times Y)\\
自反性: & \forall X \in R^3, X \times X = 0\\
雅可比等价: & \forall X,Y,Z \in R^3\\
& X \times(Y \times Z) +Y \times(Z \times X)+Z \times(X \times Y) = 0
\end{align}
$$

因此，叉乘满足李代数性质

## 4 推导SE(3)的指数映射

$$
\begin{align}
已知 exp(A) = &  \sum_{n=0}^{\infty}\frac{1}{n!}A^n ,a^{\wedge}a^{\wedge} = aa^T-I,a^{\wedge}a^{\wedge}a^{\wedge}=-a^{\wedge}\\

\end{align}
$$

$$
\begin{align}
\sum_{n=0}^{\infty} \frac {1}{(n+1)!}(\phi^{\wedge})^n  = &\sum_{n=0}^{\infty} \frac {1}{(n+1)!}(\theta a^{\wedge})^n \\
= & I +\frac {1}{2!}\theta a^{\wedge} + \frac {1}{3!}\theta^2 a^{\wedge}a^{\wedge} +\frac {1}{4!}\theta^3 a^{\wedge}a^{\wedge}a^{\wedge} +\frac {1}{5!}\theta^4 a^{\wedge}a^{\wedge}a^{\wedge}a^{\wedge} +...\\
= & aa^T -a^{\wedge}a^{\wedge} +\frac{1}{2!}\theta a^{\wedge}+\frac{1}{3!}\theta a^{\wedge}a^{\wedge} - \frac{1}{4!}\theta^3 a^{\wedge} - \frac{1}{5!}\theta^4 a^{\wedge}a^{\wedge} +...\\
= & aa^T + (\frac{1}{2!}\theta - \frac{1}{4!}\theta^3 +...)a^{\wedge} +(-1 + \frac{1}{3!}\theta^2 -\frac{1}{5!}\theta^4 +...)(aa^T-I) \\
= & aa^T + \frac{1-cos\theta}{\theta}a^{\wedge} +(-\frac{sin\theta}{\theta})(aa^T-I) \\
= & \frac{sin\theta}{\theta}I +(1- \frac{sin\theta}{\theta})aa^T + \frac{1-cos\theta}{\theta}a^{\wedge}
\end{align}
$$



## 5 伴随

对于任意旋转矩阵**R**及任意向量**a**,**b**,有：
$$
\begin{align}
& (Ra) \times (Rb) = R(a \times b) \\
& (Ra)^{\wedge} v = Ra \times v =Ra \times (RR^{-1}v) \\
& 即(Ra)^{\wedge} = Ra^{\wedge}R^{-1} \\
& 根据矩阵性质，\\
& R \ exp(p^{\wedge})R^T = R \ exp(p^{\wedge})R^{-1} = exp(Rp^{\wedge}R^{-1}) = exp((Ra)^{\wedge})
\end{align}
$$
