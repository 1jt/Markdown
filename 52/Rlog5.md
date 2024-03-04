# What did you learn？

## [Number 21: How does the CRT method improve performance of RSA?](https://bristolcrypto.blogspot.com/2015/02/52-things-number-21-how-does-crt-method.html)

**The Chinese Remainder Theorem (CRT) 中国剩余定理：**
当有俩等式 $x\equiv a\ (mod\ M),x\equiv b\ (mod\ N)$ 时，如果 $M,N$ 互质，那么可以通过 CRT 计算出 $x$ 的唯一解。

**一些题外话：**
RSA方案中的主要运算是模幂( modular exponentiation )$M=C^d(mod\ N)$。一次模幂云散在改进的状态下，可以使用 $(h - 1)$ 次乘法和 $(t - 1)$ 次平方操作（$t$ 是指数的位长度，$h$ 是汉明权重）。乘法和平方平均次数为 $t+t/2−1$。
进一步改进：我们可以使用 binary exponentiation algorithms 或者 window methods。对于后者，我们一次处理 $w$ 位指数，这种方法，我们仍然需要 $t$ 次平方，但乘法次数平均减少到 $t/w$。通过采用滑动窗口方法，乘法次数可以降到平均 $t/(w + 1)$ 次。

**开始正题：**
CRT 用于 RSA 解密的情况。因此，我们正在考虑私钥操作，这意味着我们可以访问私钥，从而可以访问模数 $N=pq$ 的因式分解。如果我们假设我们想要解密一条消息，那么我们的目标是计算 $M=C^d(mod\ N)$。
首先我们计算：
$$
M_p=C^d(mod\ p)=C^{d(mod\ p-1)}(mod\ p)\\
M_q=C^d(mod\ q)=C^{d(mod\ q-1)}(mod\ q)
$$
此计算需要对 512 位取模和 512 位指数求幂，因为 $p$ 和 $q$ 是 512 位。这比用 1024 位数字进行单次取模求幂要快。

使用 CRT 可以根据 $M_p,M_q$ 计算出 $M$：
$$
M=M_p+p\cdot(p^{-1}\ mod\ q)\cdot(M_q-M_p)\ (mod\ N)
$$
另一种表示方法：
$$
T = p^{-1}\ mod\ q\qquad 作为私钥\\
U = (M_q-M_p)T\ mod\ q\\
M = M_p+U\cdot p
$$
p.s.：$q^{-1}\ mod\ p\cdot q+p^{-1}\ mod\ q\cdot p=1\ mod \ N$

## [Number 22: How do you represent a number and multiply numbers in Montgomery arithmetic?](https://bristolcrypto.blogspot.com/2015/03/52-things-number-22-how-do-you.html)

这个连问题都看不懂了属于是

[Montgomery](https://blog.csdn.net/bjarnecpp/article/details/77644958)






