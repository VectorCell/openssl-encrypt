# openssl-encrypt

Convenience scripts to encrypt/decrypt files with RSA public/private key pairs. Encryption only requires the public key, decryption requires the private key.

Usage:

```
rsa-encrypt [inputfile] [publickey]
```
Generates two files, a key file, encrypted with the public key provided (or the user's default one) using RSA, and a file encrypted with the key file using AES-256.

```
rsa-decrypt [keyfile] [inputfile]
```
Generates one file, a decrypted file. This is always decrypted with the private key at ~/.ssh/id_rsa

These scripts use the public/private key pairs found in ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub, unless specified.
If another public key is specified, it should be in .pem format. Creation of a public key in .pem format requires access to the private key. An .pem public key can be generated like this:

```
openssl rsa -in ~/.ssh/id_rsa -pubout > ~/.ssh/id_rsa.pub.pem
```
