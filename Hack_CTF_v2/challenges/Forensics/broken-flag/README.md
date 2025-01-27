# Broken Flag

## Description

Here is a mysterious file.

## Files

* [BrokenFlag.zip](<files/BrokenFlag.zip>)

### Steps Followed:

1. Extract the provided `BrokenFlag.zip` file:
   - The extraction results in three image files: `notFunny.png`, `whatEvenIsThis.png`, and `Ig3twhy7h4tsFunny.png`.
2. Analyze the image `whatEvenIsThis.png`:
   - Replace the white pixels with `1` and black pixels with `0`.
   - This gives one part of the flag: `hacks{im4g3_4nd`.
![image](https://github.com/user-attachments/assets/3380358e-29ed-4131-ad55-73d5d545448c)
![image](https://github.com/user-attachments/assets/935fffbc-23d5-409d-8ed9-fb2558f4d16e)
  
3. Use `zsteg` to analyze the images `notFunny.png` and `Ig3twhy7h4tsFunny.png`:
   - Command: `zsteg notFunny.png`
   - Output: `b1,bgr,lsb,xy       .. text: "S465626 1694263 1801877 640168 465626 1801877 1536566 1226671 435791 1801877 2026202"`
   - Command: `zsteg Ig3twhy7h4tsFunny.png`
   - Output: `b1,bgr,lsb,xy       .. text: "461 4493 65537"`
![image](https://github.com/user-attachments/assets/170c0ea7-7248-4deb-80d9-345424323c40)
![image](https://github.com/user-attachments/assets/d68d38ce-da77-405d-a92d-d315816e32cf)

4. The output from `zsteg` looks like RSA parameters:
   - `p = 461`, `q = 4493`, and `e = 65537`.
5. Use these values to decrypt the ciphertext:
   - Decrypt each ciphertext using RSA to retrieve one letter of the flag.
6. Combining the decrypted letters reveals the remaining part of the flag.
```python
p = 461
q = 4493
e = 65537
n = p * q
phi_n = (p - 1) * (q - 1)

def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    g, x1, y1 = extended_gcd(b, a % b)
    x = y1
    y = x1 - (a // b) * y1
    return g, x, y

def mod_inverse(a, m):
    g, x, y = extended_gcd(a, m)
    if g != 1:
        raise Exception('Modular inverse does not exist')
    return x % m
d = mod_inverse(e, phi_n)
ciphertext = [465626, 1694263, 1801877, 640168, 465626, 1801877, 1536566, 1226671, 435791, 1801877, 2026202]

plaintext = [pow(c, d, n) for c in ciphertext]
print(''.join([chr(p) for p in plaintext]))
```
output: _rs4_sUcKs}

### Final Flag:
`hacks{im4g3_4nd_rs4_sUcKs}`
