---
layout: post
title: "HTTPS NOTES"
date: 2016-12-07 22:49
comments: true
categories: Program
---

###HTTPS###

HTTP over SSL/TLS，在安全传输层中传输HTTP内容

###SSL/TLS###
    
SSL(Secure Socket Layer)
TLS(Transport Layer Security)
SSL3.0相当于TLS1.0。SSL主要用来为双方计算程序通讯时，保障数据的完整性和私密性。

私密性

* 过程：利用密钥，对正文使用密码（指定的算法）进行加密后传输；收到密文后，使用指定的密钥选择密码，对密文进行解密
* 编／解码使用相同的密钥——对称密钥加密系统；编／解码使用不同的密钥——非对称密钥加密系统；

完整性

* 对正文添加一个数字签名，用于收到报文后对数字签名进行校验，则可验证完整性

SSL handshake（SSL握手）refer：《HTTP权威指南》

* 客户端发送可供选择的密码并请求证书
* 服务器发送选中的密码和证书
* 客户端发送保密信息；客户端和服务器生成密钥
* 客户端和服务端互相告知，开始加密过程

使用openssl命令查看HTTPS过程

		openssl s_client -state -connect www.leisiwo.com:443 -servername leisiwo.com

SNI(Server Name Indication)

* TLS 扩展。通过不加密的HOSTNAME来让服务器选择指定的HOSTNAME所需的证书，来完成TLS。


####如何在github pages（custom domain）上使用HTTPS####

* 参考[secure-and-fast-github-pages-with-cloudflare](https://blog.cloudflare.com/secure-and-fast-github-pages-with-cloudflare/)


####REFERENCE####

* [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security)
* [HTTPS](https://en.wikipedia.org/wiki/HTTPS)
* [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication)
