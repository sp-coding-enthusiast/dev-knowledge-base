# Mini Image Processing Cheat Sheet – OpenCV

Concise, high‑impact concepts and formulas for **quick revision and interviews**.

---

## 1. Image Representation

* Images are **numerical matrices (arrays)**, not pictures.
* Stored typically as `uint8` values.

```
Image → NumPy array
Shape → (Height, Width, Channels)
```

This allows **mathematical operations** directly on images.

---

## 2. uint8 Data Type (Critical Concept)

* Unsigned 8‑bit integer
* Value range:

```
0 to 255
```

### Overflow / Underflow

```
255 + 1 = 0
0 - 1   = 255
```

⚠️ Arithmetic order and casting **change results significantly**.

---

## 3. Basic Arithmetic Operations

### Addition

```python
result = image1 + image2
```

* Can overflow due to `uint8`
* Prefer OpenCV safe add:

```python
result = cv2.add(image1, image2)
```

---

### Averaging

Two common approaches:

```python
avg1 = image1 // 2 + image2 // 2
avg2 = (image1 + image2) // 2
```

* Results differ due to **integer truncation**
* Best practice:

```python
avg = cv2.addWeighted(image1, 0.5, image2, 0.5, 0)
```

---

### Multiplication (Brightness Control)

```python
bright = image * scalar
```

⚠️ Must clamp values:

```python
bright = np.clip(image * scalar, 0, 255).astype(np.uint8)
```

---

## 4. Image Blending

### Formula

```
Blended = α × img1 + (1 − α) × img2
```

### OpenCV

```python
blended = cv2.addWeighted(img1, alpha, img2, beta, gamma)
```

* `alpha + beta = 1`
* `gamma` → brightness offset

---

## 5. Image Differencing

Used to **detect changes** between two images.

```python
diff = cv2.subtract(img1, img2)
```

### Highlighting Differences

```python
diff[gray > 5] = [0, 0, 255]
```

(Common in motion detection & quality inspection)

---

## 6. Masking

Mask = image that selects **specific pixels** based on conditions.

```python
mask = gray > 5
```

Applications:

* Object isolation
* Region-based editing
* Highlighting defects

---

## 7. Bitwise Operations

Operate on **binary pixel representations**.

### NOT

```python
inv = cv2.bitwise_not(mask)
```

### AND (Intersection)

```python
res = cv2.bitwise_and(mask1, mask2)
```

### OR (Union)

```python
res = cv2.bitwise_or(mask1, mask2)
```

---

## 8. Thresholding

Converts grayscale image to binary mask.

### Formula

```
Pixel ≥ threshold → maxVal
Else              → 0
```

### OpenCV

```python
_, binary = cv2.threshold(image, thresh, maxval, type)
```

---

## 9. Normalization

Scales pixel values to a standard range.

### Formula

```
I_norm = I / 255
```

Used in **ML / DL pipelines**.

---

## 10. Utility Functions (Best Practice)

### Display Image Correctly

```python
show_image(img, fig_size=None)
```

Handles:

* BGR → RGB
* Scaling
* Matplotlib compatibility

---

### Normalize Image

```python
normalize_image(img)
```

Used for:

* Training models
* Stable numerical computation

---

## 11. Extra Must‑Know Formulas (Interview Gold)

### Grayscale Conversion

```
Gray = 0.299R + 0.587G + 0.114B
```

---

### Image Inversion

```
I_inv = 255 − I
```

---

### Mean Blur

```
I'(x, y) = average of neighboring pixels
```

---

## 12. One‑Line Summary

> Image processing in OpenCV is **safe and unsafe arithmetic on uint8 matrices combined with masking and bitwise logic**.

---

