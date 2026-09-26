# Hybrid Encryption Framework -- Baudot + Chaotic Maps + AES / 3DES / Twofish

> **Integrating Baudot Encoding and Chaotic Maps with Symmetric Cryptography: A Hybrid Encryption Framework**
> IEEE ICECA 2025 -- DOI: [10.1109/ICECA66444.2025.11383142](https://doi.org/10.1109/ICECA66444.2025.11383142)

---

## Overview

A **triple-layer hybrid encryption pipeline** that combines classical encoding techniques with chaotic randomness and modern symmetric ciphers. The framework is designed for a client-server communication model and benchmarked across file sizes from 10 KB to 200 KB.

### Encryption Pipeline

```
Plaintext
    |
    v
[Layer 1] Modified Caesar Cipher
          -- circular linked list determines shift value based on adjacent word count
    |
    v
[Layer 2] Baudot Encoding
          -- maps characters to 5-bit Baudot codes
    |
    v
[Layer 3] Symmetric Encryption (choose one)
          |-- AES-256 (CBC mode)
          |-- 3DES
          +-- Twofish
    |
    v
Ciphertext
```

---

## Algorithms

| Algorithm | Key Size | Block Size | Notes |
|---|---|---|---|
| AES-256 | 256-bit | 128-bit | Fastest; NIST standard |
| 3DES | 168-bit (effective) | 64-bit | Secure but slower than AES |
| Twofish | 256-bit | 128-bit | Feistel network; AES finalist |

**Chaotic key generation:** Tent map and logistic map used to generate pseudo-random key material with high sensitivity to initial conditions -- small changes in seed produce completely different keys (avalanche effect).

---

## Benchmarks

Evaluated on synthetic plaintext at 10 / 50 / 100 / 150 / 200 KB:

| Metric | Description |
|---|---|
| Encryption time (ms) | Time to encrypt at each file size |
| Decryption time (ms) | Time to decrypt and recover plaintext |
| Avalanche effect (%) | % of output bits changed per 1-bit input change |

---

## Files

| File | Description |
|---|---|
| `AES CODES.ipynb` | AES-256 encryption + benchmark |
| `3DES CODES.ipynb` | 3DES encryption + benchmark |
| `2FISH CODES.ipynb` | Twofish encryption + benchmark |

---

## Requirements

```bash
pip install pycryptodome
```

---

## Key Concepts

- **Avalanche effect** -- a property of good ciphers: flipping 1 input bit changes ~50% of output bits
- **Chaotic maps** -- deterministic systems with extreme sensitivity to initial conditions; useful for key generation
- **Baudot encoding** -- 5-bit character encoding predating ASCII; adds a structural obfuscation layer
- **Why hybrid?** -- No single algorithm is optimal across all metrics; this framework lets you select by speed vs security trade-off

---

## Authors

Geda Tejesh Chowdary | Paramkusam Sriharsha | Yelipe Gowtham

Amrita Vishwa Vidyapeetham, Bengaluru
