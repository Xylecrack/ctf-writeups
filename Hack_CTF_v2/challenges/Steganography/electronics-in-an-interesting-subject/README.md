# Electronics in an interesting subject

## Description

I was given this file. But it looks pretty weird to me!

## Files

* [test.png](<files/test.png>)

## Challenge Writeup: Decoding Image with Repeated Pixels

### Steps Followed:

1. **Inspect the Image**:  
   - Upon inspecting the image using **Aperisolve**, it was noticed that the blue channel had repeated pixels, which could be a clue to extracting the flag.

2. **Extract the Blue Channel**:  
   - The image was loaded and converted to the RGB mode using the **PIL** library:
     ```python
     from PIL import Image
     import numpy as np

     image_path = 'test.png'
     image = Image.open(image_path)
     rgb_image = image.convert('RGB')
     ```

3. **Isolate the Blue Channel**:  
   - The blue channel of the image was extracted by accessing the third dimension (index 2) of the pixel array:
     ```python
     pixels = np.array(rgb_image)
     blue_pixels = pixels[:, :, 2]
     ```

4. **Flatten the Array of Blue Pixels**:  
   - The blue channel was flattened into a one-dimensional array:
     ```python
     blue_pixels_flat = blue_pixels.flatten()
     ```

5. **Find Unique Blue Pixels**:  
   - Repeated pixels were removed by using a set to store unique blue pixel values:
     ```python
     seen = set()
     unique_blue_pixels = []
     for pixel in blue_pixels_flat:
         if pixel not in seen:
             seen.add(pixel)
             unique_blue_pixels.append(pixel)
     ```

6. **Apply Caesar Cipher Decryption**:  
   - A Caesar cipher with a shift of 13 (ROT13) was applied to decode the unique blue pixel values:
     ```python
     flag = [chr(unique_blue_pixels[i]-13) for i in range(len(unique_blue_pixels))]
     ```

7. **Print the Flag**:  
   - The decoded flag was printed:
     ```python
     print(''.join(flag))
     ```

### Final Flag:
hacks{eASY_P4Sy}
