# What did you learn？

## [Number 15: Key generation, encryption and decryption algorithms for RSA-OAEP and ECIES.](https://bristolcrypto.blogspot.com/2015/01/key-generation-encryption-and.html)

### 1. RSA-OAEP

#### 1.1 RSA

略

#### 1.2 OAEP

Optimal Asymmetric Encryption Padding
它是与非对称加密（通常是 RSA）一起使用的填充方案。它可以给确定性加密方案带来一些随机性。当与 RSA 一起使用时，组合方案被证明是 IND-CCA 安全的。

令

- $f$ 是一个 $k$ 比特的陷门单向置换（trapdoor one-way permutation）：$f:\{0,1\}^k \rightarrow \{0,1\}^k$
- $m$ 是一个 $n$ 比特的消息
- $G,H$ 是两个伪随机函数，其中 $G:\{0,1\}^s \rightarrow \{0,1\}^{n+t},H:\{0,1\}^{n+t} \rightarrow \{0,1\}^s,\ where\ k=n+t+s$
- $R$ 是一个 $s$ 比特的随机数: $R \overset{\$}{\leftarrow} \{0,1\}^s$

**Encryption:**
计算 $k$ 比特密文的过程如下：
$$
E(m) = f_{pk}(\{(m||0^t) \oplus G(R)\} || \{R \oplus H((m||0^t)\oplus G(R)) \})
$$

**Decryption:**
通过陷门解密：
$$
D(c) = f_{sk}(c) = \{(m||0^t) \oplus G(R)\} || \{R \oplus H((m||0^t)\oplus G(R)) \}
$$

然后

1. 令前 $n+t$个比特为 $T:T=(m||0^t) \oplus G(R)$，剩下的 $s$ 比特为 $S:S=R \oplus H((m||0^t)\oplus G(R))$
2. $R$ 可以根据 $R=S\oplus H(T)$ 计算出来
3. 接着计算 $m||0^t=T\oplus G(R)$
4. 可以通过 $n$ 位消息 $m$ 后面是否正好有 $t$ 个 0 来验证有效性。如果有效，则删除前 $t$ 位并输出 $m$。

在实际应用中，我们分别用 RSA 加密和解密函数来代替 $f_{pk}$ 和 $f_{sk}$。

### 2. ECIES

Elliptic Curve Integrated Encryption Scheme
> 是 ElGamal 加密方案在椭圆曲线上的一种变体

#### 2.1 Elliptic Curve

定义在素数域 $F_q$，选择一个点 $P$ 并拥有素数阶 $n$
略（看NO.12）

#### 2.2 ECIES

ECIES 经常与一个对称加密方案和一个 MAC 方案一起使用。

- symmetric encryption scheme : $Enc_k(m)=c,Dec(c)=m$
- MAC scheme : $MAC_k(m)=t,Ver(t,m)=T/F$
- Key Derivation Function : $KDF(s_1,s_2)=(k_{enc},k_{MAC})$，其中 $s_1,s_2$ 是俩种子

**Key Generation：**

1. 选择一个随机整数 $d \in [1,n-1]$
2. 计算一个新的点 $Q=dP$
3. 公钥是 $Q$，私钥是 $d$

**Encryption:**

1. 选择一个随机整数 $k \in [1,n-1]$
2. 计算 $R=kP,z=kQ$，$Z$ 不能是 $\infty$
3. 计算 $(k_1,k_2)=KDF(x_Z,R)$，其中 $x_Z$ 是 $Z$ 的 $x$ 坐标 
4. 计算 $c=Enc_{k_1}(m)$，$t=MAC_{k_2}(c)$
5. 输出密文 $(R,c,t)$

**Decryption:**

1. 验证 $R$ 是否有效。通过将 $R$ 代入曲线中可以轻松完成此操作。
2. 计算 $Z'=dR$
3. 计算 $(k'_1,k'_2)=KDF(x_{Z'},R)$，其中 $x_{Z'}$ 是 $Z'$ 的 $x$ 坐标
4. 验证 $Very(t,c)$
5. 解密 $m'=Dec_{k'_1}(c)$
6. 输出明文 $m'$

正确性：$Z'=dR=d(kP)=k(dP)=kQ=Z$

## [Number 16: Describe the key generation, signature and verification algorithms for DSA, Schnorr and RSA-FDH.](https://bristolcrypto.blogspot.com/2015/01/52-things-number-15-describe-key.html)


