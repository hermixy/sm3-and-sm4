# 国密公开算法sm3/sm4

* 强调！本实现没有经过详尽的测试与安全实现的考虑，只用于加深对算法的理解。
* 注意！本实现当前存在实现错误，任何在54-63字节的输入均无法得到预期的输出。
* Emphasize! This implementation does not go through a detailed test and safety considerations, only to deepen the * understanding of the algorithm.
* Note! Currently there is an implementation mistake in padding process, and any input of 54-63 bytes can not get the expected output.

【标准 c 】写成，适应所有平台，包括 32bit 和 64bit。算法文档详见国家密码管理局网站。

* 本实现试图还原官方文档的流程，忠实地对每一个步骤做出了划分，故实际应用中还有优化的余地。

* 本实现内部不做任何参数检查，为避免可能造成的溢出，请熟知下述说明。另所有的空间分配均在栈上完成，小机器注目。

# 关于 sm3

* 鉴于在下机器限制，sm3 算法无法对最大 2^64bit 长度的消息进行测试，放弃支持，对应的位置直接使用对应的数据结构，故本代码的sm3为残缺版，请注意！（官方文档指出最大可以支持 2^64bit 长度）

* 附带基于 sm3 的 HMAC 实现。

* 要应用源文件 sm3.c，只需声明外部函数 sm3 即可。—— 参数说明：（左起）待摘要消息、待摘要消息的长度（单位为字节）、存放摘要的空间（32 字节限定）。无返回。

* 要应用源文件 sm3_hmac，只需声明外部函数 sm3_hmac，且需要 sm3.c。—— 参数说明：（左起）待摘要的消息、待摘要消息的长度（单位为字节）、密钥（16 字节限定）、存放摘要的空间（32 字节限定）。无返回。

# 关于 sm4

* 没有复杂的分组密码模式的实现，接口仅仅为普通的电码本（ECB）模式，要使用请注意安全性问题。

* 要应用源文件 sm4.c，只需引用头文件 sm4.h 并 声明外部函数 sm4 即可。—— 参数说明：（左起）加解密模式（枚举，见头文件）、待加/解密消息长度（单位为字节）、16 字节密钥、待加/解密消息、存放加/解密结果的空间（不小于待加/解密消息长度，且为 16 的倍数，单位为字节）。返回字符串，人可读，解释此次处理的结果。

# ！注意

1) 重申，本实现没有经过优化、详尽的测试、安全性的完善。实现目的仅为帮助理解两种算法的流程以及为其他实现提供参照。

2) 虽然本实现没有许可证，但提醒诸君避免用于违反任何相关规定的行为，具体解释详见国家密码管理局网站。

3) 欢迎指出各种问题，其实这是我初学代码时的练习…… 本文件中指出的所有问题实际上均由于在下的年轻无知，但鉴于“往事不可追”，加上此种算法不知里面怎么样，于是不专门进行改进调整。如若诸君有所不满，尽情分支自己修改。对于提出的问题，我尽量解决（其实应该都不麻烦）。



期待下一次的见面。
