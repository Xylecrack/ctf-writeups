# Someone Corrupted my Image 😠

## Description

Someone painted over this image. I need to decrypt this data ASAP!! Please help me decrypt this!

## Files

* [image.png](<files/image.png>)

## Challenge Writeup: image.png

### Challenge Overview:
The challenge provided an image containing a script for AES encryption in ECB mode. The script hinted that the key's last two hexadecimal digits, the full initialization vector (IV), and some ciphertext were hidden in the image.

![image (1)](https://github.com/user-attachments/assets/8df76ff6-4515-4dec-bd23-195a118883e6)

### Steps Taken:

1. **Initial Setup**:  
   We were given a base key (`b'lnmhacks87AB$$'`), the ciphertext in hexadecimal format (`1fd124436d6d503d7fe7bca2fbd3d6b1`), and two partial messages (`p1` and `p2`).

2. **Decryption Process**:
   - We iterated through all possible combinations of two characters (from `string.ascii_letters`, `string.digits`, and `string.punctuation`) to append to the base key, thus completing the AES key.
   - For each potential key, we attempted to decrypt the ciphertext (`c2_hex`), using the AES ECB mode.
   - We then used XOR operations to decrypt `c2` using the derived key, followed by another XOR to match the partial message `p2`.

3. **Key Generation**:
   - By appending two characters (`ch1` and `ch2`) from the character set to the base key, we generated potential AES keys and decrypted the ciphertext iteratively.

4. **IV Extraction**:
   - After successfully decrypting the ciphertext and obtaining a decrypted block (`c1`), we used another XOR operation with `p1` to retrieve the IV.

5. **Flag Identification**:
   - The IV was checked to see if it contained the substring `b"hacks"`, which led us to the correct key and IV combination.

### Solution Code:
```python
from Crypto.Cipher import AES
from pwn import xor
import string

base_key = b'lnmhacks87AB$$'  
c2_hex = '1fd124436d6d503d7fe7bca2fbd3d6b1'
p1 = b'The message is p'
p2 = b'rotected by AES!'

c2 = bytes.fromhex(c2_hex)

chars = string.ascii_letters + string.digits + string.punctuation
found = False

for ch1 in chars:
    for ch2 in chars:
        
        key = base_key + ch1.encode() + ch2.encode()

        aes = AES.new(key, AES.MODE_ECB)
        decrypted_c2 = aes.decrypt(c2)

        c1 = xor(decrypted_c2, p2)

        decrypted_c1 = aes.decrypt(c1)

        iv = xor(decrypted_c1, p1)

        if b"hacks" in iv:
            print("Key:", key.decode())
            print("IV:", iv)
            found = True
            break
    if found:
        break
```

### Conclusion:
By iterating through all possible key combinations and applying XOR decryption with the known partial messages, we successfully retrieved the AES initialization vector (IV). The IV revealed the flag, which contained the substring `hacks`, indicating the correct key and IV combination.

### Flag:
hacks{1V_H1dd3n}
