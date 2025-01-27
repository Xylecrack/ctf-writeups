# ?? Encrypted

## Description

I found this file but no decryption anywhere seems to work and

now they are whispering that this can even run.

RUN, WALK, FLY??? Just get out of your shell...

## Files

* [BigBang](<files/BigBang>)

## Challenge Writeup: BingBang

### Steps Followed:

1. **Inspect the Provided File**:  
   - The challenge provided a PDF file which contained a hex string. After further investigation, it was discovered that the hex string was 32-bit bytecode.

2. **Disassemble the Bytecode**:  
   - Used `ndisasm` to disassemble the bytecode:
     ```bash
     ndisasm -b 32 code.bin
      00000000  31C0              xor eax,eax
      00000002  50                push eax
      00000003  682A6F2E67        push dword 0x672e6f2a
      00000008  68292B2B45        push dword 0x452b2b29
      0000000D  6829452F72        push dword 0x722f4529
      00000012  686E452E72        push dword 0x722e456e
      00000017  6869617D29        push dword 0x297d6169
      0000001C  68727B7971        push dword 0x71797b72
      00000021  B918000000        mov ecx,0x18
      00000026  8D3424            lea esi,[esp]
      00000029  89E7              mov edi,esp
      0000002B  AC                lodsb
      0000002C  341A              xor al,0x1a
      0000002E  AA                stosb
      0000002F  E2FA              loop 0x2b
      00000031  B804000000        mov eax,0x4
      00000036  BB01000000        mov ebx,0x1
      0000003B  89E1              mov ecx,esp
      0000003D  BA18000000        mov edx,0x18
      00000042  CD80              int 0x80
      00000044  B801000000        mov eax,0x1
      00000049  31DB              xor ebx,ebx
      0000004B  CD80              int 0x80
      0000004D  64333432          xor esi,[fs:edx+esi]
      00000051  3438              xor al,0x38
      00000053  396537            cmp [ebp+0x37],esp
      00000056  61                popa
      00000057  6333              arpl [ebx],si
      00000059  3431              xor al,0x31
      0000005B  61                popa
      0000005C  61                popa
      0000005D  61                popa
      0000005E  65326661          xor ah,[gs:esi+0x61]
      00000062  6238              bound edi,[eax]
      00000064  303430            xor [eax+esi],dh
      00000067  3030              xor [eax],dh
      00000069  3030              xor [eax],dh
      0000006B  306262            xor [edx+0x62],ah
      0000006E  3031              xor [ecx],dh
      00000070  3030              xor [eax],dh
      00000072  3030              xor [eax],dh
      00000074  3030              xor [eax],dh
      00000076  3839              cmp [ecx],bh
      00000078  65316261          xor [gs:edx+0x61],esp
      0000007C  3138              xor [eax],edi
      0000007E  3030              xor [eax],dh
      00000080  3030              xor [eax],dh
      00000082  3030              xor [eax],dh
      00000084  63643830          arpl [eax+edi+0x30],sp
      00000088  6238              bound edi,[eax]
      0000008A  3031              xor [ecx],dh
      0000008C  3030              xor [eax],dh
      0000008E  3030              xor [eax],dh
      00000090  3030              xor [eax],dh
      00000092  3331              xor esi,[ecx]
      00000094  64626364          bound esp,[fs:ebx+0x64]
      00000098  3830              cmp [eax],dh
      0000009A  0A                db 0x0a
     ```
   - The disassembled code revealed a series of assembly instructions. The string is pushed onto stack and XOR'ed with `0x1a`.
    
3. **Extract the Encoded String**:  
   - From the disassembly, found the encoded string `*o.g)+)E)E/rnE.ria})r{yq` in the bytecode.

4. **Decode the String**:  
   - The string was XORed with the value `26`, which was observed in the bytecode. Used the following Python code to decode it:
     ```python
     s = "*o.g)+)E)E/rnE.ria})r{yq"
     h = ""
     for i in range(len(s)):
         h += chr(ord(s[i]) ^ 26)
     ```

5. **Reformat the Decoded String**:  
   - The decoded string was split into chunks of 4 characters, reversed, and then joined to form the final flag:
     ```python
     chunks = [h[i:i+4] for i in range(0, len(h), 4)]
     flag = ''.join(chunks[::-1])
     ```

6. **Output the Flag**:
   - Printed the decoded flag:
     ```python
     print(flag)
     ```

### Final Flag:
hacks{g3t_4h3_5h313_0u4}
