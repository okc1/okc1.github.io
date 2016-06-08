---
layout: post
title: "[Design] Cryptographic standard, AES and RSA "
comments: true
category: Design

---

# Overview

## 3 areas of cryptographic standard:

1. encryption standard

    1. Data Encryption Standard (obsolete)
    1. Triple DES
    1. __Advanced Encryption Standard (AES)__
    1. __RSA__
    1. OpenPGP
    1. CipherSaber

1. hash standard

    1. __MD5__
    1. __SHA-1__
    1. SHA-2
    1. HMAC
    1. PBKDF2

1. digital signature standard

    1. Digital Signature Algorithm (DSA)
    1. RSA
    1. Elliptic

## Symmetric-key algorithm 

[Use the same cryptographic keys](http://en.wikipedia.org/wiki/Symmetric-key_algorithm) for both encryption and decryption. 

The keys represent a shared secret between two parties, and maintain a private information link. 

This requirement that both parties have access to the secret key is one of the main drawbacks. 

## Public-key cryptography 

The public key is used: 

1. encrypt plaintext 
1. verify a digital signature

private key is used: 

1. decrypt ciphertext 
1. create a digital signature.

# Encryption standard

## RSA Vs. AES

__RSA is very computationally expensive__ by comparison with AES. It involves mathematics with very large numbers, whilst AES can be implemented with relatively simple bit operations. 

[RSA is a public-key encryption algorithm](http://security.stackexchange.com/questions/10949/encryption-should-i-be-using-rsa-or-aes) (asymmetric), while AES is a symmetric key algorithm. Often a cryptosystem will use both algorithms. 

[A good compromise is to](http://stackoverflow.com/questions/13238674/aes-vs-rsa-to-encrypt-large-size-of-data) use RSA to encrypt the symmetric key that is then used in AES encryption of the larger data.

## GitHub

uses RSA encryption.

# hash standard

## MD5

The MD5 message-digest algorithm is a widely used cryptographic hash function producing a 128-bit (16-byte) hash value, or 32 digit Hex.

> d -> 8277e0910d750195b448797616e091ad
>
> good morning -> 2b849500e4585dab4196ec9a415edf8f

## SHA-1

SHA-1 produces a 160-bit (20-byte) hash value, or 40 digit Hex.

## For more

About MD5, SHA-1 and other, refer to __[Design] Cryptographic Hash, MD5 and Digital Signature__

# digital signature standard

A valid digital signature gives a recipient confidence that the message was created by a known sender.

commonly used for software distribution, financial transactions 

{% img middle /assets/images/digital_signature.png %}

[To create a digital signature](http://searchsecurity.techtarget.com/definition/digital-signature), signing software (such as an email program) creates a one-way hash of the data to be signed. The private key is then used to encrypt the hash. 

> The reason for encrypting the hash instead of entire message is that a hash function can convert an arbitrary input into a fixed length value, which is usually much shorter. 

Other party validate the integrity of the data by using the signer's public key to decrypt the hash.

> Note: you can choose to '__ Add digital signature to this message __' in Microsoft Office. 
