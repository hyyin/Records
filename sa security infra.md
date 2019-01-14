# infra

用docave componet

SA side:

随机生成一个key，用来加密数据，用master key加密此key，master key可配置，配置文件也加密，可以提供一个tool，供部署人员设置master key。

AES 256 算法，加密需要加密的数据，想想如何将加密的过程尽量透明化 -- 改造entity framework

非对称加密，ECC算法，

Apeg 每一个response是一个sql lite，sql lite数据冗余一份，用apeg的加密key加密，另一份用 证书公钥加密。

确保SA系统用证书私钥，可以解密所有sqllite db.

Apeg 只能用C++，平台有windows，mac等


[加密算法比较](https://www.cnblogs.com/sunxuchu/p/5483956.html)

apeg实例的passphrase是不同的，

ECDH

ECDSA

ECIES

KDF 秘钥导出函数


https://www.codeproject.com/Tips/1071190/Encryption-and-Decryption-of-Data-using-Elliptic-C


https://stackoverflow.com/questions/10264770/creating-an-ecc-private-public-key-with-native-c-sharp

http://www.bouncycastle.org/csharp/

https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.ecdiffiehellmancng?view=netframework-4.7.2

response 要用ecc签名

==============================================================================================

一个具体的RSA签名过程如下：


  
  小明对外发布公钥，并声明对应的私钥在自己手上
  小明对消息M计算摘要，得到摘要D
  小明使用私钥对D进行签名，得到签名S
  将M和S一起发送出去
  


验证过程如下：


  
  接收者首先对M使用跟小明一样的摘要算法计算摘要，得到D
  使用小明公钥对S进行解签，得到D’
  如果D和D’相同，那么证明M确实是小明发出的，并且没有被篡改过

---------------------

本文来自 qmickecs 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/qmickecs/article/details/73696954?utm_source=copy 


===========

https://blog.csdn.net/sszgg2006/article/details/41945163

ECC理解

https://blog.csdn.net/mrpre/article/details/72850644

ECDSA理解

=============================================================================

https://www.cryptopp.com/wiki/Main_Page

跨平台库

https://blog.csdn.net/livelylittlefish/article/details/6095294

bsl 1.0 license

Boost的发布采用Boost Software License，这是一个不同于GPL、Apache的非常宽松的许可证，允许库用户将Boost用于任何用途，包括商业用途和非商业用途。用户无须支付任何费用，即可享有Boost的全部功能。

==========================

https://www.cryptopp.com/wiki/Elliptic_Curve_Integrated_Encryption_Scheme#Android_Pay_Example

====================================================================================================

c# 调用 c++

https://www.cryptopp.com/wiki/Wrapper_DLL

extern "C" _declspec(dllexport) int add(int a, int b)
{
	return a + b;
}

extern "C" 结果是方法名不变
用dumpbin 确认函数是否导出

https://blog.csdn.net/qq_33414271/article/details/79534763

注意 x86 x64 平台问题


==============================================

各种奇葩问题，注意 头文件顺序

https://blog.csdn.net/wangweitingaabbcc/article/details/7663949  靠谱一点的字符串传递方案

https://blog.csdn.net/xuedingkai/article/details/53396840

https://www.cnblogs.com/lanzhi/p/6469898.html 大神方案！解决了 字符串不定长的问题

坑爹啊，用sbyte传值！

int 传递形式： c++端 int &  c#端 ref int

https://stackoverflow.com/questions/14633338/how-do-i-return-a-byte-array-from-c-to-c-sharp

根源是 char*  = sbyte

https://ask.csdn.net/questions/685716 32位 64位 加载问题

https://blog.csdn.net/yuquan0405/article/details/45844035 解决方案

https://blog.csdn.net/g710710/article/details/23161807 x86 x64 any cpu 区别



		StringSource Prias(PriKeybuffer, privateKeyLength, true);
		StringSource Pubas(PbuKeybuffer, pubKeyLength, true);

    和等于的意义是不相同的。。。。

    我擦


============================================
诡异的时不时 actualsize ！= 计算size的问题


// them when calling one from the CRT. This is necessary because free
// needs to support users patching in custom implementations.
extern "C" void __declspec(noinline) __cdecl _free_base(void* const block)
{
    if (block == nullptr)
    {
        return;
    }

    if (!HeapFree(select_heap(block), 0, block))
    {
        errno = __acrt_errno_from_os_error(GetLastError());
    }
}

这又是什么鬼

感觉是析构函数出了问题

原来是 api里 delete了指针，不能传栈变量。。。


ECDSA: 实例：https://blog.csdn.net/u011280717/article/details/79689205

