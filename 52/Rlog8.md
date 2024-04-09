# What did you learn？

> side-channel attack

## [Number 38: What is the difference between a covert channel and a side-channel?](https://bristolcrypto.blogspot.com/2015/06/52-things-number-38-what-is-difference.html)

隐蔽信道和侧通道是信息泄漏通道的两种类型。

### Covert Channel

1. 隐蔽信道使用的机制并非用于通信
   > 例如：可以尝试写入一个文件，根据锁定与否可以传达信息 “1” 或 “0”
2. 在一个隐蔽信道中，一个内部程序会泄露信息给另一个外部程序（例如特洛伊木马）[1]

### Side Channel

1. 测信道攻击（side-channel attack）也叫被动非侵入式攻击（passive non-invasive attacks），即只有可直接访问的接口才会被利用。至于设备则不会被永久改变，因此不会留下任何攻击的证据。
   > 侧信道攻击的基本思想是通过测量加密设备的执行时间、功耗或电磁场等来确定其密钥 [2]
2. 在物理侧信道攻击中，经常使用一些非常规的技术手段
   > 买通保安十分钟拔一次网线
3. 传统的侧信道攻击涉及差分功率分析（differential power analysis）和时序分析（timing analysis）
   > 所需的实验次数可能比数学密码分析所需的少得多 [1]
4. 在软件侧信道攻击中，受害者进程**无意中**承担了发送进程的角色，而监听（攻击者）进程则承担了接收进程的角色。如果受害进程正在使用密钥执行加密操作，则软件侧信道攻击允许监听进程获取将导致部分或全部密钥恢复的信息 [1]

> 就像想知道老师在不在办公室。隐蔽信道就是让别人给老师打个电话问一下，侧信道就是看看办公室的门是不是开着

[1] Wang, Zhenghong, and Ruby B. Lee. "Covert and side channels due to processor architecture." Computer Security Applications Conference, 2006. ACSAC'06. 22nd Annual. IEEE, 2006.
[2] Mangard, Stefan, Elisabeth Oswald, and Thomas Popp. Power analysis attacks: Revealing the secrets of smart cards. Vol. 31. Springer Science & Business Media, 2008.

## [Number 39: What is the difference between a side-channel attack and a fault attack?](https://bristolcrypto.blogspot.com/2015/07/52-things-number-39-what-is-difference.html)

Side-channel attacks (SCA)
> 可利用泄露 [timing](https://www.rambus.com/timing-attacks-on-implementations-of-diffie-hellman-rsa-dss-and-other-systems/), [power consumption](https://www.rambus.com/differential-power-analysis/), electromagnetic emanations, [acoustic noise](https://www.tau.ac.il/~tromer/acoustic/) etc.

Fault attacks (FA) 故障攻击，利用的则是错误计算的结果。这个错误可能是程序或者设计上的 bug (例如因特尔的 FDIV bug)，也可能是敌手直接干预（例如电源故障(power **glitch**)、时钟故障(clock glitch)、温度变化(temperature variation)、离子束注入(ion-beam injection)等）造成的。
> 《魔法学徒故障攻击指南》（['The Sorcerer’s Apprentice Guide to Fault Attacks'](https://eprint.iacr.org/2004/100.pdf)）你值得拥有

听起来确实有点抽象，一个是 computation leakage，一个是 erroneous computation。不如看点实在的例子，从以下三个子类：
> 这种分类仅代表作者意见

### Non-Invasive

*An attack is classed as non-invasive if the adversary has no physical contact with the target.*

**SCA:**
Timing attacks. 这是个有争议，因为它是最适合但也是入侵最浅的 SCA 向量
> Timing attacks are arguable both the most applicable and the least invasive SCA vector.

时间攻击可以[远程执行](https://crypto.stanford.edu/~dabo/papers/ssl-timing.pdf)，也是最容易被引入的。拿 OpenSSL 这种大型库来说，它可以兼容大量平台与一整套密码学套件。确保每个敏感计算都被编程进一个恒定时间，这个工作非常繁琐且艰难
> constant time，我理解为不管输入是什么，程序的执行时间都是一样的，即恒定的意思，这样就不会因为输入的不同而导致时间的差异，从而避免了时间攻击（当然这样很难）。而不是翻译为常数时间。

**FA:**
非侵入式故障攻击并不常见，因为它需要错误行为来触发，但是靠人家主动暴露错误就太难太被动了。就像前面提到过的 FDIV，拿这个构建攻击，可以，它将在每 90 亿个随机输入中返回一个错误的除法结果，相当不现实。但是，这不代表这种攻击不可能，比较也没有不可能的证据。

### Semi-Invasive

*An attack is classed as semi-invasive if the adversary has limited physical contact with the target.*

**SCA:**
功耗分析（power analysis），如果敌手能够将能耗与操作联系起来，那么就可以通过监控能耗来分析正在执行的操作。说是半侵入式的，因为攻击者需要对目标设备进行电源连接，而目标设备并不总是可用，因此攻击者需要修改目标。

**FA:**
时钟和电源故障攻击（clock and power glitch attacks），这种攻击是通过改变目标设备所处的目标环境从而引发错误行为。就比如一个芯片的时钟输入，时钟控制着目标设备的运行速度。一个设备的时钟不能太大，要留给电路时间来稳定，也就是目标必须遵循一个“关键路径”（'critical path'）。一旦突破这个限制，就可以引发设备内部的竞争，会产生未定义行为，这种攻击非常[高效](http://www.eurasia.nu/wiki/index.php/Xbox_360_Reset_Glitch_Hack)
> 不过这种攻击造成的后果也是不可预测的，所以很难复刻

### Invasive

*An attack is classed as invasive if the adversary has unlimited resources and access the target.*

**SCA:**
探测型（Probing）的 SCAs 直接连接目标设备的数据总线（data bus），允许攻击者几乎直接通过总线读取任何信息。必须对目标进行完全解封装并仔细检查，以精确定位秘密数据。
> Probing SCAs use a direct tap on the data bus
> 这儿的tap最好不要翻译为“水龙头”或者“轻拍”，而是“利用”，”接触“，”窃听“等意思

**FA:**
探测型（Probing）的 FAs  允许攻击者完全改变目标设备的行为。再次强调，目标必须完全解封装并绘制出来，以准确影响行为，而一旦完成，对手就有能力重新连接目标，从而改变其操作。

总结：SCA 和 FA 都已在现实设备上被证明具有毁灭性的效果。当然，我们设计了几种对策来减轻这些攻击，这就是后续的话题了。

## [Number 40: What is normally considered the difference between SPA and DPA?](https://bristolcrypto.blogspot.com/2015/07/52-things-number-40-what-is-normally.html)

电磁(Electronmagnetic, EM)功率分析攻击被划分成两种类型的攻击，简单功率分析(SPA)或者差分功率分析(DPA)。这两种攻击要么使用电磁要么使用能量记录设备，但是它们在分析能量数据的数量和方法上有本质的不同。

在检查这些攻击的不同之处之前值得说明的是power/EM攻击是什么。
