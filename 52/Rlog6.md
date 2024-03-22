# What did you learn？

> Security Definitions and Proofs

## [Number 27: What is the AEAD security definition for symmetric key encryption?](https://bristolcrypto.blogspot.com/2015/04/52-things-number-27-what-is-aead.html)

前面（#18）介绍的分组密码的各种模式，本质上是为了机密性（confidentiality）服务的，现实情况中，我们还需要保证完整性（integrity）和认证性（authenticity）。
> **AE** 指的就是 **Authenticated Encryption**，认证加密

为了达到这些目的，引入一个叫做 message authentication code （MAC）的东西，经典的实现方法是利用哈希函数（HMAC）。但是加密和认证这两个原语不能随随便便地组合在一起。为了达到 IND-CCA 安全性，








