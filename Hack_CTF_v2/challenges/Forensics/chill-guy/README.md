# Chill guy

## Description

what secrets lie within this file?

## Files

* [chill_guy.tar.gz](<files/chill_guy.tar.gz>)

### Steps Followed:

1. Extract the provided `chill_guy.tar.gz` file:
   - Command: `tar -xvzf chill_guy.tar.gz`
2. Two files were extracted, one of which was named `randomfile`.
3. Analyze `randomfile`:
   - Identified it as a JPEG file missing the first 8 bytes of the JPEG header.
4. Fix the file by adding the JPEG header bytes:
   - Add the following bytes to the beginning of the file: `FFD8 FFE0 0010 4A46`.
   - Use a hex editor or a tool like `xxd` for this step.
5. Save the modified file as a `.jpg` and verify it is a valid image.
6. Use `stegseek` to brute force the password from the modified JPEG file:
   - Command: `stegseek randomfile.jpg rockyou.txt`
7. Output from `stegseek`:
   - **Found passphrase:** `"blacksmith"`
   - **Original filename:** `"flag.txt"`
8. Extract `flag.txt` using the passphrase to retrieve the flag.

### Final Flag:
Hacks{4re_y0u_4_ch1ll_guy}





