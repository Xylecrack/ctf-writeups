# Gamer Lights = More FPS

## Description

I always get the **unlucky number** in lottery :(

But this time I got this image, and if I can crack the flag I will get more RGB lightings for my PC setup!

Please help me...

## Files

* [rgb.png](<files/rgb.png>)

### Steps Followed:

Add the image to cyberchef, and split color channels. blue.png has less size than the other two, so it has been altered.
![image](https://github.com/user-attachments/assets/2e7932b4-0d0c-4f58-9701-20fe1b8f3f74)

1. Load the provided image `rgb.png` using the Python Imaging Library (PIL):
   ```python
   from PIL import Image
   import numpy as np

   image_path = 'rgb.png'  
   image = Image.open(image_path)
   ```
2. Convert the image to RGB mode:
   ```python
   rgb_image = image.convert('RGB')
   ```
3. Convert the image to a NumPy array for pixel manipulation:
   ```python
   pixels = np.array(rgb_image)
   ```
4. Extract the blue pixel values (third channel):
   ```python
   blue_pixels = pixels[:, :, 2]
   ```
5. Flatten the array of blue pixels into a one-dimensional list:
   ```python
   blue_pixels_flat = blue_pixels.flatten()
   ```
6. Identify unique blue pixel values:
   ```python
   seen = set()
   unique_blue_pixels = []
   for pixel in blue_pixels_flat:
       if pixel not in seen:
           seen.add(pixel)
           unique_blue_pixels.append(pixel)
   ```
7. Convert the unique blue pixel values to ASCII characters (only values below 128 are valid ASCII):
   ```python
   flag = ''.join(chr(pixel) for pixel in unique_blue_pixels if pixel < 128)
   ```
8. Print the final flag:
   ```python
   print("ASCII representation of unique blue pixels:")
   print(flag)
   ```

### Final Flag:
hacks{rgb_gives_you_extra_fps}
