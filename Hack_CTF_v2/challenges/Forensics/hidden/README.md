# HIDDEN

## Description

Hidden deep within the file lies the flag. You might get distracted but keep yourself pointed in the right direction.

## Files

* [flag_1_1](<files/flag_1_1>)

## Challenge Writeup: flag_1_1

### Steps Followed:

1. The file `flag_1_1` was identified as **bzip2 compressed data**:
   - Command: `mv flag_1_1 flag_1_1.bz2`
2. Decompress the `flag_1_1.bz2` file:
   - Command: `bzip2 -d flag_1_1.bz2`
3. The decompressed file is identified as a **gzip compressed** file:
   - Command: `gzip -d < flag_1_1 > flag`
4. The resulting file `flag` was determined to be a **Microsoft Word 2007+** document.
5. Inspect the document to find the embedded image:
   - The image `image3.png` in the media folder has the highest size, so it likely contains the flag.
6. Extract the image from the document.
7. Upon inspection of the image's metadata, a strange sequence of text was found:
`meta Artist .. file: Unicode text, UTF-8 text, with no line terminators 00000000: 23 2003 20 20 2003 20 2003 2003 2003 2003 20 20 2003 2003 2003 2003 |#. . .... ....| 00000010: 20 2003 20 20 2003 2003 2003 20 20 2003 20 20 2003 20 2003 20 | . ... . . . | 00000020: 20 2003 20 20 20 2003 2003 20 20 2003 20 20 20 20 2003 20 | . .. . . | 00000030: 20 2003 20 20 20 2003 2003 20 20 2003 20 20 20 2003 20 2003 | . .. . . .| 00000040: 2003 2003 2003 20 20 2003 2003 20 20 2003 20 20 2003 2003 20 20 |... .. . .. | 00000050: 20 2003 20 20 2003 20 20 20 2003 2003 2003 20 20 2003 2003 2003 | . . ... ...| 00000060: 2003 2003 20 20 20 20 20 2003 20 23 |.. . # |`
![image](https://github.com/user-attachments/assets/b7ae2e8f-3ab4-4297-a722-3f86061453fd)
9. The hex values `2003` and `20` can be translated to binary as follows:
- `2003` is `0` and `20` is `1`.
9. The following Python script was used to process the data:
```python
s = '''meta Artist         .. file: Unicode text, UTF-8 text, with no line terminators
    00000000: 23 2003 20 20 2003 20 2003 2003  2003 2003 20 20 2003 2003 2003 2003  |#.  . ....  ....|
    00000010: 20 2003 20 20 2003 2003 2003 20  20 2003 20 20 2003 20 2003 20  | .  ...  .  . . |
    00000020: 20 2003 20 20 20 2003 2003 20  20 2003 20 20 20 20 2003 20  | .   ..  .    . |
    00000030: 20 2003 20 20 20 2003 2003 20  20 2003 20 20 20 2003 20 2003  | .   ..  .   . .|
    00000040: 2003 2003 2003 20 20 2003 2003 20  20 2003 20 20 2003 2003 20 20  |...  ..  .  ..  |
    00000050: 20 2003 20 20 2003 20 20 20  2003 2003 2003 20 20 2003 2003 2003  | .  .   ...  ...|
    00000060: 2003 2003 20 20 20 20 20 2003  20 23                    |..     . #      |'''
s = s.split()
o = ""
for i in s:
    if i == "2003":
        o += "0"
    elif i == "20":
        o += "1"
print(' '.join(o[i:i+8] for i in range(0, len(o), 8)))
```
10. The output from the script was used to uncover hidden binary data, leading to the final flag.
![image](https://github.com/user-attachments/assets/ff263d67-c457-40f7-af68-8c83a71e3b16)

### Final Flag:
hacks{st3gn0}
