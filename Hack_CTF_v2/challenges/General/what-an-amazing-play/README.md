# What an amazing play!

## Challenge Description

Oh no!!!! While writing this amazing play on a piece of paper, the scriptwriter accidentally dropped some water on it. We could only recover this much of the script. I think he was trying to convey a flag…… I meant a message through this play!! Can you uncover the message from this recovered script?

---

## Provided Files

- [Another_Great_CTF.txt](<files/Another_Great_CTF.txt>)

---

## Solution Walkthrough

### Step 1: Identify the Esoteric Language

The file contains code written in an esoteric programming language called Shakespeare Programming Language (SPL or Shakespearlang). It is designed to look like a play script.

### Step 2: Execute the Code

To execute the script, use an online interpreter for SPL. A suitable tool is [Esolang Park's SPL IDE](https://esolangpark.vercel.app/ide/shakespeare).

#### Initial Execution

Run the provided file [Another Great CTF Script](files/Another_Great_CTF.txt). The output from the first execution is:

```
hacks{
```

This suggests that the program is incomplete or missing instructions to print the rest of the flag.

### Step 3: Modify the Script

Inspect the script and notice several sections of code without "Speak your mind!" statements, which are equivalent to "return" or "printf" in SPL. To resolve this, add "Speak your mind!" at appropriate locations in the script.

#### Modified Script

Here is the [updated script](files/Another_Great_CTF_modified.txt):

### Step 4: Execute the Modified Script

Run the modified script using the same interpreter. The complete flag will be displayed:

```
hacks{3t_7U_8ru73?}
```
