# Image Filtering & Edge Detection – OpenCV

A **compact, concept-first guide** to image filtering and edge detection with **formulas, intuition, and OpenCV methods**.

---

## 1. Image Filtering – General Concept

* Image filters (kernels) are **small matrices** applied to images.
* Filtering is done using **convolution**.

### Convolution Formula

```
I'(x, y) = Σ Σ I(x − i, y − j) · K(i, j)
```

Where:

* `I` → input image
* `K` → kernel/filter
* `I'` → filtered image

Used for:

* Blurring
* Sharpening
* Edge detection

---

## 2. Average Filtering (Mean Blur)

### Concept

* Replaces each pixel with the **average of its neighbors**
* Smooths intensity variations
* Reduces noise but **blurs edges**

### Kernel Example (5×5)

```
K = (1 / 25) × ones(5, 5)
```

### OpenCV Method

```python
kernel = np.ones((5,5)) / 25
blur = cv2.filter2D(image, -1, kernel)
```

---

## 3. Gaussian Filtering (Smooth Blur)

### Concept

* Weighted average using **Gaussian distribution**
* Nearby pixels contribute more
* Produces **natural-looking blur**

### Gaussian Formula

```
G(x, y) = (1 / 2πσ²) · e^{-(x² + y²) / (2σ²)}
```

### OpenCV Method

```python
blur = cv2.GaussianBlur(image, (5,5), 0)
```

---

## 4. Median Filtering (Salt & Pepper Noise Removal)

### Concept

* Replaces pixel with **median value** in neighborhood
* Excellent for removing **salt & pepper noise**
* Preserves edges better than mean blur

### OpenCV Method

```python
median = cv2.medianBlur(image, 5)
```

---

## 5. Bilateral Filtering (Edge-Preserving Blur)

### Concept

* Considers:

  * Spatial closeness
  * Intensity similarity
* Smooths regions **without blurring edges**

### Bilateral Formula (Conceptual)

```
I'(p) = Σ I(q) · f(|p−q|) · g(|I(p)−I(q)|)
```

### OpenCV Method

```python
bilateral = cv2.bilateralFilter(image, 5, 50, 50)
```

---

## 6. Denoising (Salt & Pepper Noise)

### Concept

* Noise appears as random white and black pixels
* Median filter is most effective

### Example Flow

```python
noisy = imnoise(img, dens, method='salt & pepper')
denoised = cv2.medianBlur(noisy, 3)
```

---

## 7. Edge Detection – General Concept

Edges are detected by finding **sharp intensity changes**.

Mathematically:

* First derivative → gradients
* Second derivative → zero crossings

---

## 8. Sobel Filtering (First Derivative)

### Concept

* Computes image gradients
* Detects **edge strength and direction**

### Sobel Kernels

```
Gx → vertical edges
Gy → horizontal edges
```

### Gradient Magnitude

```
G = √(Gx² + Gy²)
```

### OpenCV Method

```python
sobelx = cv2.Sobel(blurred, cv2.CV_64F, 1, 0, ksize=5)
sobely = cv2.Sobel(blurred, cv2.CV_64F, 0, 1, ksize=5)

sobelx = cv2.convertScaleAbs(sobelx)
sobely = cv2.convertScaleAbs(sobely)
```

---

## 9. Laplacian Filtering (Second Derivative)

### Concept

* Detects edges in **all directions**
* Sensitive to noise
* Highlights fine details

### Laplacian Formula

```
∇²I = ∂²I/∂x² + ∂²I/∂y²
```

### OpenCV Method

```python
laplacian = cv2.Laplacian(blurred, cv2.CV_64F)
```

---

## 10. Canny Edge Detection (Optimal Detector)

### Concept

Multi-stage algorithm:

1. Gaussian smoothing
2. Gradient calculation (Sobel)
3. Non-maximum suppression
4. Hysteresis thresholding

### OpenCV Method

```python
edges = cv2.Canny(blurred, 60, 20)
```

* Lower threshold → weak edges
* Upper threshold → strong edges

---

## 11. Extra Important Formulas (Interview Gold)

### Image Sharpening (Unsharp Masking)

```
Sharpened = Original + α · (Original − Blurred)
```

---

### Gradient Direction

```
θ = tan⁻¹(Gy / Gx)
```

---

### Noise Model (Salt & Pepper)

```
Pixel → 0 or 255 with probability p
```

---

## 12. Key Takeaway

> Filtering = **convolution + statistics**, edge detection = **derivatives of intensity**.

---

**Visual examples (before/after)**
