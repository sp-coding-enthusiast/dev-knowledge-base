# Geometric Image Transformations – OpenCV & NumPy

This mini guide covers **core geometric transformations** used in image processing, with **concepts, formulas, and primary functions**. These are frequently tested in interviews and used in data augmentation.

---

## 1. Image Rotation

### Concept

* Changes the **orientation** of an image by a given angle
* Rotation is performed around a center point (usually the image center)

### Mathematical Idea

Rotation matrix:

```
R = [ cosθ  -sinθ ]
    [ sinθ   cosθ ]
```

Each pixel is repositioned using this transformation.

### Method Used (SciPy)

```python
from scipy import ndimage
rotated = ndimage.rotate(image, angle)
```

* Automatically handles resizing to avoid cropping
* Interpolation is applied

### OpenCV Alternative (Interview Tip)

```python
M = cv2.getRotationMatrix2D(center, angle, scale)
rotated = cv2.warpAffine(image, M, (w, h))
```

---

## 2. Mirroring / Flipping

### Concept

* Flips an image across an axis
* Used for **data augmentation** and symmetry handling

### NumPy Method

```python
flipped_v = np.flip(image, 0)  # vertical
flipped_h = np.flip(image, 1)  # horizontal
```

### Axis Meaning

* `axis = 0` → top ↔ bottom
* `axis = 1` → left ↔ right

### OpenCV Alternative

```python
cv2.flip(image, flipCode)
```

* `0` → vertical
* `1` → horizontal
* `-1` → both axes

---

## 3. Image Resizing

### Concept

* Changes image **width and height**
* Used for standardization and performance optimization

### OpenCV Method

```python
resized = cv2.resize(image, (width, height))
```

### Interpolation Methods (Important)

* `INTER_LINEAR` → default
* `INTER_NEAREST` → fastest, blocky
* `INTER_CUBIC` → high quality
* `INTER_AREA` → best for shrinking

---

## 4. Image Translation

### Concept

* Shifts image along x or y direction
* No rotation or scaling involved

### Translation Matrix

```
M = [ 1  0  tx ]
    [ 0  1  ty ]
```

* `tx` → horizontal shift
* `ty` → vertical shift

### OpenCV Method

```python
M = np.float32([[1, 0, tx], [0, 1, ty]])
translated = cv2.warpAffine(image, M, (w, h))
```

---

## 5. Scaling (Often Missed Concept)

### Concept

* Uniform or non-uniform resizing using scale factors

### Scaling Matrix

```
S = [ sx  0 ]
    [ 0  sy ]
```

### OpenCV

```python
scaled = cv2.resize(image, None, fx=sx, fy=sy)
```

---

## 6. Affine Transformation (Generalization)

### Concept

* Combines **translation, rotation, scaling, and shearing**
* Preserves straight lines

### Matrix Form

```
M = [ a  b  tx ]
    [ c  d  ty ]
```

### OpenCV

```python
transformed = cv2.warpAffine(image, M, (w, h))
```

---

## 7. Perspective Transformation (Often Asked)

### Concept

* Handles 3D-like viewpoint changes
* Used in document scanning

### OpenCV

```python
M = cv2.getPerspectiveTransform(src_pts, dst_pts)
warped = cv2.warpPerspective(image, M, (w, h))
```

---

## 8. Key Interview Takeaways

* All geometric transforms are **matrix operations**
* `warpAffine` → 2×3 matrix
* `warpPerspective` → 3×3 matrix
* Interpolation choice affects image quality

---

## 9. One-Line Summary

> Geometric image transformations reposition pixels using **linear algebra and interpolation**.

---
