## 2 熟悉Eigen 矩阵运算

1. 线性方程组的矩阵满秩时，**x**有解且唯一

2. 高斯消元法是将方程组中的一方程的未知数用含有另一未知数的代数式表示，并将其代人到另一方程中，这就消去了一未知数，得到一解；或将方程组中的一方程倍乘某个常数加到另外一方程中去，也可达到消去一未知数的目的。

3. 如果非奇异矩阵A能够化成正交矩阵Q与上三角矩阵R的乘积，即A=QR，则称其为A的QR分解。其中Q的列向量是A的列空间的标准正交基，R是一个非奇异可逆的上三角矩阵。

4. Cholesky 分解是把一个对称正定的矩阵表示成一个下三角矩阵L和其转置的乘积的分解。它要求矩阵的所有特征值必须大于零，故分解的下三角的对角元也是大于零的。

5.  

   ```C++
   #include <iostream>
   using namespace std;
   #include <eigen3/Eigen/Core>
   #include <eigen3/Eigen/Dense>
   #define MATRIX_SIZE 100
   
   int main( int argc, char** argv )
   {
       Eigen::Matrix< double, Eigen::Dynamic, Eigen::Dynamic > x;
       Eigen::Matrix< double, Eigen::Dynamic, Eigen::Dynamic > x2;
       Eigen::Matrix< double, MATRIX_SIZE, MATRIX_SIZE > matrix_NN;
       matrix_NN = Eigen::MatrixXd::Random( MATRIX_SIZE, MATRIX_SIZE );
       Eigen::Matrix< double, MATRIX_SIZE,  1> v_Nd;
       v_Nd = Eigen::MatrixXd::Random( MATRIX_SIZE,1 );
   
       x = matrix_NN.colPivHouseholderQr().solve(v_Nd);
       cout << x << endl;
       x2 = matrix_NN.llt().solve(v_Nd);
       cout << x2 << endl;
       return 0;
   }
   ```

 

## 3 几何运算练习

```
#include <iostream>
#include <cmath>
using namespace std;
#include <eigen3/Eigen/Core>
#include <eigen3/Eigen/Geometry>

int main ( int argc, char** argv )
{

    Eigen::Quaterniond q1(0.55,0.3,0.2,0.2);
    Eigen::Quaterniond q2(-0.1,0.3,-0.7,0.2);
    q1= q1.normalized();
    q2= q2.normalized();
    Eigen::Matrix3d R_ = q1.matrix().inverse();
    Eigen::Matrix3d R2 = q2.matrix();
    Eigen::Matrix<double,3,1> P1;
    Eigen::Matrix<double,3,1> P2;
    Eigen::Matrix<double,3,1> t1;
    Eigen::Matrix<double,3,1> t2;
    P1 << 0.5,-0.1,0.2;
    t1 << 0.7,1.1,0.2;
    t2 << -0.1,0.4,0.8;
    P2 = R2 * R_ * (P1-t1) + t2;
    cout<<"quaternion = \n"<<P2 <<endl;
    return 0;
}
```



## 5 罗德里格斯公式

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Rodrigues-formula.svg/300px-Rodrigues-formula.svg.png)


$$
\begin{align}

v_\parallel &= kk^Tv  \\
v_\perp & = v-v_\parallel=(1-kk^T)v \\
v_{rot} & = v_{\parallel rot} + v_{\perp rot} \\
	  & = v_\parallel+(cos{\theta}v_\perp +sin{\theta}k\times v) \\
	  & = [cos{\theta} + (1-cos{\theta})kk^T + sin{\theta}k^{\wedge}]v \\
R & = cos{\theta} + （1-cos{\theta})kk^T+sin{\theta}k^{\wedge}
\end{align}
$$

## 6 四元数

设
$$
q = \begin{matrix} [s_q &v_q] \end{matrix}\\
p = \begin{matrix} [0 &v_p] \end{matrix} \\
$$
有
$$
\begin{align}
qp & =\begin{matrix}[-v_q^Tv_p & s_qv_p+v_q^{\wedge}v_p]\end{matrix}\\
q^{-1} & = \begin{matrix}[s_q & -v_q] \end{matrix}
\end{align}
$$
则
$$
R=qpq^{-1}=\left[ \begin{matrix} 0 & 0_{1\times3}\\0_{3 \times1} & \end{matrix} \right]
$$


## 7 熟悉C++11

for：对象迭代

auto&：自动推导类型

[] (const A&a1,const A&a2) {return a1.index<a2.index;}}:  lambda表达式