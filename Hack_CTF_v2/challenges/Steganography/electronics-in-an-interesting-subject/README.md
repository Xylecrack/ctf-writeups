# Electronics in an interesting subject

## Description

I was given this file. But it looks pretty weird to me!

## Files

* [test.png](<files/test.png>)

### Steps Followed:

1. **Inspect the Image**:  
   - Opened the provided image `test.png` using the Python Imaging Library (PIL):
     ```python
     from PIL import Image
     import numpy as np

     image_path = 'test.png'  
     image = Image.open(image_path)
     ```

2. **Extract the Blue Channel**:  
   - Converted the image to RGB mode and extracted the blue channel values:
     ```python
     rgb_image = image.convert('RGB')
     pixels = np.array(rgb_image)
     blue_pixels = pixels[:, :, 2]
     ```

3. **Flatten the Blue Pixels**:  
   - Flattened the blue channel pixels into a one-dimensional list for easier processing:
     ```python
     blue_pixels_flat = blue_pixels.flatten()
     ```

4. **Decode the Flag**:  
   - Noticed that the pixel values were encoded using a simple Caesar cipher (shift of -13).
   - Decoded the first 17 characters from the blue pixel values using this shift:
     ```python
     flag = [chr(blue_pixels_flat[i] - 13) for i in range(0, 17)]
     ```

5. **Output the Final Flag**:
   - Joined the decoded characters and printed the flag:
     ```python
     print(''.join(flag))
     ```

### Final Flag:
hacks{eAsY_Pe4Sy}
