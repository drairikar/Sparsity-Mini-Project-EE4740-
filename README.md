# One-Time Pad: An Information-Theoretic Look at Perfect Secrecy

Mini-project for **EE4740 Data Compression: Entropy and Sparsity**, TU Delft. A one-time-pad (OTP) cipher is
implemented, and Shannon's perfect-secrecy condition is checked empirically by measuring entropies of the
plaintext and ciphertext.

## What the notebook does

1. **OTP encryption and decryption**: each character's code point is XOR-ed with a uniformly random key
   byte of the same length as the message.
2. **Distributions**: empirical PMFs of plaintext characters and ciphertext symbols.
3. **Entropy analysis**: H(M), H(C) and H(M | C).

The input text, `King_lear.txt`, is ~2.5 k characters of Shakespeare's opening sonnets (public domain).

## Results

| Quantity | Value |
| --- | ---: |
| H(M), plaintext | 4.42 bits/char |
| H(C), ciphertext | 7.99 bits/symbol (maximum is 8) |
| H(M \| C) | 4.42 bits |

The ciphertext is close to uniform over 256 symbols, and H(M | C) = H(M), as perfect secrecy requires:
seeing the ciphertext tells you nothing about the message.

## Caveat

`joint_pdf` builds P(M, C) as P(M)·P(C), i.e. it *assumes* independence. With that construction
H(M | C) = H(M) holds by definition, so it is not tested empirically. A real check counts the observed
(mᵢ, cᵢ) pairs. With only ~2.5 k pairs spread over ~256 × 70 bins, the plug-in estimate is strongly biased
downward, so it needs a much longer text or a bias-corrected estimator (e.g. Miller–Madow).

## Running

```bash
pip install -r requirements.txt
jupyter notebook OTP_Final.ipynb
```
