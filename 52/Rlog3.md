# What did you learn？

## [Number 9: What are Shannon's definitions of entropy and information?](https://bristolcrypto.blogspot.com/2014/12/52-things-number-9-what-are-shannons_7.html)

[信息论](https://en.wikipedia.org/wiki/Information_theory)是由香农在1948为了信号处理提出来的，本章主要介绍其中两个重要概念：**熵**（entropy）和**信息**（information）。

### 1. 熵

[熵](http://en.wikipedia.org/wiki/Entropy_%28information_theory%29)是一种评估一个或多个变量**不确定性**的度量。
> 举个例子：一个原批的发言记录大概率是“原神启动”或者“原神怎么你了”，不确定性低，熵小；而一个随机的发言记录，不确定性高，熵大。

香农熵（[Shannon's Entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)#Definition)）的定义如下：
$$
H = -\sum_{i} p_i \log_b p_i
$$
其中，$p_i$是第$i$个消息出现的概率，在计算机科学中，一般取$b=2$

假如现在 4 个原批，4个正常人，那么熵为：
$$
H_{原批} = -\sum_{i=1}^4 1 \log_2 1 = 0\\
H_{正常人} = -\sum_{i=1}^4 \frac{1}{4} \log_2 \frac{1}{4} = 2
$$
这个结果也符合我们的直觉：原批的熵小，正常人的熵大。

### 2. 信息

1950年提出的[信息](https://en.wikipedia.org/wiki/Information)定义如下：
" Information is a measure of one's freedom of choice when one selects a message."
> “当一个人选择一条消息时，信息是衡量一个人选择自由度的标准。”

举个例子，还是4个原批4个正常人，如果给定一个回答——“甘雨的“履虫”效果是施放山泽麟迹后30秒内的第一次霜华矢，无需蓄力即可施放。”
那我们基本可以判断这个回答来自原批，相反，如果是其它知识点，那么我们就难以判断了。
因此我们可以说原神的包含了更多的信息（低自由度），随机回答则包含更少的信息（高自由度）。

那么信息和熵的关系是啥？
我们扩展熵的定义，给出[条件熵](https://en.wikipedia.org/wiki/Conditional_entropy)（Conditional Entropy）的定义：
$$
H(Y|X) = \sum_{x\in X} p(x) H(Y|X=x)
$$
熵是变量的不确定性，因此，条件熵的含义实际上是：给定“线索(clue)”（条件）$X$ 时 $Y$ 的不确定性。

当$X$只包含$Y$的一点信息时，给了$X$仍然很难确定$Y$，条件熵很大，即“**$X$并没有显著降低$Y$的不确定性**”；反之，如果$X$包含$Y$的基本信息，那么当给定$X$时$Y$的熵预计会很低。因此，条件熵可以被视为对**X所拥有的Y信息**的理性测量！

另一个重要测量标准被称为[互信息](https://en.wikipedia.org/wiki/Mutual_information)（Mutual Information），它是两个变量之间相互依赖性的度量。定义它的一种方法是给定条件时的熵（不确定性）损失：
$$
I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X)
$$

### 3. 密码学例子

信息论的概念广泛应用于密码学中。一个典型的例子是将密码过程视为一个通道（channel），明文和密文分别作为输入和输出。
> 因此测信道分析（side channel analysis）得益于信息论的使用。

## [Number 10: What is the difference between the RSA and strong-RSA problem?](https://bristolcrypto.blogspot.com/2014/12/52-things-number-10-what-is-difference.html)

### 1. RSA问题

$$
N = pq, \quad \phi(N) = (p-1)(q-1)\\
e, d \quad s.t. \quad ed \equiv 1 \mod \phi(N)\\
\text{公钥} = (N, e), \quad \text{私钥} = (N, d)\\
C = m^e \mod N, \quad M = c^d \mod N
$$
对手可以窃听 $C$ 并且可以知道公钥 $(n,e)$，但是要计算 $M$，对手必须找到 $n$ 的因子。如果选择了合适的 $n$，这会是一个非常难解决的问题。

### 2. Strong-RSA问题

强 RSA 假设与 RSA 假设的不同之处在于，对手可以选择（奇数）公共指数 $e\geq 3$，对手的任务是在给定密文$C = M^e \mod N$的情况下计算明文 $M$，
> 这个假设用脚想都知道解起来肯定比一般的RSA简单，所以这个问题被称为“强RSA问题”。

## [Number 11: What are the DLP, CDH and DDH problems?](https://bristolcrypto.blogspot.com/2014/12/52-things-number-11-what-are-dlp-cdh.html)

### 1. The Discrete Logarithm Problem (DLP)

令 $G$ 是一个Abelian群，$g$ 是 $G$ 的生成元，$h$ 是 $G$ 中的一个元素。DLP 问题是找到一个整数 $x$ 使得 $g^x = h$。
> $x$ is called the discrete logarithm of $h$ with base $g$

### 2. The Computational Diffie-Hellman Problem (CDH)

### 3. The Decisional Diffie-Hellman Problem (DDH)
