# Image Processing – Important Formulas & Concepts (OpenCV Focus)

This document summarizes **core concepts, formulas, and practical notes** you must know for **image processing using OpenCV**, especially useful for **interviews and hands-on work**.

---

## 1. Image Representation as a Function

A digital image can be mathematically represented as a function:

```
I(x, y)
```

* `x` → horizontal coordinate (column)
* `y` → vertical coordinate (row)
* `I(x, y)` → intensity (brightness or color value) at that pixel

For grayscale images:

```
I(x, y) ∈ [0, 255]
```

For color images:

```
I(x, y) = [B, G, R]
```

---

## 2. Image as a Numerical Matrix

An image is stored as a **3D numerical array (matrix)**:

```
Image shape = (rows, columns, channels)
```

* **Rows** → height of image
* **Columns** → width of image
* **Channels** → color information per pixel

### Examples

* Grayscale image → `(H, W)`
* Color image (OpenCV) → `(H, W, 3)`

Accessing a pixel:

```python
pixel = image[y, x]
```

---

## 3. Pixel Intensity Values (OpenCV – BGR)

In OpenCV, color images use **BGR format**:

```
[B, G, R]
```

Each value ranges from:

```
0 → no intensity
255 → full intensity
```

### Example

```
[247, 247, 247] → almost white
[0, 0, 0]       → black
[255, 0, 0]     → blue (not red!)
```

---

## 4. uint8 Data Type Behavior (Very Important)

Most images are stored as `uint8` (unsigned 8-bit integers).

### Range

```
0 to 255
```

### Overflow & Underflow

```
255 + 1 = 0
0 - 1   = 255
```

⚠️ This is **NOT a bug** — it is how unsigned integers work.

---

## 5. Color Space Conversion (BGR ↔ RGB)

* OpenCV reads images in **BGR** format
* Matplotlib expects **RGB** format

### Conversion Formula

```python
rgb_image = cv2.cvtColor(bgr_image, cv2.COLOR_BGR2RGB)
```

Without conversion, colors will look **incorrect** when displayed using `matplotlib`.

---

## 6. Grayscale Conversion Formula

Converting a color image to grayscale is done using weighted sum:

```
Gray = 0.299R + 0.587G + 0.114B
```

OpenCV implementation:

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

## 7. Image Normalization

Used to scale pixel values to a fixed range (commonly 0–1).

### Formula

```
I_normalized = I / 255
```

Used heavily in **machine learning and deep learning**.

---

## 8. Image Resizing

Changes image dimensions.

### OpenCV Function

```python
resized = cv2.resize(image, (new_width, new_height))
```

### Interpolation Methods

* `INTER_LINEAR` → default (good for resizing up/down)
* `INTER_NEAREST` → fastest, blocky
* `INTER_CUBIC` → high-quality (slower)

---

## 9. Image Thresholding

Used to convert grayscale images into binary images.

### Formula

```
T(x, y) =
  255  if I(x, y) ≥ threshold
  0    otherwise
```

### OpenCV

```python
_, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
```

---

## 10. Image Blurring (Smoothing)

Used to reduce noise.

### Mean Blur

```
I'(x, y) = average of neighboring pixels
```

```python
blur = cv2.blur(image, (5, 5))
```

### Gaussian Blur (Most Common)

```python
blur = cv2.GaussianBlur(image, (5, 5), sigmaX=0)
```

---

## 11. Edge Detection (Sobel Operator)

Detects edges using gradients.

### Gradient Formulas

```
Gx = dI/dx
Gy = dI/dy
```

Magnitude:

```
G = √(Gx² + Gy²)
```

OpenCV:

```python
sobelx = cv2.Sobel(gray, cv2.CV_64F, 1, 0)
sobely = cv2.Sobel(gray, cv2.CV_64F, 0, 1)
```

---

## 12. Canny Edge Detection

Multi-stage edge detection algorithm.

```python
edges = cv2.Canny(gray, threshold1, threshold2)
```

Key idea:

* Finds **strong + weak edges**
* Suppresses noise

---

## 13. Image Histogram

Shows distribution of pixel intensities.

### Formula Concept

```
Histogram[i] = number of pixels with intensity i
```

OpenCV:

```python
hist = cv2.calcHist([gray], [0], None, [256], [0, 256])
```

---

## 14. Histogram Equalization

Improves image contrast.

```python
equalized = cv2.equalizeHist(gray)
```

---

## 15. Key Interview Takeaways

* Images are **matrices, not pictures**
* Pixel operations are **numerical operations**
* OpenCV uses **BGR**, not RGB
* `uint8` overflow is **expected behavior**
* Most image processing = **matrix math + filters**

---

## 16. One-Line Summary

> Image processing in OpenCV is about **manipulating numerical matrices using mathematical operations to extract or enhance visual information**.

---
