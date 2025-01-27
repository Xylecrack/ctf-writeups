# Too many cards

## Description

A list of 100 possible credit card numbers has been intercepted, but only one of them is valid. The valid number, however, was encoded to keep it hidden from prying eyes.



Your mission:

Decode each credit card number to reveal its original form.

Identify the valid credit card number from the decoded list using a standard verification method.

Finally, submit the original, unencoded number as the flag.



Flag Format: hacks{xxxx-xxxx-xxxx-xxxx}



## Files

* [credit.txt](<files/credit.txt>)

* [Question_creditcard.txt](<files/Question_creditcard.txt>)

## Challenge Writeup: Decode Credit Card Number

### Steps Followed:

1. **Inspect the `credit.txt` file**:  
   - The file contains encoded credit card numbers, one per line.

2. **Identify the Cipher**:  
   - After testing multiple ciphers, it was discovered that the credit card numbers are encoded using **ROT-13**.

3. **Decode the Credit Card Number**:  
   - A function was created to decode the ROT-13 encoded string:
     ```python
     def decode_cc(encoded_cc):
         hex_string = encoded_cc.translate(str.maketrans(
             'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ',
             'nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZABCDEFGHIJKLM'
         ))
         return str(int(hex_string, 0))
     ```
   - The `translate` function was used to perform the ROT-13 transformation.

4. **Verify the Validity of Credit Card Number**:  
   - The **Luhn Algorithm** was used to validate the decoded credit card numbers:
     ```python
     def is_valid_luhn(cc_number):
         total = 0
         reversed_cc = cc_number[::-1]
         for i in range(len(reversed_cc)):
             digit = int(reversed_cc[i])
             if i % 2 == 1:
                 doubled = digit * 2
                 total += (doubled // 10) + (doubled % 10)
             else:
                 total += digit
         return total % 10 == 0
     ```

5. **Process the `credit.txt` File**:
   - The file was read, and each line was decoded and validated:
     ```python
     with open('credit.txt', 'r') as file:
         encoded_numbers = file.readlines()

     encoded_numbers = [line.strip() for line in encoded_numbers]
     ```

6. **Format the Valid Credit Card Number**:
   - For the valid credit card number, it was formatted into groups of 4 digits, separated by dashes.

7. **Output the Final Flag**:
   - Once a valid number was found, it was printed in the flag format `hacks{xxxx-xxxx-xxxx-xxxx}`:
     ```python
     print(f"hacks{{{formatted}}}")
     ```

### Final Flag:
`hacks{8908-9089-0890-8908}`
