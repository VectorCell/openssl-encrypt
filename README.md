# openssl-encrypt

Convenience scripts to encrypt/decrypt files with RSA public/private key pairs. Encryption only requires the public key, decryption requires the private key.

Usage:

```
rsa-encrypt -i inputfile [-k publickey] [-o outputfile]
```
Generates two files, a key file, encrypted with the public key provided (or the user's default one) using RSA, and a file encrypted with the key file using AES-256.
If the output file is not specified, the name of the inputfile is used, appended with .key and .enc for the key and encrypted file.
If the output file is specified, the name is used as given, and the key is that name appended with .key

```
rsa-decrypt [-k keyfile] [-i inputfile] [-o outputfile]
```
Generates one file, a decrypted file. This is always decrypted with the private key at ~/.ssh/id_rsa
If the output file is not specified, it attempts to use the name of the input file, minus the .enc extension. If it can't do this, it will use the name of the input file, plus a .dec extension.

These scripts use the public/private key pairs found in ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub, unless specified.
If another public key is specified, it should be in .pem format. Creation of a public key in .pem format requires access to the private key. An .pem public key can be generated like this:

```
openssl rsa -in ~/.ssh/id_rsa -pubout > ~/.ssh/id_rsa.pub.pem
```
