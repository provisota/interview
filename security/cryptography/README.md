# Scope
1. Hash Functions:
    - A hash function is a function that takes an input (or 'message') and returns a fixed-size string of bytes. The output is typically a 'digest' that is unique to each unique input. It is commonly used in various applications such as checksums, digital signatures, and data retrieval.
    - Hash functions are deterministic, meaning that the same input will always produce the same output. They are designed to be fast and to produce a hash that looks 'random' and spread uniformly across the space of possible hash values.
    - An important property of a hash function is that it is computationally infeasible to regenerate the original message given only the hash value. In other words, they are one-way functions.
2. Symmetric and Asymmetric Encryption:
    - Symmetric encryption is a type of encryption where the same key is used for encryption and decryption. It is fast and efficient for large amounts of data, but the key must be kept secret and distributed securely to the other party.
    - Asymmetric encryption, also known as public key encryption, uses two different keys for encryption and decryption - a public key for encryption and a private key for decryption. It is more secure because the encryption key can be distributed widely while the decryption key is kept secret. However, it is slower and less efficient for large amounts of data.

# Questions
1. What is hash function and what are its typical usecases?
2. How does symmetric encryption works?
3. How does asymmetric encryption work?
# Answers
1. A hash function is a function that takes an input (or 'message') and returns a fixed-size string of bytes. The output is typically a 'digest' that is unique to each unique input. Hash functions are deterministic, meaning that the same input will always produce the same output. They are designed to be fast and to produce a hash that looks 'random' and spread uniformly across the space of possible hash values. An important property of a hash function is that it is computationally infeasible to regenerate the original message given only the hash value. In other words, they are one-way functions. Typical use cases of hash functions include data retrieval, digital signatures, and checksums.

2. Symmetric encryption is a type of encryption where the same key is used for both encryption and decryption. In symmetric encryption, the sender and receiver must have a copy of the same key. The sender uses this key to encrypt the plaintext and sends the ciphertext to the receiver. The receiver applies the same key to decrypt the message and recover the plaintext. Because a single key is used for both functions, symmetric encryption is generally fast and efficient, making it suitable for encrypting large amounts of data.

3. Asymmetric encryption, also known as public key encryption, uses two different keys for encryption and decryption - a public key for encryption and a private key for decryption. The public key is freely available and can be distributed widely, while the private key is kept secret. When a sender wants to encrypt a message, they use the receiver's public key. Only the receiver's private key can be used to decrypt the sender's message. This means that even if someone else has the public key, they cannot decrypt the message. This is what makes asymmetric encryption more secure than symmetric encryption. However, it is also slower and less efficient, making it less suitable for encrypting large amounts of data.