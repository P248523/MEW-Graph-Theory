MEW — Matrix Encryption Walks
Short description MEW (Matrix Encryption Walks) is an experimental, easy-to-understand symmetric encryption scheme implemented for research and testing purposes. This implementation is not intended for production use.

Overview
MEW uses two pseudo-random key matrices of size key_size × key_size.
Each byte is transformed using XOR operations with entries from the key matrices and a deterministic matrix "walk" derived from byte values.
Encryption consists of two forward passes with a reversal and coordinate append step between them; decryption reverses these steps to recover the plaintext.
Algorithm (brief)
Generate two key matrices km1 and km2 filled with random bytes.
For each input byte:
XOR with km1[row][col] to produce intermediate t.
Interpret the last 2 bits of t as a direction and the remaining bits as a movement value.
Move the current coordinates accordingly and XOR t with km2[new_row][new_col] to produce the output byte.
Append final coordinates, reverse the intermediate output, and perform a second pass; final coordinates are appended to the ciphertext.
Quick usage
from mew import MEW
m = MEW(key_size=32)
cipher = m.encrypt("hello world")
plain = m.decrypt(cipher)
Included scripts
mew.py — core MEW implementation
experiments.py — experimental suite that measures avalanche effect, entropy, timing, and other metrics
test_mew.py — unit tests
results/ — generated experiment outputs (CSV files and plots)
Notes
The implementation currently supports key_size <= 256 (single-byte coordinates). Larger key sizes require multi-byte coordinate support and are not implemented.
MEW is experimental and has not undergone formal cryptographic analysis.
If you want changes to the tone, level of detail, or additional sections (installation, examples, license), tell me which parts to adjust.
