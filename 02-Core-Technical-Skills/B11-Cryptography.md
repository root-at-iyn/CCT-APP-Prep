# Cryptography

## Differences between encryption and encoding.

### Encoding

Encoding is the process where data is transformed into a different format using a particular scheme. This transformation does not require a key to decode the transformed *(encoded)* data, but only requires the same scheme's decoding function is used. Examples of encoding schemes are: 

- Base64
- ASCII
- UTF-8
- UTF-16

### Encryption

Encryption is the process of scrambling plain text data into ciphertext data using a key. Without the key, the encypted data *(ciphertext)* cannot be reversed back to plain text data. Encryption is used to protect the confidentiality of data, and can be done using public-key encryption *(key pairs where one key is used to encrypt and the other to decrypt)* or using bulk ciphers *(algorithms that use cryptographic primitives and a key)*. 

## Symmetric / Asymmetric encryption

### Symmetric Encryption

- Uses the same key is for both encryption and decryption.
- Examples include AES, 3DES, Blowfish, Twofish, Skipjack, DES, RC4
- Symmetric encryption uses bulk ciphers, which are either stream ciphers or block ciphers.

There are two types of bulk ciphers:

#### Stream Ciphers

A stream cipher operates on **1 bit of data at a time**. The key in a stream cipher is used to generate pseudorandom bits *(keystream)* which is then XOR'd with the plaintext bits to encrypt it. The keystream is made up of a key which should remain secret **(128-bits or 256-bits)**, and a nonce which must be unique *(between 64-bits - 128-bits)*. The ciphertext is decrypted by XORing the ciphertext with the same keystream. RC4 (128 bit) is the most common stream cipher.

#### Block Ciphers

A block cipher operates on data in groups (or blocks) of bytes. Stream ciphers perform better than block ciphers. However, block ciphers provide better security. DES (56-bit), Triple-Data Encryption Standard (3DES) (168-bit), and Advanced Encryption Standard (AES) are the most common block ciphers. DES and 3DES operate on blocks of 8 bytes at a time. AES operates on blocks of 16 bytes at a time.

Block ciphers can operate in cipher block chaining (CBC) mode. CBC mode means that each block depends on the proper encryption of the block before it. This interdependence ensures that a change to any of the plaintext bits will cause the final encrypted block to change in a way that cannot be predicted or counteracted without knowing the key to the block cipher.

CBC mode requires an initial chaining vector (ICV or IV), which is used to prevent two identical text sequences from producing the same ciphertext when encrypted. The ICV is updated each time a block is encrypted; the result is an output chaining vector (OCV or OV). For contiguous data, the OCV is automatically used as the ICV for the next block of data. For discontiguous data, it is your responsibility to pass the OCV from the previous block of data as the ICV for the next block. The recipient of the final encrypted data needs the original ICV to decrypt the data. In most cases there is no need for the ICV to be secret, but it should never be reused with the same key. The size of the ICV is the same as the cipher block size (8 bytes for DES and TDES, 16 bytes for AES).

### Asymmetric Encryption

- Also known as `public key encryption`, uses a key pair *(public key / private key)* where one key is used to `encrypt` data, and the other key is used to `decrypt` data.
- RSA is an example of an asymmetric encryption algorithm

## Encryption algorithms:
### - DES
- A symmetric encryption algorithm (Block Cipher) that encrypts a plain text data with **56 bit key**. The key size is actually 64 bits, but 8 bits of the 64-bit key is used for checking errors in the cipher text *(parity bits)*. This is why the effective key length is `56-bits`.
1. The plain text is data is divided into block sizes of 64-bits.
2. Each block is goes through an inital permutation and is then divded into two parts.
3. The two parts go through the `Fiestel` function for 16 rounds.
4. The text goes through another final round of permutation and results in ciphertext.
- As DES is a symmetric encryption algorithm, the same key is used to decrypt the cipher text.

### - 3DES
- A symmetric encryption algorithm (Block Cipher) that was introduced to solves some of the problems with DES which is no longer considered secure. It applies the DES cipher algorithm three times to each data block for more effective key length
- This works in three phases using three 56-bit keys (K1, K2, K3) which is also called a key bundle. It first uses K1 to encrypt, then K2 to decrypt, and encrypting again with K3:
    1. Encrypt (K1)
    2. Decrypt (K2)
    3. Encrypt (K3)
- 3DES runs 3 times because double encriphering is vulnerable to `meet-in-the-middle` attacks *(encrypt from one end, decrypt from the other and look for collisions -- keys that produce the same answer in either direction)*
- 3DES with 3 keys has an effective key length of `168-bits`, but with 2 keys this decreases to `112-bits`.

### - AES
- AES is a symmetric encryption algorithm (Block Cipher) that processes `blocks of 128-bits`, with a secret key that is a size of either **128, 192, or 256 bits**.
- AES key size is typically 128-bits since it's slightly faster that 256-bit keys, while not loosing a significant difference in security benefits from an applications perspective.
- Plaintext data is processed in `16 byte` chunks.
- The 16 byte plaintext chunks are viewed as a two-dimensional array of bytes (S = S<sub>0</sub>,S<sub>1</sub>, ...,S<sub>15</sub>):

    |S<sub>0</sub>|S<sub>4</sub>|S<sub>8</sub>|S<sub>12</sub>|
    |-------------|-------------|-------------|-------------|
    |S<sub>1</sub>|S<sub>5</sub>|S<sub>9</sub>|S<sub>13</sub>|
    |S<sub>2</sub>|S<sub>6</sub>|S<sub>10</sub>|S<sub>14</sub>|
    |S<sub>3</sub>|S<sub>7</sub>|S<sub>11</sub>|S<sub>15</sub>|

- The letter `S` represents the state.
- AES transforms the bytes, columns, and rows in the array to produce ciphertext.
- The state is transformed using:
    - 10 rounds for 128-bit keys
    - 12 rounds for 192-bit keys
    - 14 rounds for 256-bit keys

### - RSA
- RSA is an assymetric encyption algorithm, which uses a public / private key pair.
### - RC4
Is a stream encryption cipher.
## Hashes
Hashes are one way functions. They are used to provide integrity, 
### - SHA1
### - MD5

## Message Integrity codes:
### - HMAC
