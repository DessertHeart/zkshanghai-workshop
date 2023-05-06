# 第3课 课后作业

> 题目: https://zkshanghai.xyz/notes/exercise3.html

## 第1题 二次非剩余 Quadratic nonresidue

- **完备性**：如果 $QR(m, x)=0$ 并且双方都按照协议行事，那么验证者总是接受。

   > 双方诚实的基础上，

  - $b=0$， $y=s^2x$ 时：Prover计算 $QR(m,y)=QR(m,s^2x)$ ，由于 $QR(m,x)=0$ ，则一定有 $QR(m,s^2x)=0$ ，因此Verifier接收到的就是0，验证 $QR(m,y)=0=b$ ，Verifier accept。
  - $b=1$， $y = s^2$ 时：Prover计算 $QR(m,y)=QR(m,s^2)$ 。 $s^2$ 一定是模 $m$ 的二次剩余，因为根据定义，存在一个数 $s$ ，使得 $s^2 = s^2 \mod m$ 。因此 $QR(m,s^2)=1$ ，Verifier就会接收到1，验证 $QR(m,y)=1=b$ ，Verifier accept。

- **可靠性**：如果 $QR(m, x)=1$ ，那么无论 Prover 做什么（Prover 不必遵循协议），Verifer 都会以 $\geq 1 / 2$ 的概率拒绝

  - 对于Prover来说，如果诚实计算 $QR(m,y)$ ，只会有 $1/2$ 的概率通过验证，如果不诚实计算 $QR(m,y)$ ，不会有超过 $1/2$ 概率通过验证。因此，Verifier总会以超过 $1/2$ 的概率拒绝。如下例（假设事实为 $QR(m,x)=1 $，即 $x$ 是模 $m$ 的二次剩余）：
    1. Verifier选择 $b=0$ ，发送 $y = s^2x$ ， $QR(m,y)=QR(m,s^2x)=1 \neq b$ ；
    2. Verifier选择 $b=1$ ，发送 $y=s^2$ ， $QR(m,y)=QR(m,s^2)=1=b$ 。

## 第2题 二次剩余 Quadratic residue

- **完备性**：如果双方都按照协议行事，那么 Verifier 总是接受。
  
  - 答：

- **可靠性**：

  - 答：

- **知识可靠性**：

  - 答：

- **零知识**：

  - 答：

## 第3题 双线性自映射意味着DDH的失效 Self-pairing implies failure of DDH

答：

## 第4题 BLS 签名聚合 BLS signature aggregation

答：

