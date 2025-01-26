# GTA 6

## Challenge Description

We got the first copy of GTA 6. Try and get a high score!

## Provided Files

- [GTA6](files/GTA6)

---

## Solution Walkthrough

### Step 1: Analyze the Challenge

This challenge involves a binary executable named `GTA6`. From the description, it appears to be a buffer overflow vulnerability.

### Step 2: Triggering the Buffer Overflow

When prompted to **"Enter your name in the leaderboard"**, input an excessive amount of text to trigger the buffer overflow.
![image](https://github.com/user-attachments/assets/47d02a8d-7d2e-4cf1-8579-707a0b47a753)


### Step 3: Revealing the Flag

After spamming a large amount of text in the leaderboard input field, open the leaderboard. The flag will be displayed:

```
Hacks{buffer_overflow_detected}
```
