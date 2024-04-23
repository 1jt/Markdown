***
#### Metadata
- 作者::* Authors: [[Ashrujit Ghoshal]], [[Mingxun Zhou]], [[Elaine Shi]]
- 作者机构:: 
- 日期::- 出处:: 
- 标签:: * Tags: #✅
- 备注:: 
***
## Abstract

Classically, Private Information Retrieval (PIR) was studied in a setting without any preprocessing. In this setting, it is well-known that 1) public-key cryptography is necessary to achieve non-trivial (i.e., sublinear) communication efficiency in the single-server setting, and 2) the total server computation per query must be linear in the size of the database, no matter in the single-server or multi-server setting. Recent works have shown that both of these barriers can be overcome if we are willing to introduce a pre-processing phase. In particular, a recent work called Piano showed that using only one-way functions, one can construct a single-server preprocessing PIR with  ̃ O(√n) bandwidth and computation per query, assuming  ̃ O(√n) client storage. For the two-server setting, the state-of-the-art is defined by two incomparable results. First, Piano immediately implies a scheme in the two-server setting with the same performance bounds as stated above. Moreover, Beimel et al. showed a two-server scheme with O(n1/3) bandwidth and O(n/ log2 n) computation per query, and one with O(n1/2+ ) cost both in bandwidth and computation — both schemes provide information theoretic security. In this paper, we show that assuming the existence of one-way functions, we can construct a two-server preprocessing PIR scheme with  ̃ O(n1/4) bandwidth and  ̃ O(n1/2) computation per query, while requiring only  ̃ O(n1/2) client storage. We also construct a new single-server preprocessing PIR scheme with  ̃ O(n1/4) online bandwidth and  ̃ O(n1/2) offline bandwidth and computation per query, also requiring  ̃ O(n1/2) client storage. Specifically, the online bandwidth is the bandwidth required for the client to obtain an answer, and the offline bandwidth can be viewed as background maintenance work amortized to each query. Our new constructions not only advance the theoretical understanding of preprocessing PIR, but are also concretely efficient because the only cryptography needed is pseudorandom functions.

## Inroduction

## Experimental

## Results and discussions

## Zotero links

- zotero::* [Local library](zotero://select/items/1_AIPMB9LG)

- pdf::* PDF Attachments
	- [Ghoshal et al_Eﬃcient Pre-processing PIR Without Public-Key Cryptography.pdf](zotero://open-pdf/library/items/AP4IN6DB)

- DOI::
- citekey::