# openssl-encrypt

Convenience scripts to encrypt/decrypt files with RSA public/private key pairs.
Encryption only requires the public key, decryption requires the private key.

Usage:

```
rsa-encrypt -i inputfile [-k publickey] [-o outputfile] [--rm]
```
Generates two files, a key file, encrypted with the public key provided (or the user's default one) using RSA,
and a file encrypted with the key file using AES-256.
If the output file is not specified, the name of the inputfile is used,
appended with .key and .enc for the key and encrypted file.
If the output file is specified, the name is used as given, and the key is that name appended with .key.

```
rsa-decrypt -k keyfile -i inputfile [--rm]
```
Generates one file, a decrypted file. This is always decrypted with the private key at ~/.ssh/id_rsa.
The outputted files are given the same names as the 

The `--rm` option in each script allows the scripts to delete the input files, and the keyfile in the case of the decrypt script.

WARNING: Files are encapsulated in a .tar archive before encryption, and extracted upon decryption.
As such, files are outputted with the same filenames when decrypted that they had when encrypted. THIS INCLUDES FILES THAT WERE SPECIFIED WITH ABSOLUTE PATHS. Use the same level of caution with this as you would with tar archives.

These scripts use the public/private key pairs found in ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub, unless specified.
If another public key is specified, it should be in .pem format. Creation of a public key in .pem format
requires access to the private key. An .pem public key can be generated like this:

```
openssl rsa -in ~/.ssh/id_rsa -pubout > ~/.ssh/id_rsa.pub.pem
```
