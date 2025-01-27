# What's a MACRO???

## Challenge Description

Someone just sent me this PowerPoint Presentation. I am unable to understand the intention of the file. Your task is to find the flag hidden in this PPT.

---

## Provided Files

- [file.pptm](<files/file.pptm>)

---

## Solution Walkthrough

### Step 1: Extract the Contents of the `.pptm` File

The provided file is a `.pptm` file, which is a PowerPoint Presentation with macros enabled. To analyze it, I used `binwalk` to extract the file contents.
### Step 2: Analyze the Macro Files
To efficiently analyze all the macro files, I wrote the following Python script. This script iterates through all directories and files, extracting unique content from files named macro.vba.
```
import os

def extract_unique_macros(base_dir):
    """
    Extract and display unique contents from all macro.vba files.
    :param base_dir: Base directory containing the maliciousMacroDetails folders.
    """
    unique_contents = set()  # To store unique macro contents
    # Walk through the base directory to find macro.vba files
    for root, dirs, files in os.walk(base_dir):
        for file in files:
            if file == "macro.vba":
                file_path = os.path.join(root, file)
                try:
                    # Read the contents of the macro.vba file
                    with open(file_path, "r", encoding="utf-8", errors="ignore") as f:
                        content = f.read().strip()
                        unique_contents.add(content)  # Add to the set for uniqueness
                except Exception as e:
                    print(f"Error reading file {file_path}: {e}")

    # Display the unique contents
    print("\nUnique Macro Contents:")
    for idx, content in enumerate(unique_contents, 1):
        print(f"\n--- Macro {idx} ---\n{content}")

if __name__ == "__main__":
    base_directory = "./"  # Replace with the actual base directory path 
    extract_unique_macros(base_directory)
```
### Step 3: Run the Script
Running the script on the extracted directory displayed unique macro contents. One of the macros contained hex-encoded text.
![image](https://github.com/user-attachments/assets/100aeb5c-faf7-4664-b58c-3f87ff02e4f5)

Decoding the output 
```
print(bytes.fromhex("6861636b737b7930755f6630756e444d337d").decode("utf-8"))
```
gives `hacks{y0u_f0unD_M3}`
