# 第5课 课后作业

> https://zkshanghai.xyz/notes/exercise5.html

> KZG多项式承诺：https://dankradfeist.de/ethereum/2021/10/13/kate-polynomial-commitments-mandarin.html

## 第1题 制作一个假的 KZG 证明

要想找到一个假的 $π'$ 使得 𝑒(𝐶 − $[𝑦]_1$, $[1]_2$) = 𝑒($𝜋$, $[𝛼]_2$ − $[𝑧]_2$ )，因为造假者不知道 $f(x)$ ，故而无法得出正确的 $y$ ，故而关键是找到 假的 $y'$ 带入使得Verify的公式成立

## 第2题

朗格朗日插值多项式，实际是多个多项式相加而得， $y_i$ 为缩放系数，给定点和评估 ${(x_i,y_i)}_{i=0}^{d−1}$ ，我们可以构造一个**插值多项式** $L(X)$ ，使 
 $L(x_i)=y_i$ ，此处即   $x_i=i$  $y_i=m_i$ ,代入:

$$
L_i(X) :=\prod_{x_j \neq x_i}{\frac{X-x_j}{x_i-x_j}}
\tag{1}
$$

将该值算出得出一个 $L(X)$ ，作为输入代入KZG承诺方案

## 第3题

关键：拉格朗日多项式插值法
