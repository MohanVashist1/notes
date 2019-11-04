# CSCD27

## Lecture Notes

### LEC 1: Thursday, September 5, 2019

#### Definitions

**Safety:** Satisfies specifications

**Security:** Resists attacks

**Security Theature:**

![security theatre](/Users/joshuaconcon/notes/cscd27/security theatre.png)

**CIA Security Properties:**

- **Confidentiality:** Information is disclosed to legitimate users
- **Integrity:** Information is created or modified by legitimate users
- **Availability:** Information is accessible to legitimate users

**The properties can be conflicting:**

- **Anonymity:** "Do not record the identity of the user that performed an action"
- **Accountability: **"Knowing that someone has done an action"
- **Non-repudation:** "Someone cannot deny having done an action"

Security is often a Compromise

|                            | System         | Security                          |
| -------------------------- | -------------- | --------------------------------- |
| What is it supposed to do? | Specification  | Risk Analysis and Security Policy |
| How does it do it?         | Implementation | Mechanisms                        |
| Does it really do it?      | Validation     | Assurance                         |

**Risk Analysis and Security Policy**

- Goal: Inferring what can go wring with the system
- Outcome: Set of security goals
- Principles: You never prevent a threat, you lower a risk. Performing an attack is more or less difficult the assets to protect vs the attacker's efforts

**Mechanisms**

- Goal: Define a strategy to realize the security goals
- Outcome: Set of security mechanisms
- Principle: Deploying security mechanisms has a cost (cost of recovering vs cost of deployment)

**Assurance**

- Goal: Make sure that the security mechanisms realize the security goals
- Outcome: Methodology
- ### Principle: Full assurance cannot be achieved.

#### Risk Management Analysis of Security

- You can never prevent a threat, you can only lower the risk
- Performing an attack is more or less difficult 
  - the asset to protect vs the attacker's efforts
- Deploying a counter-measure has a cost
  - cost of recoverying vs cost of deployment

Risk Exposure $=$ probability $\times$ impact

## LEC 2: Thursday, September 12, 2019

#### Classical Cryptography

**Caesar Cipher:**

- A shift cipher - attributed to Julius Caesar
- Shift the alphabet 3 places further down and substitute letters

**Threats of Communication over an insecure medium:**

- **Interception:** an attacker can read messages
- **Modification:** an attacker can modify messages
- **Fabrication:** an attacker can inject messages
- **Interruption:** an attacker can block messages

**Confidentiality and Integrity of communications** - Implement a **virtual trusted channel** over an insecure medium

#### Definitions

**Cryptographic Algorithm:** The method to do encryption and decryption

**Cryptographic Key:** An input variable used by the algorithm for the transformation

**N-bit security entropy (aka the key space):** The number of bits necessary to encode the number of possible keys (could be different from the key length)

**Plaintext:** The message in its clear form (the original message)

**Ciphertext:** The message in its ciphered form (the encrypted message)

**Encryption:** Transform a plaintext into ciphertext

**Decryption:** Transform a ciphertext into plaintext

Cryptographic algorithms are mathematical operations, so messages and keys must be represented as numbers. For instance, ASCII encoding.

**Caesar Cipher:**

- **Algorithm:** shift the alphabet of a certain number of positions
- **Key:** the number of positions to shift
- **Key space:** 25 possible rotations (around 5 bits of security)
- **Encoding:** $a = 0, b =2,..., z=25$
- **Encrypting:** $E(k,p) = (p+k)\mod 26 = c$
- **Decrpyting:** $D(k,c) = (c-k) \mod 26 = p$

##### Breaking the Cipher

**The Kerckhoff's principle (1883):**

- "The enemy knows the system"
- The security of a communication should not rely on the fact that the algorithms are secrets
- A cryptosystem should be secure even if everything about the system, except the key, is public knowledge
- No security by obscurity

**Breaking the cipher - the attacker's model:**

- Exhaustive Search (Brute Force)
  - Try all possible $n$ keys (on average it takes $\frac{n}{2}$ tries)
  - Always works
- Ciphertext only
  - You know one or several <u>random ciphertexts</u>
  - Requires Statistical Analysis
- Known plaintext
  - You know one or several pairs of <u>random plaintext</u> and their corresponding ciphertexts
  - Look at the first letter and get the shift
- Chosen plaintext
  - You know one or several pairs of <u>Chosen plaintext</u> and their corresponding ciphertexts
  - Choose $A$ and get the shift
- Chosen ciphertext
  - You know one or several pairs of plaintext and their corresponding <u>chosen ciphertexts</u>
  - Choose $A$ and get the shift

**Stastical Cryptanalysis:** Monoalphabetic ciphers do not change the relative frequency of letters in a message

**Substitution Ciphers (mono alphabetic ciphers):**

- This is an improvement over the casear cipher

- **Algorithm:** Allow an arbitrary permutation of the alphabet
- **Key:** set of substitutions
- **Key space:** 26! possible substitutions (89 bits)



**Breaking substitution ciphers:**

- Exhaustive Search (Brute Force)
  - Doable with a computer
- Ciphertext only
  - Requires Statistical Analysis
- Known plaintext
  - Match letters together
- Chosen plaintext
  - Choose $ABCDE...$ and match letters
- Chosen ciphertext
  - Choose $ABCDE...$ and match letters

**Polyalphabetic cipher (Renaissance Cipher):**

- Vigenere Cipher
- **Algorithm:** Combine the message and the key
- **Key:** a word
- **Key space:** the length of the word
- **Advantage:** Encryption of a letter is context dependent

**Breaking polyaphabetic ciphers:**

- Exhaustive Search (Brute Force)
  - Small key length only
- Ciphertext only
  - Requires Statistical Analysis for small key lengths and a significant amount of cipher text
- Known plaintext
  - subtract plaintext from ciphertext
- Chosen plaintext
  - Choose $AAAAA...$ and match letters
- Chosen ciphertext
  - Choose $AAAAA...$ and match letters

**OTP - One Time Pad:**

- Improvement over the Vigenere cipher
- **Algorithm:** combine the message and the key
- **Key:** an infinite random string
- **Key space:** infinite
- **Advantage:** This is the perfect cipher
- **Disadvantage:** Hard to use in practice, in terms of transmitting the key

The ciphertext bears no statistical relationship with the plaintext, so we can not derive anything with statistical analysis.

For any plaintext and ciphertext, there exists a key mapping one to the other, and all keys are equally probable $\longrightarrow$ A ciphertext can be decrypted to any plaintext of the same length

**Transposition Cipher:**

- **Algorithm:** switch letters around a permutation
- **Key:** a set of permutation
- **Key space:** the set of permuations

**Breaking Transposition ciphers:**

- Exhaustive Search (Brute Force)
  - Small key length only
- Ciphertext only
  - Hard
- Known plaintext
  - Match letters together
- Chosen plaintext
  - Choose $ABCDE...$ and match letters
- Chosen ciphertext
  - Choose $ABCDE...$ and match letters

The seeds of modern cryptography

- Diffusion
  - Mix-up symbols
  - Transposition Cipher
- Confusion
  - Replace a symbol with another
  - Polyalphabetic Cipher
- Randomization
  - Repeated encryption of the same text are different
  - OTP

#### Cryptography is not just about condifentiality

- Integrity
  - Digital Signatures, Hash Functions
- Non-repudiation
  - Contract-signing
- Anonymity
  - Electronic Cash, Electronic Voting

##### The Cryptography Toolbox

- Symmetric Cryptography Schemes
  - The same key is used for encryption and decryption
- Asymmetric Cryptography Schemes
  - Public key for encryption
  - Private key for decrpytion
- Message Digests
  - meant for creating fingerprints of messages
  - Unkeyed messages digests: hashes, checksum
  - Keyed message digests: MACs
- Digital Signatures
  - The private key for encryption
  - The public key for decryption
- Certificates
  - meant for verifying identity
  - binding between a public key and an owner
  - certified by a certification authority