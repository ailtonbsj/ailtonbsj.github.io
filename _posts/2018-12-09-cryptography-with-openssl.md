---
layout: post
title:  "Cryptography with OpenSSL"
date:   2018-12-09 12:12:00 -0300
categories: tutorial linux hacker
---
We can use OpenSSL to do a several operations related with cryptography. The command below are the most commons options.

## Symmetric-key Encryption
```bash
# List all Ciphers
openssl list -cipher-algorithms

# AES encryption
openssl aes-256-cbc -in inseguro.txt -out seguro_aes.txt -pass pass:minhasenha

# AES decryption
openssl aes-256-cbc -d -in seguro_aes.txt -out novo.txt
```

## Asymmetric-key Encryption
```bash
# Generate private key
openssl genrsa -out priv.pem 1024 
# openssl rsa -in priv.pem -text -noout

# Generate public key
openssl rsa -in priv.pem -pubout -out pub.pem
# openssl rsa -in pub.pem -pubin -text -noout

# Encrypt
openssl rsautl -encrypt -inkey pub.pem -pubin -in inseguro.txt -out seguro_rsa.enc

# Decrypt
openssl rsautl -decrypt -inkey priv.pem -in seguro_rsa.enc > novo_rsa.txt
```

## Digital signature
```bash
# Signing
cat text.txt | openssl dgst -sha256 | cut -f 2 -d " " > soma.txt
openssl pkeyutl -sign -inkey priv.pem -in soma.txt | openssl enc -base64 > sign.base64

# Verify signature
cat text.txt | openssl dgst -sha256 | cut -f 2 -d " " > soma.txt
cat sign.base64 | openssl enc -base64 -d > text.sig
openssl pkeyutl -verify -pubin -inkey pub.pem -sigfile text.sig -in soma.txt
```