# Obfuscated Life

## Challenge Description

Obfuscated with your life? Get the solution below ;D

---

## Files

- [hacks.js](<files/hacks.js>)

---

## Solution 

### Analyze the Obfuscated Code

The provided file `hacks.js` contains obfuscated JavaScript code. To make it readable, I used an online deobfuscation tool: [Obfuscator.io Deobfuscator](https://obf-io.deobfuscate.io/).

After deobfuscating the code, I got the following output:

```javascript
function hi() {
  if (document.domain == "obfuscator.io") {
    console.log("hacks{don't_be_a_obfuscated_nerd}");
  }
  console.log("Hmmmm I wonder where the flag is?");
}
hi();
```
## Complete Flag

hacks{don't_be_a_obfuscated_nerd}
