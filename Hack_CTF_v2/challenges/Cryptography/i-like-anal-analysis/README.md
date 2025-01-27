# I like ANAL (analysis)

## Description

I was trying out this new encryption and switched to ECB mode. Can you break this?

## Files

* [output.txt](<files/output.txt>)

### Steps Followed:

1. **Inspect the Provided File**:  
   - The challenge provided a file `output.txt`, which contained multiple lines. Each line was encrypted using **ECB mode** with the same password, which means the same letter would always produce the same encrypted output.

2. **Hashing the Entries**:  
   - We first hashed each line in the file using **MD5** to generate a hash for each entry. Each line was encoded to bytes and the MD5 hash was computed using `hashlib.md5`. The result was stored as a dictionary mapping each hash to an alphabetical character.

3. **Mapping to Alphabet**:  
   - We used an ordered alphabet string (`"ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789{}_"`) to assign a unique character to each hash. The mapping was stored in the dictionary `d`, ensuring that each hash corresponds to one specific character.

4. **Substitution for Decryption**:  
   - Once the mapping was complete, we applied a substitution cipher to the output using the following substitution table:

     ```
     D → SPACE
     C → E
     E → A
     A → T
     G → O
     K → N
     F → R
     O → S
     P → I
     B → H
     N → L
     L → C
     M → Y
     R → D
     J → U
     V → P
     H → F
     S → W
     T → M
     U → B
     W → K
     I → Q
     Q → V
     Y → _
     X → {
     Z → }
     0 → P
     2 → J
     3 → U
     ```

5. **Manual Fine-Tuning**:  
   - After applying the substitution, we noticed some characters still needed manual fine-tuning to match the correct flag format. We used frequency analysis via **quipquip** to match common letters and adjusted the substitutions accordingly.

6. **Final Flag**:  
   - After applying the substitution and fine-tuning the characters, we obtained the final decrypted output, which revealed the flag.

### Flag:  
hacks{freq_anal_usinp_aes}
---

### Code Implementation:

```python
import hashlib

with open("./output.txt", 'r') as f:
    lines = f.readlines()

alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789{}_"
i = 0
d = {}

result = []
for line in lines:
    b = bytearray(line.encode())
    s = hashlib.md5(b).hexdigest()
    if i < len(alphabet):
        if not s in d:
            d[s] = alphabet[i]
            i = i + 1
        result.append(d[s])
    else:
        print("skip")

result = "".join(str(x) for x in result)

def subs(ecb_output):
    substitution = {
        'D': ' ', 'C': 'E', 'E': 'A', 'A': 'T', 'G': 'O', 'K': 'N',
        'F': 'R', 'O': 'S', 'P': 'I', 'B': 'H', 'N': 'L', 'L': 'C',
        'M': 'Y', 'R': 'D', 'J': 'U', 'V': 'P', 'H': 'F', 'S': 'W',
        'T': 'M', 'U': 'B', 'W': 'K', 'I': 'Q', 'Q': 'V', 'Y': '_',
        'X': '{', 'Z': '}', '0': 'P', '2': 'J', '3': 'U'
    }

    result = []
    for char in ecb_output:
        result.append(substitution.get(char, char))  
    return ''.join(result)

decrypted_output = subs(result)
print(decrypted_output.lower())
```
```plaintext
the art of frequency analysis is a very old technique which has come into use well before the ape of modern hacks{freq_anal_usinp_aes} computers usinp common sense and meta knowledpe of the oripinal lanpuape of the plainte1t to decipher cipherte1t has been prevalant since the world war it is quite an interestinp challenpe to do it makes you feel like a cryptopraphy e1pert durinp the world war era of human history or you mipht imapine yourself as a hacker breakinp random words and sentances for paddinp ahead lets be full of hackinp ctf flap cipher lnmhacks encrypt full empty why how data bits binary forensics cryptopraphy code technolopy cyber security codinp two thousand twenty four python java database why is frequency analysis does require a pood number of words and letters no letters where harmed in the makinp of this frequency analysis question but maybe they should have been it would have been much easier to create this challenpe this way orpanisinp a ctf is hard work please enjoy what we have prepared for you
```
