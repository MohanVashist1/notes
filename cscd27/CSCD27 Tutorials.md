# CSCD27

## Tutorials

### TUT 3: Tuesday, September 24, 2019

#### Stream Cipher

1. We implement a basic stream cipher that combines (xor) a plaintext message (m) with a key (k) of the same length.

- How is the message encrypted and decrypted? Write down the equations.
  - $E_K (M) = K \bigoplus M$
  - $D_K (C) = K \bigoplus C$
- Considering a known-plaintext attack (1 instance), can you recover the key? If so, write down the equations.
  - Have $C_1$ know corresponding $M_1$
  - We know that $C_1 = M_1 \bigoplus K$ so we can do $C_1 \bigoplus M_1 = (M_1 \bigoplus K) \bigoplus M_1 = K$ to get the key
- Considering a ciphertext-only attack (2 instances), what can you recover? If so, write down the equations and name the attack.
  - We have $C_1, C_2$.
  - $C_1 = M_1 \bigoplus K$
  - $C_2 = M_2 \bigoplus K$
  - $C_1 \bigoplus C_2 = M_1 \bigoplus M_2$

2. We use RC4 that uses a pseudo-random number generator $RNG(s)$, s being the seed.

- How is the message encrypted and decrypted? Write down the equations.
  - $C = M \bigoplus RNG(K)$
  - $M = C \bigoplus RNG(K)$
- Considering the same known-plaintext attack as in question 1, can you recover the key?
  - We have $C_1$
  - Do $C_1 = M_1 \bigoplus RNG(K)$
  - $C_1 \bigoplus M_1 = (M_1 \bigoplus RNG(K)) \bigoplus M_1 = RNG(K)$
- Considering the same ciphertext-only attack as in question 1, what can you recover?
  - Have $C_1, C_2$
  - $C_1 = M_1 \bigoplus RNG(K)$
  - $C_2 = M_2 \bigoplus RNG(K)$
  - $C_1 \bigoplus C_2 = M_1 \bigoplus M_2$

We can make this stronger by instead of using $K$, we use $IV+K$ where $IV$ is a random string that we new every time. This will keep us protected as $IV$ will be different every time. With this, you cannot cancel out $RNG(IV_1 + K)$ with $RNG(IV_2 + K)$

3. What recommendation could you give to a software engineer who wants to use a stream cipher?

   **Don't.**

#### Block Cipher

1. We use AES 128 bits to encode a 128 bits message.

- Considering the same known-plaintext attack as considered previously, can you recover the key?
  - Since this is not being encrypted with XOR, but with a more complicated function, we cannot recover the key.
- Considering the same ciphertext-only attack as considered previously, what can you recover?
  - Here we also cannot recover the key because we cannot cancel things out like with XOR

We use AES 128 bits to encrypt the following message (32 characters):

```
On Thursday, we attack Mallory!
```

Let’s consider a chosen-plaintext attack where the attacker (Mallory) has chosen by luck the following message (16 characters):

```
 attack Mallory!
```

2. Considering that we use AES in ECB mode (Electronic Code Book), can the attacker …

- recover the key?

  - **No.** The encryption is still too complex

- recover the first half of the message?

  - **No.** The encryption is still too complex

- recover the second half of the message?

  - **No.** The encryption is still too complex

- modify the message in an intelligible way using another chosen-plaintext?

  - **No.** The encryption is still too complex, unless they are using the same key

  

  3. Same questions but considering the use of the CBC mode (Cipher Block Chaining)

- recover the key?
  
  - **No.** The encryption is still too complex
- recover the first half of the message?
  
  - **No.** The encryption is still too complex
- recover the second half of the message?
  
  - **No.** The encryption is still too complex
- modify the message in an intelligible way using another chosen-plaintext?
  
  - **No.** Even if we know that its using the same key, we need to know previous blocks to know the proper encryption for the block.
- However, if the known plain-text is the last block of the message, we can replace it, since we have the cipher for the previous block, which is necessary for generating the cipher for the last black.



#### Stream Cipher vs Block Cipher

- Stream Cipher is faster
- Stream Cipher is more vulnerable
- Block Cipher is stronger if it is using EBC.

#### Cryptographic Hash Function $(h(M) = X)$

Properties:

- If the result is known ($X$), it's hard to find the corresponding $M$.
- Hard to find collision if $h, M, X$ are known (i.e. $h(M') = X$)

The collision property is targetted by the birthday attack.

If we have a function $h$ with $n$ bit input and $m$ bit output, we need an average of $2^{\frac{m}{2}}$ cases to find a collision, and an average of $2^{n-1}$ to brute force the key.

### TUT 4: Tuesday, October 1, 2019

#### Asymmetric Cryptography

Alice wishes to send a signed and confidential message to Bob using public-key cryptography, such as a GPG implementation. Which of the following is correct:

- Alice signs with Bob’s public key, and encrypts with her private key.
- **Alice signs with her private key and encrypts with Bob’s public key.**
- Alice signs with her private key and encrypts with Bob’s private key.
- Alice signs with Bob’s private key and encrypts with Bob’s public key.
- Alice signs with her private key and encrypts with her private key.

Public Key is used to encrypt and to check the sign, Private Key is used to sign and decrypt

#### Public-key Protocol

Take a look at the simplified version of the *Needham-Shroeder* public-key protocol seen in class. This protocol tries to achieve two goals: 1) making sure that one is talking to the right person (authentication) and 2) exchanging a symmetric session key.

1. Why is Alice sending the nonce *Na* to Bob? If she does not, can you show how an attacker could compromised either of both goals?
2. Why is Bob sending the none *Nb* to Alice? If he does not, can you show how an attacker could compromised either of both goals?
3. Despite the double-challenge protocol, there is man-in-the-middle attack on the Needham-Shroeder protocol. Describe that attack and its fix.
   1. Lowe's

Asymmetric Key is used to exchange the Symmetric Keys, and then use Symmetric Keys for encrypting/decrypting, as it is faster.

#### Trust Models

1. In GPG, what are the two ways to trust a GPG key?
2. Describe how a man-in-the-middle attack could succeed on GPG?
3. In TLS/SSL, how does your browser trust a certificate supplied by a website?
4. Describe how a man-in-the-middle attack could succeed on TLS/SSL?