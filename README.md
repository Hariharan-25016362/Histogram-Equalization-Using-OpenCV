# Histogram Equalization Using OpenCV (Grayscale & Color Images)

---

## Aim

To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image  
- Plot histogram of the grayscale image  
- Apply histogram equalization on grayscale image  
- Read and display a color image  
- Plot histogram of B, G, R channels  
- Convert image to HSV color space  
- Apply histogram equalization on the Value (V) channel  
- Convert the enhanced image back to BGR format  
- Display original and enhanced images with histograms  

---

## Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### Step 2:
Read the image `img4.png` in grayscale format.
```
gray = cv2.imread('img4.png', cv2.IMREAD_GRAYSCALE)
```

### Step 3:
Display the grayscale image and plot its histogram.
```
plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(gray, cmap='gray')
plt.title('Grayscale Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.hist(gray.ravel(), 256, [0, 256])
plt.title('Grayscale Histogram')

plt.show()
```

### Step 4:
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.
```
equalized = cv2.equalizeHist(gray)
```
### Step 5:
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.
```
plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.imshow(gray, cmap='gray')
plt.title('Original Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.hist(gray.ravel(), 256, [0, 256])
plt.title('Original Histogram')

plt.subplot(2, 2, 3)
plt.imshow(equalized, cmap='gray')
plt.title('Equalized Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.hist(equalized.ravel(), 256, [0, 256])
plt.title('Equalized Histogram')

plt.tight_layout()
plt.show()
```
### Step 6:
Read the same image in color format.
```
img = cv2.imread('img4.png')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Color Image')
plt.axis('off')
plt.show()
```
### Step 7:
Split the image into B, G, R channels and plot their histograms.
```
b, g, r = cv2.split(img)

plt.figure(figsize=(8, 5))

plt.hist(b.ravel(), 256, [0, 256], color='blue', label='Blue')
plt.hist(g.ravel(), 256, [0, 256], color='green', label='Green')
plt.hist(r.ravel(), 256, [0, 256], color='red', label='Red')

plt.title('BGR Histogram')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')
plt.legend()
plt.show()
```
### Step 8:
Convert the image from BGR to HSV color space.
```
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

h, s, v = cv2.split(hsv)
```
### Step 9:
Apply histogram equalization on the V (Value) channel.
```
v_equalized = cv2.equalizeHist(v)
```
### Step 10:
Merge the channels and convert the image back to BGR format.
```
hsv_equalized = cv2.merge((h, s, v_equalized))

enhanced = cv2.cvtColor(hsv_equalized, cv2.COLOR_HSV2BGR)
```
### Step 11:
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.
```
plt.figure(figsize=(12, 8))

plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Color Image')
plt.axis('off')

plt.subplot(2, 2, 2)
for channel, color, name in zip(cv2.split(img),
                                 ['blue', 'green', 'red'],
                                 ['Blue', 'Green', 'Red']):
    hist = cv2.calcHist([img], [ [ 'Blue', 'Green', 'Red' ].index(name) ],
                        None, [256], [0, 256])
    plt.plot(hist, color=color, label=name)

plt.title('Original Color Histogram')
plt.legend()

plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(enhanced, cv2.COLOR_BGR2RGB))
plt.title('Enhanced Color Image')
plt.axis('off')

plt.subplot(2, 2, 4)
for i, color in enumerate(['blue', 'green', 'red']):
    hist = cv2.calcHist([enhanced], [i], None, [256], [0, 256])
    plt.plot(hist, color=color, label=color.capitalize())

plt.title('Enhanced Color Histogram')
plt.legend()

plt.tight_layout()
plt.show()
```
---

## Program

### Developed By:
**Name:** HARIHARAN M 

### Register No:
212225240045

---

##  Output

### Grayscale Histogram Equalization

- Original grayscale image is displayed

  <img width="398" height="325" alt="image" src="https://github.com/user-attachments/assets/88e1524e-c7ca-4eb9-8646-ba15821b6e61" />


  
 
- Histogram of original grayscale image is plotted

  <img width="466" height="407" alt="image" src="https://github.com/user-attachments/assets/242aa8a9-068f-447e-a279-7d1637e7c5bf" />


  

- Enhanced image after histogram equalization is displayed

  <img width="505" height="406" alt="image" src="https://github.com/user-attachments/assets/32fe14cf-85e5-4487-966b-b96083ec228e" />


   

- Histogram of enhanced grayscale image shows improved contrast

  <img width="558" height="443" alt="image" src="https://github.com/user-attachments/assets/4844695b-fc32-4135-99df-1600e5f53dae" />


  


### Color Image Histogram Equalization

- Original color image is displayed

  <img width="482" height="387" alt="image" src="https://github.com/user-attachments/assets/f497f405-acd0-4530-9d58-e6df1be9a6fd" />


   

- Histogram of B, G, R channels is plotted

  <img width="668" height="437" alt="image" src="https://github.com/user-attachments/assets/012f0b09-322d-4892-bc88-3ac37563d9c6" />


  

- Enhanced image after HSV-based equalization is displayed

  <img width="480" height="395" alt="image" src="https://github.com/user-attachments/assets/f888d623-9c20-40d7-8447-b7b7108b5816" />


  

- Histogram of enhanced image shows better intensity distribution

  <img width="667" height="426" alt="image" src="https://github.com/user-attachments/assets/f82c07ce-b3db-4ca3-a45b-8c4c937b952f" />


 


---

## Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
