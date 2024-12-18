# RSA Encryption and Key Management Tool

This project provides tools for managing RSA encryption and decryption keys, as well as encrypting and decrypting files. It includes the ability to generate RSA key pairs, encrypt the private key with a password, and handle file encryption/decryption.

## Overview

### Purpose

This project demonstrates how to use RSA encryption for secure key management and file encryption. It provides a simple command-line interface to generate RSA keys, protect them with a password, and encrypt/decrypt files with those keys.

The project also includes functionality to encrypt the `key_storage` folder into a `.tar.gz` archive for secure external storage.

### Structure

1. **Key Generation**: Generate RSA key pairs (public and private) with 4096-bit security.
2. **Key Encryption**: Encrypt the private key with a password.
3. **File Encryption and Decryption**: Encrypt and decrypt files using RSA public and private keys.
4. **Key Storage**: Store the keys in a folder, and encrypt this folder into a `.tar.gz` archive for secure external storage.

## Features

- **RSA Key Generation**: Generates a public/private key pair.
- **Private Key Encryption**: Encrypt the private key using a password.
- **File Encryption**: Encrypt files using the public key.
- **File Decryption**: Decrypt files using the private key.
- **Key Storage Protection**: Encrypt the entire `key_storage` folder into a `.tar.gz` file for safe external storage.

## Requirements

- Python 3.12 or later
- `cryptography` package for cryptographic operations
- `tarfile` library for working with `.tar.gz` archives

To install the required dependencies, run:

```bash
pip install cryptography
```

## How to Use

### Command-Line Interface (CLI)

This tool supports two main actions via the command line: encryption (enc) and decryption (dec). You can specify the action, the file to process, and the key storage folder.

#### 1. Encrypt a File

To encrypt a file using the RSA public key:

``` bash
python rsa_tool.py enc -f path_to_file_to_encrypt
``` 

The encrypted file will be saved in the `encrypted_files` folder.

#### 2. Decrypt a File

To decrypt a file using the RSA private key, you must provide the password that was used to protect the private key:

```bash
python rsa_tool.py dec -f path_to_file_to_decrypt -p your_password
```

The decrypted file will be saved in the `decrypted_files` folder.

### Encrypt/Decrypt Key Storage Folder

The `key_storage` folder contains the generated RSA keys (public and private). This folder can be encrypted into a `.tar.gz` archive for secure storage.

#### Encrypt the Key Storage Folder

To encrypt the `key_storage` folder into a `.tar.gz` file:

1. **Crea un archivio della cartella**:
Prima di cifrare, crea un archivio della cartella contenente le chiavi:

```bash
tar -czf chiavi.tar.gz /path/to/key_folder
```

2. **Cifra l’archivio con GPG**:
Utilizza GPG per cifrare l’archivio con una passphrase (o una chiave pubblica per una cifratura asimmetrica):

```bash
gpg -c chiavi.tar.gz
```

Il comando sopra creerà un file cifrato chiamato `chiavi.tar.gz.gpg`. Ti verrà chiesto di inserire una passphrase per cifrare l’archivio.

3. **Per decrittografare la cartella**:
Una volta che vuoi ripristinare la cartella, puoi decrittografare l’archivio e estrarre i file:

```bash
gpg -d chiavi.tar.gz.gpg > chiavi.tar.gz
tar -xzvf chiavi.tar.gz -C /path/to/extract/destination
```
