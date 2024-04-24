***
#### Metadata
- 作者::* Authors: [[Ashrujit Ghoshal]], [[Mingxun Zhou]], [[Elaine Shi]]
- 作者机构:: 
- 日期::- 出处:: 
- 标签:: * Tags: #✅
- 备注:: 
***
## Abstract

Classically, Private Information Retrieval (PIR) was studied in a setting without any preprocessing. In this setting, it is well-known that 1) public-key cryptography is necessary to achieve non-trivial (i.e., sublinear) communication efficiency in the single-server setting, and 2) the total server computation per query must be linear in the size of the database, no matter in the single-server or multi-server setting. Recent works have shown that both of these barriers can be overcome if we are willing to introduce a pre-processing phase. In particular, a recent work called Piano showed that using only one-way functions, one can construct a single-server preprocessing PIR with  $\widetilde{O}(\sqrt{n})$  bandwidth and computation per query, assuming $\widetilde{O}(\sqrt{n})$  client storage. For the two-server setting, the state-of-the-art is defined by two incomparable results. First, Piano immediately implies a scheme in the two-server setting with the same performance bounds as stated above. Moreover, Beimel et al. showed a two-server scheme with $O(n^{1/3})$ bandwidth and $O(n/ \log^2 n)$ computation per query, and one with $O(n^{1/2+\epsilon })$  cost both in bandwidth and computation — both schemes provide information theoretic security. 
In this paper, we show that assuming the existence of one-way functions, we can construct a two-server preprocessing PIR scheme with $\widetilde{O}(n^{1/4})$  bandwidth and $\widetilde{O}(n^{1/2})$ computation per query, while requiring only $\widetilde{O}(n^{1/2})$ client storage. We also construct a new single-server preprocessing PIR scheme with $\widetilde{O}(n^{1/4})$ online bandwidth and $\widetilde{O}(n^{1/2})$ offline bandwidth and computation per query, also requiring $\widetilde{O}(n^{1/2})$ client storage. Specifically, the online bandwidth is the bandwidth required for the client to obtain an answer, and the offline bandwidth can be viewed as background maintenance work amortized to each query. Our new constructions not only advance the theoretical understanding of preprocessing PIR, but are also concretely efficient because the only cryptography needed is pseudorandom functions.

## Summary

### PIR 的目标
A client with small local storage wants to query the database, while **hiding its queries** from the server
### PIR 的应用
- 私人联络发现（private contact discovery）
- 隐私保护的加密货币轻量级客户端（privacy-preserving light-weight clients for cryptocurrencies）
- 私人 DNS 查询（private DNS queries）
- 私人网页查询（private web search）

### 如果没有预处理

1. 最简单的方法就是线性扫描整个数据库，注意，必须全部扫描，不然没有扫到的地方服务器就会知道搜索绝对和这部分没有关系
2. 在单服务器模型中，经常使用多种密码学假设（e.g., $\Phi$-hiding, LWE, Damgard-Jurik, DDH, QR）,并且可以达到 $\widetilde{O}_{\lambda}(1)$ 的带宽（这些假设应该都是用于构建非对称的原语）
	> $\widetilde{O}_{\lambda}(\cdot)$ 是指隐藏了多对数因子以及对安全参数 $\lambda$ 的依赖性。
3. 在双服务器中模型中，Dvir and Gopi \[23\] 指出，PIR 从信息论的角度看每次查询的带宽**可能是** $n^{O(\sqrt{\log\log n/\log n})}$
4. 所以可以总结出如果没有预处理操作的话，会有两个方面的固有限制：
	1.  任何没有预处理的经典 PIR 的服务器**计算量**一定与 $n$ 是线性相关的。直观点说，如果服务器在查询过程中没有查看某个位置，那客户端必然不可能询问该位置    \[5\]
	2.  在单服务器设置下，如果想达到非线性的带宽，就意味着不经意传输（\[21\]），即需要某种形式的公钥加密

### 如果有预处理

1. 在预处理模型中，探索重点为亚线性计算和不使用公钥加密下的 PIR 效率
2. 预处理分为两种方式：
	1. 全局（global, server-side）：
		- Beimel et al. \[5\] : $O(n^{1/3})$ 带宽, $O(n/ \log^2 n)$ 计算, while consuming $O(n^2)$ server storage；还展示了一种无法比拟的信息论方案，$O(n^{1/2+\epsilon})$ 计算与带宽，$n^{1+\epsilon'}$ 服务器存储
	2. 客户端（client-specific ）：
		- 著名方案 PIANO，后续工作 Mughees et al. \[45\]：$\widetilde{O}(\sqrt{n})$ 带宽，$\widetilde{O}_{\lambda}(\sqrt{n})$ 服务器计算，
## Experimental

## Results and discussions

## Zotero links

- zotero::* [Local library](zotero://select/items/1_AIPMB9LG)

- pdf::* PDF Attachments
	- [Ghoshal et al_Eﬃcient Pre-processing PIR Without Public-Key Cryptography.pdf](zotero://open-pdf/library/items/AP4IN6DB)

- DOI::
- citekey::