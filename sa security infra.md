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

ECSPA

KDF


https://www.codeproject.com/Tips/1071190/Encryption-and-Decryption-of-Data-using-Elliptic-C


https://stackoverflow.com/questions/10264770/creating-an-ecc-private-public-key-with-native-c-sharp

http://www.bouncycastle.org/csharp/

https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.ecdiffiehellmancng?view=netframework-4.7.2

response 要用ecc签名




