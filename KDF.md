https://blog.csdn.net/sihai12345/article/details/79313574 如何生成安全的密码 Hash：MD5, SHA, PBKDF2, BCrypt 示例


https://crypto.stackexchange.com/questions/1842/how-does-pbkdf1-work

7
down vote
accepted
PBKDF1 as specified in PKCS#5 and RFC 2898 provides Key Derivation and Key Strengthening. The parameters of the function are a hash function (such as SHA-1), a password, a salt (sometimes called nonce, depending on context), an iteration count and the length of the derived key to be returned. The standard PBKDF1 will just calculate the hash of password concatenated with salt, and then hash the hash value that is returned by the previous step iteration count minus one times:

K=H(H(...H(P||S)...))
If you only need key derivation but not key strengthening, use an iteration count of one. The purpose of the key strengthening is to increase the complexity of the key derivation, making certain attacks that exploit weak passwords more time consuming.

There are related key derivation functions that also provide Key Stretching, such as PBKDF2 and the .NET PasswordDeriveBytes function. Key Stretching is a feature that allows derived keys of any length to be returned, instead of being limited by the output length of the hash function.


PBKDF1 定长
PBKDF2 变长
bcrypt 更安全


https://www.cryptopp.com/wiki/Key_Derivation_Function 
Key Derivation Function

https://www.cryptopp.com/docs/ref/class_p_k_c_s5___p_b_k_d_f2___h_m_a_c.html#details


https://crypto.stackexchange.com/questions/62807/why-do-some-key-derivation-functions-like-pbkdf2-use-a-salt

why-do-some-key-derivation-functions-like-pbkdf2-use-a-salt







