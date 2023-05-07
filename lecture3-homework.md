# 第3课 课后作业

> 题目(抽象代数): https://zkshanghai.xyz/notes/exercise3.html


## 第1题 二次非剩余 Quadratic nonresidue

- **完备性**：如果 $QR(m, x)=0$ 并且双方都按照协议行事，那么验证者总是接受。

   > 双方诚实的基础上，

  - $b=0$， $y=s^2x$ 时：Prover计算 $QR(m,y)=QR(m,s^2x)$ ，由于 $QR(m,x)=0$ ，则一定有 $QR(m,s^2x)=0$ ，因此Verifier接收到的就是0，验证 $QR(m,y)=0=b$ ，Verifier accept。
  - $b=1$， $y = s^2$ 时：Prover计算 $QR(m,y)=QR(m,s^2)$ 。 $s^2$ 一定是模 $m$ 的二次剩余，因为根据定义，存在一个数 $s$ ，使得 $s^2 = s^2 \mod m$ 。因此 $QR(m,s^2)=1$ ，Verifier就会接收到1，验证 $QR(m,y)=1=b$ ，Verifier accept。

- **可靠性**：如果 $QR(m, x)=1$ ，那么无论 Prover 做什么（Prover 不必遵循协议），Verifer 都会以 $\geq 1 / 2$ 的概率拒绝

  - 对于Prover来说，如果诚实计算 $QR(m,y)$ ，只会有 $1/2$ 的概率通过验证，如果不诚实计算 $QR(m,y)$ ，不会有超过 $1/2$ 概率通过验证。因此，Verifier总会以超过 $1/2$ 的概率拒绝。如下例（假设事实为 $QR(m,x)=1 $，即 $x$ 是模 $m$ 的二次剩余）：
    1. Verifier选择 $b=0$ ，发送 $y = s^2x$ ， $QR(m,y)=QR(m,s^2x)=1 \neq b$ ；
    2. Verifier选择 $b=1$ ，发送 $y=s^2$ ， $QR(m,y)=QR(m,s^2)=1=b$ 。

## 第2题 二次剩余 Quadratic residue *(ToDo)*

- **完备性**：如果双方都按照协议行事，那么 Verifier 总是接受。

- **可靠性**：

- **知识可靠性**：

- **零知识**：

## 第3题 双线性自映射意味着DDH的失效 Self-pairing implies failure of DDH
> 阿贝尔群：亦称交换群。一种重要的群类。对于群 $G$ 中任意二元 $a$ ， $b$ ，一般地，除了结合律外， $ab≠ba$ 若群 $G$ 的运算满足交换律，即对任意的 $a$ ， $b∈G$ 都有 $ab=ba$ ，则称 $G$ 为阿贝尔群。

> [双线性映射](https://www.bilibili.com/video/BV11M411m7Qq/?spm_id_from=333.337.search-card.all.click&vd_source=0dd037413d496f35de84d58a72548d41)：1.双线性 2.非退化性 3.可计算性

要判断等式 $\alpha \beta g = y$ 是否成立，只需要计算 $e(\alpha g, \beta g) = e(y, g)$ 是否成立（双线性映射 “可计算性” 性质）。在等式 $\alpha \beta g = y$ 两端同时计算与 $g$ 的映射得到 $e(\alpha \beta g, g) = e(y, g)$ 。而 $e(\alpha \beta g, g) = e(\alpha g, \beta g)$ (?)

## 第4题 BLS 签名聚合 BLS signature aggregation

1. **验证算法始终能接受正确的签名**。因为在 $Verifiy(pk,m,\sigma)$ 这一步，等式左端 $e(g_0,\sigma) = e(g_0, \alpha H(m))$ ，等式右端 $e(pk,H(m)) = e(\alpha g_0, H(m))= e(g_0,\alpha H(m))$ ，等式两端相等，会始终通过算法验证。

2. **选择消息攻击下的存在性不可伪造性**。攻击者想要伪造签名 $\sigma \leftarrow \alpha H(m)$ ，首先在多项式时间计算出 $\alpha$ 是困难的，因为知道公钥和生成元 $g_0$ 在多项式时间内计算出私钥是离散对数困难问题。其次，攻击者想要任选消息 $m$ 使得 $H(m)$ 等于一个特定的值，这在多项式时间内也无法做到（因为哈希函数具有抗碰撞性，无法在多项式时间内找到一个 $m$ ，使得 $H(m)$ 等于一个事先给定的值）。

