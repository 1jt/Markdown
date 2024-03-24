# What did you learn？

> Security Definitions and Proofs

## [Number 27: What is the AEAD security definition for symmetric key encryption?](https://bristolcrypto.blogspot.com/2015/04/52-things-number-27-what-is-aead.html)

前面（#18）介绍的分组密码的各种模式，本质上是为了机密性（confidentiality）服务的，现实情况中，我们还需要保证完整性（integrity）和认证性（authenticity）。
> **AE** 指的就是 **Authenticated Encryption**，认证加密
> **AD** 指的就是 **variable-length Associated Data**，例如 packet header
> > For more information on the impact of associated data, see [here](https://dl.acm.org/doi/10.1145/586110.586125) and [here](https://eprint.iacr.org/2011/269.pdf).

为了达到这些目的，引入一个叫做 message authentication code （MAC）的东西，经典的实现方法是利用哈希函数（HMAC）。但是加密和认证这两个原语不能随随便便地组合在一起。为了达到 IND-CCA 安全性，我们必须遵守“先加密后认证”原则（'Encrypt-then-MAC' paradigm）
> [Encrypt-and-MAC](https://link.springer.com/chapter/10.1007/3-540-44448-3_41), [MAC-then-Encrypt](https://eprint.iacr.org/2014/206.pdf) 是不可以的，英文教材可以参照 **P132** (有证明)

We normally expect authenticity and integrity but not confidentiality from this optional component. For further reading and examples, see Adam Langley's [blog](https://www.imperialviolet.org/2015/05/16/aeads.html) on the topic

1. IND-CCA2 (下章)
2. IND-CCA3
   > [Shrimpton](https://eprint.iacr.org/2004/272.pdf) 2004 年提出来的，解密语言机只能返回无效符号$\bot$，而不是错误的明文。这个模型更加接近现实，因为在现实中，解密器不会告诉你明文是错误的，而是会告诉你解密失败了。就跟在 AE 中一样，完整性和机密性是分开了的。
3. CCM
   > a combination of a blockcipher in **C**ounter mode with **C**BC-MAC with the **M**AC-then-Encrypt approach。由于需要提前知道信息长度，所以不适用于online，且需要调用两次分组密码，所以在效率上会逊色一些。
4. GCM
   > uses Encrypt-then-**M**AC with a blockcipher in **C**ounter mode and a polynomial-based hash function called **G**HASH. [Saarinen](http://eprint.iacr.org/2011/202) 指出，这个方法存在弱密钥。
5. [CAESAR](https://competitions.cr.yp.to/caesar.html)
    > Competition for Authenticated Encryption: Security, Applicability, and Robustness
    > [AE Zoo](https://aezoo.compute.dtu.dk/doku.php)

## [Number 28: What is the IND-CCA security definition for public key encryption?](https://bristolcrypto.blogspot.com/2015/04/52-things-number-28-what-is-ind-cca.html)

IND-CCA security : **Ind**istinguishable **C**hosen **C**iphertext **A**ttack

*model 1* : **find-then-guess** security game
> 敌手允许在第 3，4 步之前与之后访问加密与解密预言机，当然也有第 3,6 步

1. Generate the public and secret keys $(p_k,s_k)$. The adversary A has access to the public key $p_k$

2. Assign $b\leftarrow\{0,1\}$ privately

3. A is allowed to query the decryption oracle $Dec_{sk}$ and the encryption oracle $Enc_{pk}$

4. A then outputs a pair of messages $(m_0,m_1)$

5. We output the encryption $c=Enc_{pk}(m_b)$

6. The adversary is allowed to enquire for more encryptions or decryptions, as in step 3, but he is not allowed to ask for the decryption of $c$

7. A outputs $b'^′'\in\{0,1\}$. A wins if $b=b'$

我们说 the **advantage** of A is $Adv(A)=2∣Pr[A\ wins]−1/2∣$. A scheme is said to be IND-CCA secure if the said advantage is negligible.

*model 2* : **real-or-random** security game
> 上一章的 IND-CCA2 就是这个模型

不同点就是在 Step 5,  A 不会每次都乖乖加密 $m_b$，而是在 $b=0$ 的时候返回一个随机消息 $m'$ 的加密, A 必须得区分他是在 “real” 还是 “random” 的世界中， advantage 和安全性的定义是相似的。

这两个定义其实是等价的，对于模型 1 的攻击者 A，我们可以构造一个模型 2 的攻击者 B：
$$
Adv_{find-and-guess}(A)=2\cdot Adv_{real-and-random}(B)
$$

## [Number 29: What is the UF-CMA security definition for digital signatures?](https://bristolcrypto.blogspot.com/2015/04/52-things-number-29-what-is-uf-cma.html)

在之前的文章中我们介绍了 DSA, Schnorr and RSA-FDH（#16）签名算法的细节

现在我们来看看签名系统及其安全性。

1. 签名系统的定义
A signature scheme $S$ is a tuple of algorithms $(KG,Sign,VRFY)$ :
    - $KG$ is a randomised algorithm which outputs a secret key $sk$ and a public key $pk$.
    - $Sign$ is a (possibly) randomised algorithm which on input $sk$ and a message $m$ it outputs a signature $\sigma$
    - $VRFY$ is a deterministic (non-stateful) algorithm which takes in the public key $pk$, a message $m$ and a signature $\sigma$ and returns 1 if $\sigma$ is a signature on $m$ and 0 otherwise


