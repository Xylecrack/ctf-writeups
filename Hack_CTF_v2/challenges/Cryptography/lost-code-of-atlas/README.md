# Lost Code of Atlas

## Description

In a world governed by advanced technology and digital warfare, an ancient piece of code, known as the "Atlas Protocol," is said to hold the key to controlling all global networks. It was encrypted centuries ago by a secret society to protect humanity from falling under the control of a malevolent AI known only as The Shadow. But now, the code has been fragmented into pieces and hidden within the most secure digital vaults.



The global defense system, a group of elite hackers known as The Vanguard, has discovered the first clue to the Atlas Protocol's location, but the path ahead is fraught with danger. A notorious group of cyber criminals, The Black Hat Collective, seeks to unlock the Atlas Protocol and seize control of the world’s digital infrastructure for their own sinister purposes.



Both factions race to uncover the pieces of the Atlas Protocol, hidden deep within encrypted servers, firewalled systems, and virtual landscapes.The Vanguard must use their expertise in cryptography, reverse engineering, and digital infiltration to find and protect the scattered pieces of the Atlas Protocol before The Black Hat Collective can steal them.The fate of the world lies in the hands of those who can outsmart, outhack, and outmaneuver the opposition in this high-stakes. Help the Vanguards by decrypting this code.



The Vanguards found this written on a piece of paper: lovectf.lnmhacks

And this: 0CE4A410E54BA0C19B4D992922E938B2


### Clue:
The Vanguards found a piece of paper with the following clues:
- **Key**: `lovectf.lnmhacks`
- **Ciphertext**: `0CE4A410E54BA0C19B4D992922E938B2`

### Steps to Solve:

1. **Understanding the Cipher**:  
   The ciphertext `0CE4A410E54BA0C19B4D992922E938B2` is likely encrypted using **AES** in **CBC mode**, with the initialization vector (IV) set to all zero bytes. This is deduced from the absence of an IV in the provided data and the reference to AES encryption.

2. **AES Decryption with Provided Key**:  
   The key provided is `lovectf.lnmhacks`, and the ciphertext is in hexadecimal format. The decryption involves using this key with the AES algorithm in CBC mode.

3. **Unhexlify the Ciphertext**:  
   The hexadecimal ciphertext string is first converted into its byte representation using the `unhexlify` function from the `binascii` module.

4. **Unpad the Decrypted Data**:  
   AES encryption often uses padding to ensure the plaintext is a multiple of the AES block size (16 bytes). After decryption, the `unpad` function is used to remove any padding added during encryption.

5. **Decryption Code**:
   We use the `Crypto.Cipher.AES` module to decrypt the data with the provided key. The decryption is done using CBC mode and a zero IV (`b'\x00' * 16`).

### Code:

```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad
from binascii import unhexlify

ciphertext = unhexlify("0CE4A410E54BA0C19B4D992922E938B2")
key = b"lovectf.lnmhacks"

try:
    cipher = AES.new(key, AES.MODE_CBC, iv=b'\x00' * 16)
    decrypted = unpad(cipher.decrypt(ciphertext), AES.block_size).decode('utf-8')
except Exception as e:
    decrypted = str(e)

print(decrypted)
```

### Flag:
hacks{anel_cif}
