---
title: 'mcrypt使用[PHP]'
tags:
  - php
url: 118.html
id: 118
categories:
  - 'NULL'
date: 2008-02-27 14:22:00
---

  

要使用本函数库要先准备 mcrypt 程序，可以到 [ftp://argeas.cs-net.gr/pub/unix/mcrypt](ftp://argeas.cs-net.gr/pub/unix/mcrypt) 下载这个程序 libmcrypt-x.x.tar.gz。同时在编译 php 程序时需要加入 --with-mcrypt 的选项，俾使本函数库能顺利运作。  
本函数提供的编码方式有 des、tripledes、blowfish (默认值)、3-way、safer-sk64、safer-sk128、twofish、tea、rc2 及使用 cbc, ofb, cfb, ecb 作为密码检索的 gost。此外还有 rc6 及 idea 等非免费的编码方式。  
见下面列示为已定义的密码：

  
mcrypt_blowfish  
mcrypt_des  
mcrypt_tripledes  
mcrypt_threeway  
mcrypt_gost  
mcrypt_crypt  
mcrypt\_des\_compat  
mcrypt_safer64  
mcrypt_safer128  
mcrypt_cast128  
mcrypt_tean  
mcrypt_rc2  
mcrypt_twofish (mcrypt 2.x 前的版本用)  
mcrypt_twofish128 (mcrypt 2.x 后的版本用)  
mcrypt_twofish192  
mcrypt_twofish256  
mcrypt_rc6  
mcrypt_idea  
在密码检索本 (cipher) 方面，本函库支持 cbc、ofb、cfb 与 ecb 四种密码检索本。这四种密码检索本的简单叙述如下，更详细的信息请参考 schneier 所着作的 applied cryptography (isbn: 0-471-11709-9)：

  
ecb (electronic codebook): 适合随机的资料，例如使用另外的密钥。若资料量少且随机时，使用 ecb 较不适合。  
cbc (cipher block chaining): 适合文件的加密，安全性较 ecb 好。  
cfb (cipher feedback): 适合对位组资料流中的某段独立位组资料 (single bytes) 加密。  
ofb (output feedback): 与 cfb 相容，尤其适合在无法忍受错误波及的应用上。  
目前 php 仍无法对单位 (bit) 的熵值做加密解密的步骤，目前只适合对字符串作密码处理。

在使用 cfb 及 ofb 二种模式时，必须要向量初始化 (initialization vector, iv)，cbc 模式也可以使用向量初始化。  
向量初始化的值在加解密时必须是独一无二的，同时也要保持相同。当加密后的资料输出时，也可同时输出密码钥匙 (例如存在文件中)；或者也可以将向量初始化的值与加密后的资料一起输出。

mcrypt\_get\_cipher_name: 取得编码方式的名称。  
mcrypt\_get\_block_size: 取得编码方式的区块大小。  
mcrypt\_get\_key_size: 取得编码钥匙大小。  
mcrypt\_create\_iv: 从随机源将向量初始化。  
mcrypt_cbc: 使用 cbc 将资料加/解密。  
mcrypt_cfb: 使用 cfb 将资料加/解密。  
mcrypt_ecb: 使用 ecb 将资料加/解密。  
mcrypt_ofb: 使用 ofb 将资料加/解密。

mcrypt\_get\_cipher_name  
取得编码方式的名称。  
语法: string mcrypt\_get\_cipher_name(int cipher);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数用来取得编码方式的名称。返回值为名称字符串，若没有指定的编码方式则返回 false 或输入的名称。  
使用范例  
下例会输出 tripledes 字符串。  
$cipher = mcrypt_tripledes;  
print mcrypt\_get\_cipher_name($cipher);  
?>

mcrypt\_get\_block_size  
取得编码方式的区块大小。  
语法: int mcrypt\_get\_block_size(int cipher);  
返回值: 整数  
函数种类: 编码处理  
内容说明: 本函数用来取得编码方式的区块大小。参数为编码名称，返回整数单位为位组 (byte)。

mcrypt\_get\_key_size  
取得编码钥匙大小。  
语法: int mcrypt\_get\_key_size(int cipher);  
返回值: 整数  
函数种类: 编码处理  
内容说明: 本函数用来取得编码钥匙的大小。参数为编码名称，返回整数治募�单位为位组 (byte)。

mcrypt\_create\_iv  
从随机源将向量初始化。  
语法: string mcrypt\_create\_iv(int size, int source);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数用来建立向量初始化 (initialization vector, iv) 的值。参数 size 为指定的向量初始化长度。  
参数 source 为随机资料的来源，来源可以是 mcrypt\_rand (系统产生的随机值)、mcrypt\_dev\_random (unix 系统中 /dev/random 的资料)、mcrypt\_dev\_urandom (unix 系统中 /dev/urandom 的资料)，若使用 mcrypt\_rand 当做随机源，记得先使用 srand() 产生乱数种子。  
使用范例  
$cipher = mcrypt_tripledes;  
$block\_size = mcrypt\_get\_block\_size($cipher);  
$iv = mcrypt\_create\_iv($block\_size, mcrypt\_dev_random);  
?>

mcrypt_cbc  
使用 cbc 将资料加/解密。  
语法: string mcrypt_cbc(int cipher, string key, string data, int mode, string \[iv\]);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数使用 cbc 密码检索本 (cipher block chaining)，将资料加密及解密。参数 cipher 为加/解密方式，例如 mcrypt\_tripledes。参数 key 是密码钥匙，当然要注意保持它的机密性。欲加密或解密的字符串就放在参数 data 之中。参数 mode 表示加密 mcrypt\_encrypt 或是解密 mcrypt_decrypt。参数 iv 是可省略的参数，代表向量初始化 (initialization vector, iv)。

mcrypt_cfb  
使用 cfb 将资料加/解密。  
语法: string mcrypt_cfb(int cipher, string key, string data, int mode, string iv);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数使用 cfb 密码检索本 (cipher feedback)，将资料加密及解密。参数 cipher 为加/解密方式，例如 mcrypt\_tripledes。参数 key 是密码钥匙，当然要注意保持它的机密性。欲加密或解密的字符串就放在参数 data 之中。参数 mode 表示加密 mcrypt\_encrypt 或是解密 mcrypt_decrypt。参数 iv 是代表向量初始化 (initialization vector, iv)。

mcrypt_ecb  
使用 ecb 将资料加/解密。  
语法: string mcrypt_ecb(int cipher, string key, string data, int mode);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数使用 ecb 密码检索本 (electronic codebook)，将资料加密及解密。参数 cipher 为加/解密方式，例如 mcrypt\_tripledes。参数 key 是密码钥匙，当然要注意保持它的机密性。欲加密或解密的字符串就放在参数 data 之中。参数 mode 表示加密 mcrypt\_encrypt 或是解密 mcrypt_decrypt。

mcrypt_ofb  
使用 ofb 将资料加/解密。  
语法: string mcrypt_ofb(int cipher, string key, string data, int mode, string iv);  
返回值: 字符串  
函数种类: 编码处理  
内容说明: 本函数使用 ofb 密码检索本 (output feedback)，将资料加密及解密。参数 cipher 为加/解密方式，例如 mcrypt_tripledes。参数 key 是密码钥匙，当然要注意保持它的机密性。欲加密或解密的字符串就放在参数 data

humen1 Tech