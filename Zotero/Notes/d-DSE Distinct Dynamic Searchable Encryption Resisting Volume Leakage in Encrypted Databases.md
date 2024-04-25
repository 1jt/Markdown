***
#### Metadata
- 作者::* Authors: [[Dongli Liu]], [[Wei Wang]], [[Peng Xu]], [[Laurence T. Yang]], [[Bo Luo]], [[Kaitai Liang]]
- 作者机构:: 
- 日期::* Date: [[2024-03-02]]
- 出处:: 
- 标签:: * Tags: #Computer-Science---Cryptography-and-Security
- 备注:: 

***
## Abstract

Dynamic Searchable Encryption (DSE) has emerged as a solution to efficiently handle and protect large-scale data storage in encrypted databases (EDBs). Volume leakage poses a significant threat, as it enables adversaries to reconstruct search queries and potentially compromise the security and privacy of data. Padding strategies are common countermeasures for the leakage, but they significantly increase storage and communication costs. In this work, we develop a new perspective to handle volume leakage. We start with distinct search and further explore a new concept called distinct DSE (d-DSE).
We also define new security notions, in particular Distinct with Volume-Hiding security, as well as forward and backward privacy, for the new concept. Based on d-DSE, we construct the d-DSE designed EDB with related constructions for distinct keyword (d-KW-dDSE), keyword (KW-dDSE), and join queries (JOIN-dDSE) and update queries in encrypted databases. We instantiate a concrete scheme BF-SRE, employing Symmetric Revocable Encryption. We conduct extensive experiments on real-world datasets, such as Crime, Wikipedia, and Enron, for performance evaluation. The results demonstrate that our scheme is practical in data search and with comparable computational performance to the SOTA DSE scheme (MITRA*, AURA) and padding strategies (SEAL, ShieldDB). Furthermore, our proposal sharply reduces the communication cost as compared to padding strategies, with roughly 6.36 to 53.14x advantage for search queries.

---
## Summary

## Experimental

## Results and discussions

## Zotero links

- zotero::* [Local library](zotero://select/items/1_SWIT5MX5)

- pdf::* PDF Attachments
	- [Liu 等 - 2024 - d-DSE Distinct Dynamic Search[[]]ab[]()le Encryption Resisting Volume Leakage in Encrypted Databases.pdf](zotero://open-pdf/library/items/YGJEXCYP)

- URL:: * URL: [http://arxiv.org/abs/2403.01182](http://arxiv.org/abs/2403.01182)

- citekey:: * Citation Key: [[liuDDSEDistinctDynamic2024]]