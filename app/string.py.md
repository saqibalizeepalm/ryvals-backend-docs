# Documentation for `string.py` File 📜

The `string.py` file provides functionality for hashing and encrypting strings. This module is essential for ensuring data security, such as safeguarding sensitive information through hashing and encryption. Below is a detailed explanation of the components within this file.

## Table of Contents 📚
1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Class: Hash](#class-hash)
    - [Attributes](#attributes)
    - [Methods](#methods)
        - [_generatesalt](#method-generatesalt)
        - [createhashforstring](#method-createhashforstring)
        - [encrypt_string](#method-encrypt_string)
        - [decrypt_string](#method-decrypt_string)

## Overview 🌟
The `string.py` file offers several functions for cryptographic operations using the `Hash` class. The main operations include:
- Generating a secure salt.
- Hashing a string.
- Encrypting a string.
- Decrypting a string.

## Dependencies 📦
The module relies on the following Python libraries:
- `os`: For accessing environment variables.
- `random`: Used for generating random numbers.
- `hashlib`: Provides a common interface to many secure hash and message digest algorithms.
- `secrets`: Used for generating cryptographically strong random numbers.
- `cryptography.fernet`: Implements symmetric encryption and decryption.

## Class: Hash 🔐
The `Hash` class encapsulates all functionalities for hashing and encryption. It does not need to be instantiated since all methods are static.

### Attributes 📋
- **_fernet_key**: A class-level attribute that stores the Fernet encryption key, fetched from the environment variables.

### Methods 🛠️

#### Method: `_generatesalt()` 🍀
```python
@staticmethod
def _generatesalt():
    secrets_generator = secrets.SystemRandom()
    salt = hashlib.sha256(str(secrets_generator.uniform(0, 1)).encode('utf-8'))
    return salt.hexdigest()
```
- **Purpose**: To generate a unique salt using a secure random number generator.
- **Returns**: A SHA-256 hashed salt as a hexadecimal string.

#### Method: `createhashforstring(string)` 🔨
```python
@staticmethod
def createhashforstring(string):
    salt = Hash._generatesalt()
    salt = salt[0:5] + string + salt[0:5]
    return hashlib.sha256(salt.encode('utf-8')).hexdigest()
```
- **Purpose**: Creates a hash for the given string by adding a salt.
- **Parameters**: 
  - `string`: The string to hash.
- **Returns**: A SHA-256 hash of the salted string.

#### Method: `encrypt_string(plain_text)` 🔒
```python
@staticmethod
def encrypt_string(plain_text):
    cipher_suite = Fernet(Hash._fernet_key)
    plain_text = plain_text.encode('utf-8')
    return cipher_suite.encrypt(plain_text)
```
- **Purpose**: Encrypts a given plain text string.
- **Parameters**: 
  - `plain_text`: The text to encrypt.
- **Returns**: Encrypted string in bytes.

#### Method: `decrypt_string(encrypted_text)` 🔓
```python
@staticmethod
def decrypt_string(encrypted_text):
    cipher_suite = Fernet(Hash._fernet_key)
    try:
        return cipher_suite.decrypt(encrypted_text)
    except InvalidToken:
        return b''
```
- **Purpose**: Decrypts a given encrypted string.
- **Parameters**: 
  - `encrypted_text`: The encrypted text to decrypt.
- **Returns**: The original plain text in bytes, or an empty byte string if decryption fails due to an invalid token.

## Conclusion 🎯
The `string.py` file is a crucial component for data security within the application. It provides robust methods for hashing and encrypting strings, ensuring that sensitive information is adequately protected. Proper handling of the encryption key is essential for maintaining the security of the encrypted data.