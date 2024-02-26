# What did you learn？

## [Number 9: What are Shannon's definitions of entropy and information?](https://bristolcrypto.blogspot.com/2014/12/52-things-number-9-what-are-shannons_7.html)

[信息论](https://en.wikipedia.org/wiki/Information_theory)是由香农在1948为了信号处理提出来的，本章主要介绍其中两个重要概念：**熵**（entropy）和**信息**（information）。

### 1. 熵

[熵](http://en.wikipedia.org/wiki/Entropy_%28information_theory%29)是一种评估一个或多个变量**不确定性**的度量。
> 举个例子：一个原批的发言记录大概率是“原神启动”或者“原神怎么你了”，不确定性低，熵小；而一个随机的发言记录，不确定性高，熵大。

香农熵（[Shannon's Entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)#Definition)）的定义如下：
$$
H(X) = -\sum_{i=1}^{n} p(x_i) \log_2 p(x_i)
$$
其中，$H(X)$是随机变量$X$的熵，$p(x_i)$是$X$的第$i$个取值的概率。
