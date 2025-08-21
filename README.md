# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** G.Ramanujam 
- **Register Number:** 212224240129

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
img=cv2.imread("Eagle_in_Flight.jpg",0)
```

#### 2. Print the image width, height & Channel.
```python
img.shape
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img)
plt.title('BGR Image')
plt.axis('on')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
img_save=cv2.imread('Eagle_in_Flight.jpg')
cv2.imwrite('Eagle.png',img_save)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img=cv2.imread('Eagle.png')
img_rgb=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
img_save=cv2.imread('Eagle_in_Flight.jpg')
cv2.imwrite('Eagle.png',img_save)
plt.imshow(img_rgb)
plt.show()
img_rgb.shape
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = img_rgb[0:450,200:550] 
plt.imshow(crop[:,:,::1])
plt.title("Cropped Region")
plt.axis("off")
plt.show()
crop.shape
```

#### 8. Resize the image up by a factor of 2x.
```python
res=cv2.resize(crop,None,fx=50,fy=50,interpolation=cv2.INTER_LINEAR)
```

#### 9. Flip the cropped/resized image horizontally.
```python
flipped_img=cv2.flip(crop,1)
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
plt.imshow(flipped_img[:,:,::1])
plt.title("Flipped image")
plt.axis('off')
plt.show()
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text=cv2.putText(img_rgb,"ramanujam",(200,50),cv2.FONT_HERSHEY_SIMPLEX,2,(255,255,255),2)
plt.imshow(text)
plt.title('New Image')
plt.show()
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rcol= (255, 0, 255)
cv2.rectangle(img_rgb, (400, 100), (800, 650), rcol, 3)
```

#### 13. Display the final annotated image.
```python
plt.title("Annotated image")
plt.imshow(img_rgb)
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img =cv2.imread('Eagle_in_Flight.jpg',cv2.IMREAD_COLOR)
img_rgb= cv2.cvtColor(img, cv2.COLOR_BGR2RGB) 
```

#### 15. Adjust the brightness of the image.
```python
m = np.ones(img_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img_rgb, m)  
img_darker = cv2.subtract(img_rgb, m)  
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_brighter), plt.title("Brighter Image"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_darker), plt.title("Darker Image"), plt.axis("off")
plt.show()
```

#### 18. Modify the image contrast.
```python
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2
img_higher1 = cv2.multiply(img.astype("float32"), matrix1).clip(0,255).astype("uint8")
img_higher2 = cv2.multiply(img.astype("float32"), matrix2).clip(0,255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_higher1), plt.title("Higher Contrast (1.1x)"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_higher2), plt.title("Higher Contrast (1.2x)"), plt.axis("off")
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(b, cmap='gray'), plt.title("Blue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(g, cmap='gray'), plt.title("Green Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(r, cmap='gray'), plt.title("Red Channel"), plt.axis("off")
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(h, cmap='gray'), plt.title("Hue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(s, cmap='gray'), plt.title("Saturation Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(v, cmap='gray'), plt.title("Value Channel"), plt.axis("off")
plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.cvtColor(cv2.merge([h, s, v]), cv2.COLOR_HSV2RGB)
combined = np.concatenate((img_rgb, merged_hsv), axis=1)
plt.figure(figsize=(10, 5))
plt.imshow(combined)
plt.title("Original Image  &  Merged HSV Image")
plt.axis("off")
plt.show()
```

## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.


<img width="701" height="544" alt="Screenshot 2025-08-21 140442" src="https://github.com/user-attachments/assets/42f27cb5-df31-470a-8fb9-78392e3d3f7a" />

<img width="416" height="534" alt="Screenshot 2025-08-21 140500" src="https://github.com/user-attachments/assets/08965494-9d52-4566-b501-e8b057d45e56" />

<img width="398" height="527" alt="Screenshot 2025-08-21 140509" src="https://github.com/user-attachments/assets/b27f5fb2-9b86-4bdb-9e75-f32322de1161" />

<img width="751" height="549" alt="Screenshot 2025-08-21 140524" src="https://github.com/user-attachments/assets/f5f94a86-3e87-4c70-8146-644bf026d8e9" />

<img width="710" height="555" alt="Screenshot 2025-08-21 140542" src="https://github.com/user-attachments/assets/f1d2be20-c596-499f-b5b3-a351b85b2e20" />

<img width="894" height="269" alt="Screenshot 2025-08-21 140554" src="https://github.com/user-attachments/assets/4dbc58f3-c78f-4931-9b08-4f6d5b72e1e0" />

<img width="888" height="274" alt="Screenshot 2025-08-21 140604" src="https://github.com/user-attachments/assets/54d2c68b-aa63-4edc-ab2c-bf1d6a61a097" />

<img width="889" height="258" alt="Screenshot 2025-08-21 140643" src="https://github.com/user-attachments/assets/0d480545-46e7-46c2-83ea-dc5d35243f00" />

<img width="523" height="459" alt="Screenshot 2025-08-21 140653" src="https://github.com/user-attachments/assets/26bc03c8-de26-49bd-aa86-5e50a20c340a" />

<img width="897" height="266" alt="Screenshot 2025-08-21 140708" src="https://github.com/user-attachments/assets/c02f2ef9-c420-480d-bfc4-c0e9e9f0bb2e" />

<img width="909" height="382" alt="Screenshot 2025-08-21 140723" src="https://github.com/user-attachments/assets/e1fa03ac-33e3-4041-993d-d1a1b24d75a4" />


## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

