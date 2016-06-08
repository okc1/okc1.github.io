---
layout: post
title: "[Design] Cryptographic Hash, MD5 and Digital signature "
comments: true
category: Design

---

### Overview

[Cryptographic hash function](http://en.wikipedia.org/wiki/Cryptographic_hash_function) is a hash function which is considered practically impossible to invert. 

The input is arbitrary length, and output is fixed length. 

The input is called 'message' and output (the hash value) is called '__digest__'. 

Common examples are:

1. MD5
    1. 128-bit (16-byte) hash value, typically expressed with 32 digit hex number
    1. have colllision attack risks
1. SHA-1 (said to be [better than MD5](http://security.stackexchange.com/questions/19705/is-sha1-better-than-md5-only-because-it-generates-a-hash-of-160-bits))
    1. 160-bit (20-byte) hash value, typically expressed with 40 digit hex number
    1. No known collision found so far

#### Properties

1. Computationally efficient
1. Collision resistant
1. Hide information
1. Look random

#### Examples

> I generated checksum values on an important file I backed up to ensure that everything went OK. [source](http://pcsupport.about.com/od/termsm/g/md5.htm)

> To verify that the latest version of Firefox I was downloading is correct, I ran a cryptographic hash function, SHA-1 to be exact, on the download and compared that checksum with the one published on Mozilla's site. [source](http://pcsupport.about.com/od/termsc/g/cryptographic-hash-function.htm)

### Digital signature

[Digital signature](http://en.wikipedia.org/wiki/Digital_signature) is a mathematical scheme for demonstrating the authenticity of a digital message. It uses public/private keys.

In practice, the signature is not used directly on the file, but rather on the [digest of the file](http://en.wikipedia.org/wiki/Digital_signature#How_they_work). 

{% img middle /assets/images/Digital-Signature-diagram.png %}

[Video](https://www.khanacademy.org/economics-finance-domain/core-finance/money-and-banking/bitcoin/v/bitcoin-digital-signatures) on digital signature. 
