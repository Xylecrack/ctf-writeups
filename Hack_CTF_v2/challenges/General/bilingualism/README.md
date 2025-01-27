# Bilingualism

## Description

I can speak two languages! How cool is that? But can you understand both of them?

## Files

* [Bilingualism.txt](<files/Bilingualism.txt>)

## Challenge Writeup: Bilingualism

### Steps Followed:

1. **Inspect the Provided File**:  
   - The challenge provided a file `Bilingualism.txt` that contained a mix of whitespace and a JavaScript script.

2. **Analyze the JavaScript Script**:  
   - Upon inspection, it was found that in the JavaScript:
     - `i` represents the **tab** character.
     - `j` represents the **space** character.
     - `k` represents the **newline** character.

3. **Interpret the Whitespace**:  
   - The JavaScript code outputs a sequence using these whitespace characters, which when decoded gives:
     ```plaintext
     hacks{	 	 
	 

 	}
     ```

4. **Replace the Variables**:  
   - Replaced the characters `i`, `j`, and `k` with their respective whitespace characters:
     - `i` becomes a **tab** (`\t`).
     - `j` becomes a **space** (` `).
     - `k` becomes a **newline** (`\n`).

5. **Output the Flag**:  
   - After replacing the variables, the flag is:
    ```python
    s = """hacks{	 	 
    	 
    
     	}"""
    
    print(s.replace("\t", "i").replace(" ", "j").replace("\n", "k"))     
    ```

### Final Flag:
hacks{ijijkijkkji}
